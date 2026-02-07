# Implementation Architecture Guide

This document provides architectural guidance for building conformant Aifeels implementations.

---

## Overview

An Aifeels implementation consists of:
1. **State Manager** — Maintains emotional state
2. **Event Processor** — Applies events to state
3. **Decay Engine** — Handles temporal dynamics
4. **Action Evaluator** — Recommends actions based on thresholds
5. **MCP Server** — Exposes state via MCP tools
6. **Audit Logger** — Records all state transitions

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                      Agent/Application                       │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           │ MCP Protocol
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                    MCP Server Layer                          │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ get_emotional_state()                                  │ │
│  │ update_emotional_state(event)                          │ │
│  │ evaluate_emotional_risk()                              │ │
│  │ recommended_action()                                   │ │
│  └────────────────────────┬───────────────────────────────┘ │
└───────────────────────────┼─────────────────────────────────┘
                            │
┌───────────────────────────▼─────────────────────────────────┐
│                    Core Engine                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │State Manager │  │Event         │  │Action        │      │
│  │              │◄─┤Processor     │  │Evaluator     │      │
│  │- Current     │  │              │  │              │      │
│  │  state       │  │- Apply       │  │- Threshold   │      │
│  │- Metadata    │  │  events      │  │  checks      │      │
│  │              │  │- Validate    │  │- Precedence  │      │
│  └──────┬───────┘  └──────────────┘  └──────────────┘      │
│         │                                                    │
│  ┌──────▼───────┐  ┌──────────────┐  ┌──────────────┐      │
│  │Decay Engine  │  │Audit Logger  │  │Storage       │      │
│  │              │  │              │  │              │      │
│  │- Linear      │  │- Event log   │  │- Persist     │      │
│  │  decay       │  │- State log   │  │  state       │      │
│  │- Time calc   │  │- Action log  │  │- Load state  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

---

## Component Specifications

### 1. State Manager

**Responsibilities:**
- Maintain current emotional state (5 primitives + metadata)
- Ensure values stay in [0.0, 1.0]
- Update metadata (last_updated, trend, confidence)

**Data Structure:**
```python
class EmotionalState:
    frustration: float  # [0.0, 1.0]
    trust: float        # [0.0, 1.0]
    urgency: float      # [0.0, 1.0]
    stress: float       # [0.0, 1.0]
    caution: float      # [0.0, 1.0]
    
    metadata: StateMetadata
    
class StateMetadata:
    last_updated: datetime  # ISO 8601
    trend: str              # "increasing" | "decreasing" | "stable"
    confidence: float       # [0.5, 1.0]
```

**Key Operations:**
- `get_state()` — Returns current state (with decay applied)
- `set_signal(name, value)` — Sets a signal value (with clamping)
- `clamp(value)` — Ensures value is in [0.0, 1.0]
- `update_metadata()` — Recalculates trend and confidence

---

### 2. Event Processor

**Responsibilities:**
- Validate event structure
- Apply event effects to state
- Handle multiple simultaneous events
- Log all events

**Event Structure:**
```python
class Event:
    event_type: str      # e.g., "task_failed"
    timestamp: datetime  # ISO 8601
    context: dict        # Optional additional data
```

**Key Operations:**
- `validate_event(event)` — Checks event structure
- `apply_event(event, state)` — Modifies state based on event
- `apply_effects(effects, state)` — Applies effect deltas
- `clamp_state(state)` — Ensures all signals in bounds

**Effect Application:**
```python
def apply_event(event: Event, state: EmotionalState):
    effects = EVENT_EFFECTS[event.event_type]
    
    for signal, delta in effects.items():
        new_value = getattr(state, signal) + delta
        setattr(state, signal, clamp(new_value))
    
    state.metadata.last_updated = event.timestamp
    update_trend(state)
```

---

### 3. Decay Engine

**Responsibilities:**
- Calculate elapsed time since last update
- Apply linear decay to all signals
- MUST be called before every state read

**Decay Formula (from SPEC.md Section 5.1):**
```
new_value = max(0.0, current_value - (elapsed_seconds / 300.0 * 0.05))
```

**Key Operations:**
```python
def apply_decay(state: EmotionalState, current_time: datetime):
    elapsed = (current_time - state.metadata.last_updated).total_seconds()
    decay_amount = (elapsed / 300.0) * 0.05
    
    state.frustration = max(0.0, state.frustration - decay_amount)
    state.trust = max(0.0, state.trust - decay_amount)
    state.urgency = max(0.0, state.urgency - decay_amount)
    state.stress = max(0.0, state.stress - decay_amount)
    state.caution = max(0.0, state.caution - decay_amount)
    
    state.metadata.last_updated = current_time
```

