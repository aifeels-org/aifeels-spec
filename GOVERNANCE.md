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

## 11. Succession Planning

### Lead Maintainer Unavailability

If the lead maintainer becomes unavailable:

**Short-term (< 30 days):**
- Other maintainers (if any) continue RFC reviews
- Non-urgent decisions deferred
- Emergency security patches allowed
- Community discussions continue

**Long-term (> 30 days):**
- Remaining maintainers elect new lead (simple majority)
- If no remaining maintainers, community nominates interim maintainer
- Succession announced publicly in Discussions
- New lead added to MAINTAINERS.md

### Bus Factor Mitigation

Current measures:
- All processes documented in this GOVERNANCE.md
- Specification is self-contained in SPEC.md
- RFC process ensures community input
- GitHub contains complete project history

**Goals (by v1.0):**
- Minimum 2 active maintainers
- Geographic and organizational diversity
- Documented knowledge transfer process

### Emergency Contact

If maintainers are unreachable: governance@aifeels.org

(Monitored by multiple parties for continuity)

---

## 12. Technical Steering Committee (Future)

### Formation Criteria

A Technical Steering Committee (TSC) will be formed when:
- Project has 5+ regular contributors
- 3+ independent implementations exist
- RFC volume exceeds single maintainer capacity

### TSC Structure

**Size:** 5-7 members

**Composition:**
- Active maintainers (2 seats)
- Implementation authors (2-3 seats)
- Community representatives (1-2 seats)

**Terms:**
- 1 year, renewable
- Staggered terms (not all expire simultaneously)

**Selection:**
- Maintainers: Self-appointed
- Others: Community nomination + vote

### TSC Responsibilities

- Approve RFCs requiring TSC review
- Resolve maintainer conflicts
- Set strategic direction (roadmap)
- Manage trademark and certification
- Appoint new maintainers

### TSC Decision Making

- **Quorum:** 60% of members
- **Simple majority:** Most decisions
- **2/3 majority:** Breaking changes, trademark policy
- **All votes:** Documented publicly in Discussions

---

## 13. Conflict Resolution

### RFC Disagreements

1. **Discussion (14+ days):** Community discusses in RFC
2. **Maintainer vote:** Accept or reject with rationale
3. **Appeal:** Submitter can appeal with new evidence (7 days)
4. **Final decision:** Maintainers have final authority

### Maintainer Conflicts

When maintainers disagree:

1. **Private discussion** - Attempt consensus
2. **Vote** - Simple majority if no consensus
3. **Tie** - Status quo prevails (no change)
4. **Escalation** - If serious, involve TSC (when formed)

### Community Disputes

1. **Code of Conduct** - All disputes subject to CODE_OF_CONDUCT.md
2. **Reporting** - governance@aifeels.org
3. **Investigation** - Maintainers investigate (7 days)
4. **Resolution** - Warning, temp ban (7-30 days), or permanent ban
5. **Appeal** - 14 days to appeal to different maintainer

### Vendor Neutrality Violations

If a decision appears to favor specific vendor:

1. **Report** - governance@aifeels.org with evidence
2. **Review** - Maintainers review decision (14 days)
3. **Reversal** - If confirmed, decision reversed
4. **Transparency** - Outcome announced publicly

---

## 14. Emergency Procedures

### Security Vulnerabilities

**Specification-level security issues:**

1. **Report** - security@aifeels.org (private)
2. **Acknowledgment** - Within 7 days
3. **Assessment** - Severity and impact (14 days)
4. **Fix** - Develop patch (target 30 days)
5. **Disclosure** - 90 days or when fix ready (whichever sooner)
6. **Announcement** - Public advisory with CVE (if applicable)

**See SECURITY.md for complete process.**

### Critical Spec Bugs

If spec bug discovered that:
- Breaks all implementations
- Creates security risk
- Makes spec unusable

**Emergency process:**

1. **Immediate acknowledgment** - Issue labeled "critical"
2. **Expedited RFC** - 3-day review (vs. 14 days)
3. **Patch release** - v0.1.1 with fix
4. **Announcement** - All channels (GitHub, Discussions)
5. **Migration guide** - Provided with patch

### Maintainer Incapacity

If all maintainers become unavailable:

1. **Contact** - governance@aifeels.org
2. **Interim** - Community nominates interim maintainer (Discussions)
3. **Vote** - Community votes on interim (7 days)
4. **Authority** - Interim has limited authority:
   - Can merge security patches
   - Can moderate discussions
   - Cannot approve breaking changes
5. **Restoration** - When original maintainers return or permanent replacement selected

---

## 15. Governance Version History

This governance document is versioned:

| Version | Date | Changes |
|---------|------|---------|
| 2.0 | 2025-02-07 | Added succession planning, TSC, conflict resolution, emergency procedures |
| 1.0 | 2025-02-06 | Initial governance framework |

**Material changes** to governance require:
- RFC with 30-day review period
- Community consensus
- Maintainer approval

---

## 16. Contact

**Questions about governance:**  
Open an issue: https://github.com/aifeels-org/aifeels-spec/issues

**Questions about the spec:**  
See [docs/FAQ.md](docs/FAQ.md) or open a discussion

---

*Last Updated: 2025-02-07*  
*Governance Version: 2.0*
