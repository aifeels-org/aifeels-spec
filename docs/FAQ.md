# Aifeels FAQ

## General Questions

### What is Aifeels?

Aifeels is an open specification for emotional state management in agentic AI systems. It provides a standardized way for autonomous agents to:
- Track their own emotional state (frustration, trust, urgency, etc.)
- Make deterministic decisions based on that state
- Self-regulate autonomy (know when to ask for help)

### Why does this exist?

Modern AI agents can infer emotion from text, but they don't maintain their own emotional state as a decision signal. This creates problems:
- Agents get stuck in infinite loops (high frustration, no self-awareness)
- Handoff timing is arbitrary (no systematic escalation)
- Decisions aren't auditable (why did the agent stop?)

Aifeels solves this by making emotional state a standard primitive.

### Is this trying to simulate human emotions?

**No.** Aifeels is not a psychology framework. It's a system state model. The "emotions" are just numerical signals that represent system-relevant conditions (like "repeated failures" or "time pressure").

### Who should use Aifeels?

Anyone building autonomous AI agents that need to:
- Self-regulate based on task success/failure
- Escalate to humans intelligently
- Make auditable autonomy decisions
- Coordinate with other agents (future)

## Technical Questions

### Why only 5 primitives?

Minimalism reduces complexity and divergence risk. We can add more in future versions if proven necessary via RFCs.

The five primitives (frustration, trust, urgency, stress, caution) were chosen because they:
- Map to agentic behaviors (not human psychology)
- Cover the most common escalation patterns
- Don't overlap significantly

### Why linear decay instead of exponential?

Simpler to understand, implement, and debug. Linear decay guarantees reaching zero in finite time (100 minutes from max). Exponential decay is asymptotic, which can cause edge cases.

See SPEC.md Section 5.1 for the decay formula.

### Can I customize decay rates?

Not in v0.1. All implementations MUST use 0.05 per 300 seconds. This ensures interoperability.

Custom decay rates may be considered for v0.2 if there's strong evidence they're needed. Submit an RFC.

### Can I add custom emotional primitives?

Not in v0.1. The five primitives are fixed.

To propose a new primitive for v0.2+:
1. Submit an RFC
2. Provide evidence it's needed (real use cases)
3. Show it doesn't overlap with existing primitives
4. Include reference implementation

See RFC/TEMPLATE.md.

### What's the difference between `frustration` and `stress`?

- **Frustration** — Repeated failures, blockers (task-level)
- **Stress** — Resource constraints, parallel demands (system-level)

Example: An agent with high frustration (task keeps failing) but low stress (plenty of resources) behaves differently than high frustration + high stress (overwhelmed).

### How does `trust` work?

`trust` represents confidence in the environment's stability and tool reliability.

- **Increases** when tasks succeed, tools work, user approves
- **Decreases** when tasks fail, tools error, user corrects

Low trust triggers caution (request confirmation before proceeding).

### What happens when multiple thresholds trigger?

Actions are selected by precedence (see SPEC.md Section 6.3):
1. `cooldown_required` (highest priority)
2. `handoff_to_human`
3. `pause_execution`
4. `request_confirmation`
5. `continue_autonomy` (default)

The highest-precedence action wins. Others are logged but not executed.

### Can I ignore the recommended action?

Yes. Aifeels provides a **recommendation**, not a mandate. The agent can override it.

However, overrides SHOULD be logged for auditability.

## Implementation Questions

### How do I implement Aifeels?

See [IMPLEMENTATION_ARCHITECTURE.md](IMPLEMENTATION_ARCHITECTURE.md) for detailed guidance.

Quick start:
1. Read SPEC.md
2. Implement the state model (Section 3)
3. Implement event handling (Section 4)
4. Implement decay (Section 5)
5. Implement action selection (Section 6)
6. Expose MCP tools (Section 7)
7. Pass conformance tests (Section 10)

### What languages are supported?

Aifeels is a **specification**, not a library. You can implement it in any language.

**Current implementations:**
- Python (reference, in progress)

**Want to build one?** Follow the spec and submit it to the community!

### Do I need to use MCP?

No, but it's recommended. MCP is the primary integration method defined in the spec.

You can expose Aifeels state via:
- MCP tools (recommended, see Section 7)
- REST API (implementation-specific)
- Language bindings (implementation-specific)

### How do I test my implementation?

Use the conformance test vectors in SPEC.md Section 10.4.

Your implementation MUST:
- Produce identical output for the same input
- Handle all 13 standard events
- Apply decay correctly
- Select actions by precedence

### Can I use this in production?

v0.1 is a **draft**. Breaking changes may occur before v1.0.

For production use:
- Pin to a specific version
- Monitor the RFC process
- Plan for migration

## Governance Questions

### Who owns Aifeels?

No one. It's an open standard governed by the community.

The initial steward is listed in GOVERNANCE.md, but ownership is shared via the RFC process.

### How do I propose changes?

For small changes (typos, clarifications): Submit a PR

For large changes (new features, breaking changes): Submit an RFC

See [GOVERNANCE.md](../GOVERNANCE.md) and [RFC/README.md](../RFC/README.md).

### Is this vendor-neutral?

**Yes.** Aifeels is intentionally vendor-neutral. No company owns it, controls it, or benefits preferentially from it.

If you spot vendor bias, report it immediately.

### Can companies build on this?

**Absolutely.** That's the point. Aifeels is Apache 2.0 licensed.

Companies can:
- Build products that use Aifeels
- Integrate Aifeels into commercial agents
- Offer Aifeels-compliant services

They cannot:
- Claim ownership of the spec
- Change the spec unilaterally
- Prevent others from using it

## Still Have Questions?

- **Spec clarification:** Open an [Issue](https://github.com/aifeels-org/aifeels-spec/issues)
- **General discussion:** Start a [Discussion](https://github.com/aifeels-org/aifeels-spec/discussions)
- **Propose a change:** Submit an [RFC](../RFC/README.md)
