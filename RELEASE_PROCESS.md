# Release Process

This document describes how new versions of the Aifeels specification are released.

---

## Release Types

### PATCH (0.1.X)
**Examples:** 0.1.0 → 0.1.1

**Scope:**
- Typo fixes
- Clarifications (no semantic changes)
- Documentation improvements
- Schema formatting (no behavioral changes)

**Process:**
1. Fix applied to `main` branch
2. Update CHANGELOG.md
3. Tag: `git tag v0.1.1`
4. Push: `git push --tags`
5. Create GitHub release (automated)

**Timeline:** As needed (no formal schedule)

---

### MINOR (0.X.0)
**Examples:** 0.1.0 → 0.2.0

**Scope:**
- New optional features
- New events (backward compatible)
- New MCP tools (optional)
- New examples, test vectors
- Performance improvements (if backward compatible)

**Process:**
1. RFC(s) approved for new features
2. Create release branch: `release/0.2.0`
3. Implement approved changes
4. Update SPEC.md, CHANGELOG.md, RELEASE_NOTES.md
5. Community review period (14 days minimum)
6. Merge to `main`
7. Tag: `git tag v0.2.0`
8. Create GitHub release with release notes
9. Announce on discussions, blog, social media

**Timeline:** Quarterly (or as needed based on RFC backlog)

---

### MAJOR (X.0.0)
**Examples:** 0.9.0 → 1.0.0, 1.5.0 → 2.0.0

**Scope:**
- Breaking changes to state schema
- Removal of deprecated features
- Incompatible event changes
- Major architectural shifts

**Special case: 0.x → 1.0**
- Stability promise (API freeze)
- Production-ready declaration
- Minimum 2 conformant implementations required

**Process:**
1. RFC(s) approved for breaking changes
2. Announce intent (30 days before work begins)
3. Create release branch: `release/1.0.0`
4. Implement changes
5. Update all documentation
6. Migration guide written
7. Extended community review (30 days minimum)
8. Final call for objections (7 days)
9. Merge to `main`
10. Tag: `git tag v1.0.0`
11. Major announcement (blog post, press release if warranted)

**Timeline:** 
- v1.0: When stable (minimum 6 months from v0.1)
- v2.0+: As needed (minimum 2 years between major versions)

---

## Pre-Release Versions

### Alpha (X.Y.Z-alpha.N)
**Example:** 0.2.0-alpha.1

**Purpose:** Early testing of features

**Stability:** Unstable, may change

### Beta (X.Y.Z-beta.N)
**Example:** 0.2.0-beta.1

**Purpose:** Feature-complete, testing for bugs

**Stability:** No new features, only fixes

### Release Candidate (X.Y.Z-rc.N)
**Example:** 1.0.0-rc.1

**Purpose:** Final validation before release

**Stability:** Only critical fixes

---

## Release Checklist

### Before Release

- [ ] All approved RFCs implemented
- [ ] SPEC.md updated
- [ ] CHANGELOG.md updated
- [ ] RELEASE_NOTES.md updated (MINOR/MAJOR only)
- [ ] VERSION file updated
- [ ] All examples validate against schemas
- [ ] CI/CD passes (no broken links, no vendor mentions)
- [ ] Conformance tests updated (if applicable)
- [ ] Migration guide written (MAJOR only)
- [ ] Community review period completed

### During Release

- [ ] Create release branch (MINOR/MAJOR)
- [ ] Final review by all maintainers
- [ ] Tag version: `git tag vX.Y.Z`
- [ ] Push tag: `git push --tags`
- [ ] Create GitHub release with notes
- [ ] Update website (if exists)

### After Release

- [ ] Announce on GitHub Discussions
- [ ] Announce on social media (if major)
- [ ] Update implementations list
- [ ] Archive previous version docs (MAJOR only)
- [ ] Close implemented RFCs
- [ ] Update roadmap

---

## Version Support Policy

### Pre-1.0 (0.x)
- **Support:** Best effort
- **Breaking changes:** Allowed with notice
- **Patch support:** Last minor only (e.g., only 0.2.x gets patches)

### Post-1.0 (1.x, 2.x, etc.)
- **Support:** 2 years minimum for each major version
- **Breaking changes:** Only in major versions
- **Patch support:** Last 2 minors (e.g., 1.4.x and 1.5.x)
- **Security fixes:** All supported versions

**Example timeline:**
```
1.0.0 released: Jan 2026
1.5.0 released: Jan 2027
2.0.0 released: Jan 2028

Support ends:
- 1.0-1.4: Jan 2028 (when 2.0 ships)
- 1.5: Jan 2029 (2 years from last 1.x)
- 2.0: Jan 2030 (minimum 2 years)
```

---

## Emergency Releases

For critical security issues or spec-breaking bugs:

1. **Identification:** Issue marked `critical` by maintainers
2. **Fix:** Hotfix branch created immediately
3. **Review:** Expedited review (24-48 hours)
4. **Release:** PATCH version bump
5. **Announcement:** Security advisory posted

**Example:** 0.1.0 → 0.1.1 (critical decay bug)

---

## Deprecation Process

When deprecating features:

1. **Announce:** Feature marked deprecated in CHANGELOG
2. **Grace period:** Minimum 6 months (1.0+), minimum 2 months (0.x)
3. **Documentation:** Migration guide provided
4. **Warnings:** Reference implementation emits warnings
5. **Removal:** Next MAJOR version only

**Example:**
```
1.3.0: Feature X deprecated, use Y instead
1.4.0-1.9.x: Feature X works but warns
2.0.0: Feature X removed
```

---

## Questions?

Release process questions → Open a [Discussion](https://github.com/aifeels-org/aifeels-spec/discussions)

---

*Last updated: 2025-02-06*  
*Process version: 1.0*
