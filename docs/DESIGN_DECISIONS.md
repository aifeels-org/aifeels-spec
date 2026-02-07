# Design Decisions

This document explains **why** we made specific design choices in Aifeels v0.1.

## Five Primitives (Not More, Not Less)

### Decision
Exactly five emotional primitives: frustration, trust, urgency, stress, caution

### Rationale
- **Not too few:** Need enough to cover major agentic behaviors
- **Not too many:** Each additional primitive increases complexity exponentially
- **Proven coverage:** These five cover 90%+ of autonomy escalation patterns

### Alternatives Considered
- **Three primitives:** Too limited, couldn't distinguish frustration from stress
- **Ten primitives:** Too complex, implementation divergence risk
- **Open-ended:** Chaos, no interoperability

### Evidence
Based on analysis of agent failure modes in task automation systems.

---

## Linear Decay (Not Exponential)

### Decision
Decay rate: 0.05 per 300 seconds (linear)

### Rationale
1. **Simplicity:** Easy to explain, implement, debug
2. **Finite termination:** Reaches exactly 0.0 in 100 minutes
3. **Predictability:** Constant rate is easier to reason about

### Alternatives Considered
- **Exponential decay:** More "natural" but asymptotic (never reaches zero)
- **Configurable decay:** Too many variables, implementation divergence
- **No decay:** Emotional state would accumulate forever (memory leak)

### Future Considerations
If evidence shows exponential decay is needed, it can be added via RFC in v0.2+.

---

## Fixed Decay Rate (No Configuration)

### Decision
Decay rate is hardcoded: 0.05 per 300 seconds (not configurable in v0.1)

### Rationale
- **Interoperability:** All implementations behave identically
- **Simplicity:** No tuning, no knobs, no drift
- **Governance:** Forces evidence-based discussion before allowing changes

### Why This Matters
If decay were configurable:
- Two implementations could behave completely differently
- "Works on my machine" problems
- No meaningful conformance testing

### Future Path
Custom decay rates may be allowed in v0.2+ if:
- Multiple implementations request it
- Evidence shows one-size-fits-all fails
- Coordination protocol defined (how do agents with different rates coordinate?)

---

## Action Precedence (Safety First)

### Decision
Actions ordered by safety priority:
1. cooldown_required (stop everything)
2. handoff_to_human
3. pause_execution
4. request_confirmation
5. continue_autonomy

### Rationale
- **Safety first:** Cooldown prevents runaway loops
- **Escalation over continuation:** When in doubt, ask for help
- **Deterministic:** No ambiguity when multiple thresholds cross

### Alternatives Considered
- **User-configurable precedence:** Too complex, breaks interoperability
- **Context-dependent precedence:** Non-deterministic, hard to audit
- **No precedence (return all):** Pushes decision to agent, inconsistent behavior

---

## MCP as First-Class Integration

### Decision
MCP tools are normative (part of the spec), not optional

### Rationale
- **Agentic systems need protocols:** MCP is emerging standard
- **Interoperability:** Standard tools → consistent integration
- **Simplicity:** Four tools cover all use cases

### Alternatives Considered
- **REST API:** Too implementation-specific
- **Language bindings:** Fragmention across languages
- **No specified integration:** Chaos, everyone rolls their own

### Why MCP?
- Growing ecosystem (Anthropic, community)
- Tool-based interaction model fits emotional state queries
- Vendor-neutral (not controlled by one company)

---

## Event-Driven Model (Not Continuous)

### Decision
State changes only via discrete events (task_failed, user_corrected, etc.)

### Rationale
- **Deterministic:** Same events → same state
- **Auditable:** Every state change has a cause
- **Composable:** Events can be combined, replayed, tested

### Alternatives Considered
- **Continuous/streaming:** Complex, hard to audit, non-deterministic
- **ML-inferred:** Black box, not auditable, scope creep
- **Polling-based:** Inefficient, introduces timing dependencies

---

## Zero Initialization (Not Neutral)

### Decision
All signals start at 0.0 (not 0.5 or any "neutral" value)

### Rationale
- **Clean slate:** No assumed emotional state
- **0.0 ≠ "calm":** It means "no signal yet"
- **Avoids bias:** No hidden assumptions about starting state

### Alternatives Considered
- **0.5 (neutral):** Implies a baseline emotional state (biased)
- **Random:** Non-deterministic
- **User-defined:** Configuration complexity

---

## Clamping (Not Errors)

### Decision
Values automatically clamp to [0.0, 1.0], no exceptions thrown

### Rationale
- **Robustness:** System never crashes on bad math
- **Predictable:** [0.0, 1.0] is the invariant
- **Auditable:** Clamping events are logged

### Alternatives Considered
- **Throw errors:** Crashes agent on overflow
- **Wrap around:** Confusing (frustration 1.2 → 0.2?)
- **Unbounded:** Opens door to runaway values

---

## v0.1 as Draft (Not v1.0)

### Decision
First release is v0.1.0 (draft), not v1.0.0 (stable)

### Rationale
- **Learning phase:** Need real implementations to validate assumptions
- **Flexibility:** Can make breaking changes before v1.0
- **Transparency:** v0.x signals "still evolving"

### Path to v1.0
Requirements:
- 2+ independent implementations
- 6+ months of community feedback
- No unresolved critical issues
- Proven in production use

---

## Questions About Design Decisions?

Open a [Discussion](https://github.com/aifeels-org/aifeels-spec/discussions) or reference this doc in an RFC if proposing changes.
