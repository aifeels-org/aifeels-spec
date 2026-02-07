# RFC Process

Request for Comments (RFC) is how we propose and discuss changes to the Aifeels specification.

## When to Submit an RFC

### ✅ RFC Required

- New emotional primitives
- Changes to existing primitives
- Breaking changes to state schema
- New normative MCP tools
- Changes to decay semantics
- Changes to action triggers or thresholds
- Major version bumps

### ❌ RFC Not Required

- Documentation improvements
- Typo fixes
- Non-normative examples
- Clarifications (use GitHub Issues)
- Reference implementation changes

## RFC Lifecycle

```
Draft → Discussion (14+ days) → Decision → Implementation
```

### 1. Draft
- Copy `TEMPLATE.md`
- Fill out all sections
- Submit as PR to `RFC/` directory
- Naming: `RFC-NNNN-short-title.md` (number assigned by maintainers)

### 2. Discussion
- Minimum 14 days for community review
- Author responds to feedback
- Revisions incorporated
- Technical concerns addressed

### 3. Decision
Maintainers decide:
- **Accepted** — Merge RFC, implement in spec
- **Rejected** — Close with rationale
- **Deferred** — Needs more evidence/work

### 4. Implementation
- Update SPEC.md
- Update schemas if needed
- Add to CHANGELOG.md
- Update version if breaking

## Acceptance Criteria

RFCs are accepted if they:
1. Solve a real, demonstrated problem
2. Maintain determinism and auditability
3. Don't break existing implementations (unless v2.0+)
4. Include implementation evidence
5. Have community support (2+ independent voices)

RFCs are rejected if they:
1. Add complexity without clear benefit
2. Violate core principles (see SPEC.md Section 1)
3. Overlap with existing features
4. Are implementation-specific
5. Advantage specific vendors

## Current RFCs

### Active
- None yet - be the first!

### Accepted
- None yet

### Rejected
- None yet

## Questions?

See [GOVERNANCE.md](../GOVERNANCE.md) or open a Discussion.