**CRITICAL:** Decay MUST be applied:
- Before every `get_state()` call
- Before every `recommended_action()` call
- Before every threshold check

---

### 4. Action Evaluator

**Responsibilities:**
- Check all action thresholds
- Apply precedence when multiple trigger
- Return single recommended action

**Thresholds (from SPEC.md Section 6.2):**
```python
THRESHOLDS = {
    "continue_autonomy": None,  # Default
    "request_confirmation": lambda s: s.frustration >= 0.70 or s.caution >= 0.60,
    "pause_execution": lambda s: s.stress >= 0.70 or s.urgency >= 0.80,
    "handoff_to_human": lambda s: s.frustration >= 0.80 or s.trust <= 0.20,
    "cooldown_required": lambda s: s.frustration >= 0.75 and s.stress >= 0.75,
}
```

**Precedence (highest to lowest):**
1. cooldown_required
2. handoff_to_human
3. pause_execution
4. request_confirmation
5. continue_autonomy

**Key Operations:**
```python
def recommended_action(state: EmotionalState) -> str:
    # Apply decay first!
    state = apply_decay(state, now())
    
    # Check in precedence order
    if THRESHOLDS["cooldown_required"](state):
        return "cooldown_required"
    if THRESHOLDS["handoff_to_human"](state):
        return "handoff_to_human"
    if THRESHOLDS["pause_execution"](state):
        return "pause_execution"
    if THRESHOLDS["request_confirmation"](state):
        return "request_confirmation"
    return "continue_autonomy"
```

---

### 5. MCP Server

**Responsibilities:**
- Expose four required tools
- Handle tool invocations
- Return results in MCP format

**Required Tools (from SPEC.md Section 7.2):**

#### `get_emotional_state`
```python
def get_emotional_state() -> dict:
    state = state_manager.get_state()  # Applies decay
    return {
        "frustration": state.frustration,
        "trust": state.trust,
        "urgency": state.urgency,
        "stress": state.stress,
        "caution": state.caution,
        "metadata": {
            "last_updated": state.metadata.last_updated.isoformat(),
            "trend": state.metadata.trend,
            "confidence": state.metadata.confidence,
        }
    }
```

#### `update_emotional_state`
```python
def update_emotional_state(event_type: str, timestamp: str, context: dict = None) -> dict:
    event = Event(
        event_type=event_type,
        timestamp=datetime.fromisoformat(timestamp),
        context=context or {}
    )
    
    event_processor.validate_event(event)
    event_processor.apply_event(event, state_manager.state)
    audit_logger.log_event(event)
    
    return get_emotional_state()
```

#### `evaluate_emotional_risk`
```python
def evaluate_emotional_risk() -> dict:
    state = state_manager.get_state()  # Applies decay
    
    risks = []
    if state.frustration >= 0.70:
        risks.append("high_frustration")
    if state.trust <= 0.30:
        risks.append("low_trust")
    if state.stress >= 0.70:
        risks.append("high_stress")
    if state.frustration >= 0.75 and state.stress >= 0.75:
        risks.append("critical_overload")
    
    return {
        "risk_level": "critical" if len(risks) >= 2 else "moderate" if risks else "low",
        "risk_factors": risks,
        "requires_attention": len(risks) > 0,
    }
```

#### `recommended_action`
```python
def recommended_action() -> dict:
    state = state_manager.get_state()  # Applies decay
    action = action_evaluator.recommended_action(state)
    
    return {
        "action": action,
        "reason": generate_reason(action, state),
        "current_state": get_emotional_state(),
    }
```

---

### 6. Audit Logger

**Responsibilities:**
- Log all events
- Log all state changes
- Log all actions
- Provide log export

**Log Entries:**
```python
class LogEntry:
    timestamp: datetime
    entry_type: str  # "event" | "state" | "action"
    data: dict
```

**Key Operations:**
- `log_event(event)` — Records event application
- `log_state(state)` — Records state snapshot
- `log_action(action, reason)` — Records action recommendation
- `export_logs(format)` — Exports logs for audit

---

## Implementation Patterns

### Pattern 1: Stateless Implementation

**Use case:** Simple agents, short-lived sessions

```python
class StatelessAifeels:
    def __init__(self):
        self.state = EmotionalState.zero()
    
    def handle_event(self, event):
        self.state = apply_decay(self.state, now())
        apply_event(event, self.state)
        return self.state
    
    def get_action(self):
        self.state = apply_decay(self.state, now())
        return recommended_action(self.state)
```

---

### Pattern 2: Persistent Implementation

**Use case:** Long-running agents, multi-session

