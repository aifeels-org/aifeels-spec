# Aifeels Specification

> An open standard for emotional state in agentic AI systems

## Overview

Aifeels is a vendor-neutral, open specification that defines how autonomous AI agents track and manage their own emotional state. Unlike sentiment analysis tools that infer emotion from text, Aifeels provides a standardized system for agents to maintain emotional signals (frustration, trust, urgency, stress, caution) that guide autonomy decisions.

This enables agents to:
- Self-regulate based on task success/failure patterns
- Make deterministic, auditable decisions about when to escalate
- Coordinate autonomy across multi-step workflows
- Maintain transparency about their decision-making process

## Current Status

**Version:** 0.1.0 (Draft)

- ✅ Core specification complete
- ✅ Five emotional primitives defined
- ✅ Event-driven state transitions
- ✅ MCP integration specified
- 🚧 Reference implementation in progress
- 🚧 Community review period

## Problem Statement

Modern autonomous agents face a critical gap: they can infer emotion from text, but they don't maintain their own emotional state as a decision signal. This leads to:

- **Runaway loops:** Agents repeatedly attempt failing tasks without self-awareness
- **Arbitrary escalation:** Handoff timing is ad-hoc, not systematic
- **Non-auditable decisions:** No clear record of why an agent stopped or escalated
- **Coordination failures:** Agents in multi-step workflows can't share autonomy context

Aifeels solves this by making emotional state a first-class primitive in agentic systems.

## Specification

The complete normative specification is available in [SPEC.md](SPEC.md).

### Quick Example

```json
{
  "frustration": 0.75,
  "trust": 0.3,
  "urgency": 0.6,
  "stress": 0.5,
  "caution": 0.4,
  "metadata": {
    "last_updated": "2025-02-06T14:30:00Z",
    "trend": "increasing",
    "confidence": 0.9
  }
}
```

After three consecutive tool errors, the agent's frustration crosses the 0.70 threshold, triggering `request_confirmation` before proceeding. If failures continue, frustration reaches 0.80, escalating to `handoff_to_human`. Every state change is auditable with full event history.

## Implementations

**Reference Implementation (Python):**  
https://github.com/aifeels-org/aifeels-reference *(coming soon)*

**Community Implementations:**
- *None yet - be the first!*

Want to build an implementation? See [docs/IMPLEMENTATION_ARCHITECTURE.md](docs/IMPLEMENTATION_ARCHITECTURE.md)

## Governance

This is an open standard governed by the community. See [GOVERNANCE.md](GOVERNANCE.md) for:
- RFC process
- Decision-making
- How to contribute

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

Apache 2.0 - See [LICENSE](LICENSE)

## Resources

- [Specification](SPEC.md) - Normative technical specification
- [Release Notes](RELEASE_NOTES.md) - What's new in v0.1.0
- [Governance](GOVERNANCE.md) - How decisions are made
- [Implementation Architecture](docs/IMPLEMENTATION_ARCHITECTURE.md) - How to build a conformant implementation
- [RFC Process](RFC/README.md) - How to propose changes
- [FAQ](docs/FAQ.md) - Common questions

## Contact

- Issues: https://github.com/aifeels-org/aifeels-spec/issues
- Discussions: https://github.com/aifeels-org/aifeels-spec/discussions
