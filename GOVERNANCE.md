# Aifeels Governance

## 1. Project Structure

Aifeels is an **open specification**, not a product or company.

**Repositories:**
- `aifeels-spec` — Normative specification and schemas (this repo)
- `aifeels-reference` — Reference implementation (Python)
- Community implementations — Independent projects

## 2. Roles

### Specification Maintainers
- Review and merge spec changes
- Approve RFCs
- Ensure spec integrity
- Guard against scope creep

**Current maintainers:** See [MAINTAINERS.md](MAINTAINERS.md)

### Contributors
- Submit RFCs
- Report spec ambiguities
- Build implementations
- Participate in discussions

## 3. RFC Process

### When to Submit an RFC

**Required for:**
- New emotional primitives
- Breaking changes to state schema
- New MCP tools (normative)
- Changes to decay semantics
- Changes to action triggers
- Major version bumps (v1.0, v2.0)

**Not required for:**
- Documentation improvements
- Non-normative examples
- Reference implementation bugs
- Typo fixes
- Clarifications (use Issues instead)

### RFC Lifecycle

1. **Draft** — Author writes RFC using RFC/TEMPLATE.md
2. **Discussion** — Community reviews (14 days minimum)
3. **Decision** — Maintainers accept/reject with rationale
4. **Implementation** — Changes merged into spec

See [RFC/README.md](RFC/README.md) for detailed process.

### Acceptance Criteria

RFCs are **accepted** if they:
- ✅ Solve a demonstrated problem (with evidence)
- ✅ Maintain determinism and auditability
- ✅ Don't break existing conformant implementations (unless v2.0+)
- ✅ Include reference implementation or proof of concept
- ✅ Have support from 2+ independent community members

RFCs are **rejected** if they:
- ❌ Add complexity without clear benefit
- ❌ Break core principles (see SPEC.md Section 1)
- ❌ Overlap with existing primitives
- ❌ Are implementation-specific (not spec-level)
- ❌ Advantage specific vendors

## 4. Versioning Policy

### Version Numbers

`MAJOR.MINOR.PATCH` (semantic versioning)

- **MAJOR** — Breaking changes (incompatible state schemas)
- **MINOR** — Additive changes (new optional features)
- **PATCH** — Clarifications, documentation, non-breaking fixes

### Current Version

**0.1.0** — Pre-1.0 draft, breaking changes allowed with notice

### Release Cycle

- v0.x — Pre-1.0, breaking changes allowed with community discussion
- v1.x — Stable, breaking changes only via deprecation path
- v2.x+ — Major revisions with migration guides

### Deprecation Policy

For v1.0+:
1. Feature marked deprecated (MINOR release)
2. Warning period (minimum 6 months)
3. Removal (MAJOR release)
4. Migration guide provided

## 5. Decision Making

### v0.x (Current - Pre-1.0)

- Maintainers have final decision authority
- Community input strongly encouraged via Issues/Discussions
- Speed prioritized for learning and iteration
- Breaking changes allowed with clear rationale

### v1.0+ (Future)

- Formal voting for breaking changes
- Implementation evidence required
- Longer review periods (30+ days)
- Higher bar for acceptance

## 6. Neutrality Principle

**Aifeels must remain vendor-neutral.**

This means:
- No design choices that advantage specific vendors
- No "recommended providers" in normative sections
- No vendor mentions in examples
- Open governance (anyone can contribute)

If a proposal would violate neutrality, it will be rejected.

## 7. Code of Conduct

**Expected:**
- Respectful, constructive dialogue
- Technical focus, evidence-based arguments
- Good-faith engagement
- Assume positive intent

**Unacceptable:**
- Personal attacks
- Scope creep advocacy without RFC
- Vendor-specific demands
- Bad-faith participation

Violations may result in removal from discussions or bans.

## 8. Intellectual Property

All contributions licensed under **Apache 2.0**.

By submitting an RFC, PR, or contribution, you agree to license your work under Apache 2.0 with no additional terms.

**Patent Policy:** See [PATENTS.md](PATENTS.md) for detailed patent non-assertion terms.

**Disclosure:** If you are aware of patents that might affect implementations, you MUST disclose them (see PATENTS.md).

## 9. Errata Process

Errata are errors in the published specification that require correction.

### Reporting Errata

1. Open an issue with title: `[ERRATA] Section X.Y: Brief description`
2. Provide:
   - Specific section reference
   - Description of the error
   - Proposed correction
   - Impact assessment (does it break implementations?)

### Errata Classification

**Editorial (Class E):**
- Typos, formatting, broken links
- No semantic impact
- Fixed in next PATCH release

**Technical (Class T):**
- Incorrect formulas, wrong examples
- Semantic impact but backward compatible
- Fixed in next MINOR release
- May require clarification document before fix

**Critical (Class C):**
- Breaking errors, security issues
- Incompatible implementations possible
- Fixed immediately via emergency PATCH
- Requires public advisory

### Errata List

Maintained at: https://github.com/aifeels-org/aifeels-spec/issues?label=errata

Resolved errata listed in CHANGELOG.md

## 10. Amendment Process

This governance document can be changed via RFC.

Proposed changes must:
- Be submitted as an RFC
- Have clear rationale
- Undergo community review
- Be approved by maintainers

## 11. Contact

**Questions about governance:**  
Open an issue: https://github.com/aifeels-org/aifeels-spec/issues

**Questions about the spec:**  
See [docs/FAQ.md](docs/FAQ.md) or open a discussion

---

*Last updated: 2025-02-06*  
*Governance version: 1.0*