```python
class PersistentAifeels:
    def __init__(self, storage_path):
        self.storage = Storage(storage_path)
        self.state = self.storage.load_state() or EmotionalState.zero()
    
    def handle_event(self, event):
        self.state = apply_decay(self.state, now())
        apply_event(event, self.state)
        self.storage.save_state(self.state)
        return self.state
    
    def get_action(self):
        self.state = apply_decay(self.state, now())
        return recommended_action(self.state)
```

---

### Pattern 3: Multi-Agent Implementation

**Use case:** Multiple agents, isolated states

```python
class MultiAgentAifeels:
    def __init__(self):
        self.states = {}  # agent_id -> EmotionalState
    
    def get_state(self, agent_id):
        if agent_id not in self.states:
            self.states[agent_id] = EmotionalState.zero()
        
        state = self.states[agent_id]
        return apply_decay(state, now())
    
    def handle_event(self, agent_id, event):
        state = self.get_state(agent_id)
        apply_event(event, state)
        return state
```

---

## Testing Strategy

### Unit Tests

**State Manager:**
- Test clamping (values always [0.0, 1.0])
- Test metadata updates
- Test serialization/deserialization

**Event Processor:**
- Test all 13 standard events
- Test effect application
- Test event validation

**Decay Engine:**
- Test decay calculation
- Test elapsed time handling
- Test zero floor

**Action Evaluator:**
- Test all threshold checks
- Test precedence ordering
- Test edge cases (exact threshold values)

---

### Integration Tests

**Event Sequences:**
```python
def test_failure_escalation():
    aifeels = Aifeels()
    
    # First failure
    aifeels.handle_event(Event("task_failed", now()))
    assert aifeels.get_action() == "continue_autonomy"
    
    # Second failure
    aifeels.handle_event(Event("task_failed", now()))
    assert aifeels.get_action() == "continue_autonomy"
    
    # Third failure → crosses threshold
    aifeels.handle_event(Event("task_failed", now()))
    assert aifeels.get_action() == "request_confirmation"
```

---

### Conformance Tests

**Use SPEC.md Section 10.4 test vectors:**

```python
def test_conformance_vector_1():
    """Test 1: Initialization"""
    aifeels = Aifeels()
    state = aifeels.get_state()
    
    assert state.frustration == 0.0
    assert state.trust == 0.0
    assert state.urgency == 0.0
    assert state.stress == 0.0
    assert state.caution == 0.0
```

---

## Performance Considerations

### Memory
- State: ~200 bytes (5 floats + metadata)
- Event log: ~100 bytes per event
- Use circular buffers for log retention

### Latency
- State read: <1ms (decay calculation + dict access)
- Event application: <1ms (delta sum + clamping)
- Action evaluation: <1ms (5 threshold checks)

### Optimization Tips
1. Cache decay calculations (invalidate on event)
2. Pre-compute threshold checks
3. Use efficient serialization (MessagePack, Protocol Buffers)
4. Batch event processing when possible

---

## Common Pitfalls

### ❌ Forgetting Decay
```python
# WRONG: State returned without decay
def get_state(self):
    return self.state  # Stale!
```

```python
# CORRECT: Always apply decay before read
def get_state(self):
    self.state = apply_decay(self.state, now())
    return self.state
```

---

### ❌ Not Clamping
```python
# WRONG: Values can go out of bounds
def apply_event(event, state):
    state.frustration += 0.3  # Could exceed 1.0
```

```python
# CORRECT: Always clamp
def apply_event(event, state):
    state.frustration = clamp(state.frustration + 0.3)
```

---

### ❌ Wrong Precedence
```python
# WRONG: Checking in wrong order
if frustration >= 0.70:
    return "request_confirmation"
if frustration >= 0.80:  # Never reached!
    return "handoff_to_human"
```

```python
# CORRECT: Check highest precedence first
if frustration >= 0.80:
    return "handoff_to_human"
if frustration >= 0.70:
    return "request_confirmation"
```

---

## Deployment Checklist

- [ ] All 5 primitives implemented
- [ ] All 13 standard events supported
- [ ] Decay applied before every read
- [ ] Clamping enforced
- [ ] Thresholds match spec
- [ ] Precedence ordering correct
- [ ] All 4 MCP tools exposed
- [ ] Audit logging enabled
- [ ] Conformance tests passing
- [ ] Documentation complete

---

## Resources

- [SPEC.md](../SPEC.md) - Normative specification
- [FAQ.md](FAQ.md) - Common questions
- [DESIGN_DECISIONS.md](DESIGN_DECISIONS.md) - Why we made these choices

---

## Questions?

Open a [Discussion](https://github.com/aifeels-org/aifeels-spec/discussions) or [Issue](https://github.com/aifeels-org/aifeels-spec/issues).
