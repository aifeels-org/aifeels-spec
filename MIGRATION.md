# Migration Guide

This document provides guidance for migrating between versions of the Aifeels specification.

---

## Version 0.1.0 (Current)

**Status:** Initial draft release  
**Release Date:** 2025-02-06

This is the first version. No migration needed.

---

## Future Migrations

### Planned: v0.1.0 → v0.2.0 (Minor)

**Expected:** Q2 2025

**Type:** Additive changes only (backward compatible)

**Potential additions:**
- Additional optional events
- New optional MCP tools
- Enhanced metadata fields
- Performance optimizations

**Migration strategy:**
- Existing implementations continue to work
- New features are opt-in
- No breaking changes to state schema
- Decay rate remains 0.05 per 300 seconds

**What to do:**
1. Review [CHANGELOG.md](CHANGELOG.md) when v0.2.0 releases
2. Determine if new features are relevant to your use case
3. Implement new features at your convenience
4. Re-run conformance tests
5. Update certification if desired

**Breaking changes:** None (guaranteed for minor versions)

---

### Planned: v0.x → v1.0.0 (Major - Stability)

**Expected:** 2025-2026

**Type:** Stabilization (minimal breaking changes expected)

**Goals:**
- Production-ready specification
- API freeze commitment
- Minimum 2 years backward compatibility guarantee

**Potential changes:**
- Schema refinements based on v0.x feedback
- Deprecation of experimental features (if any)
- Performance requirement clarifications

**Migration strategy:**
- Deprecations announced in v0.x releases (minimum 6 months notice)
- Migration guides provided for any breaking changes
- Reference implementation updated with migration examples
- Automated migration tools (if needed)

**What to do:**
1. Monitor RFC process for breaking change proposals
2. Participate in community discussions
3. Test beta/RC versions before final release
4. Budget time for migration (estimate: 1-2 weeks for most implementations)

---

### Future: v1.x → v2.0.0 (Major - Evolution)

**Expected:** 2027+

**Type:** Major evolution (breaking changes allowed)

**Potential areas:**
- Multi-agent coordination
- Long-term emotional memory
- Configurable decay rates
- Composite action triggers
- Real-time streaming events

**Migration strategy:**
- 1 year advance notice for breaking changes
- v1.x continues to receive security patches for 2 years after v2.0 release
- Parallel support period (v1.x and v2.x both maintained)
- Comprehensive migration guide with code examples

**What to do:**
1. Review v2.0 RFC proposals when published
2. Evaluate impact on your implementation
3. Plan migration timeline (6-12 months)
4. Consider supporting both v1.x and v2.x during transition

---

## Migration Principles

### Semantic Versioning

Aifeels follows [Semantic Versioning 2.0.0](https://semver.org/):

- **MAJOR (X.0.0)** - Incompatible API changes
- **MINOR (0.X.0)** - Backward-compatible additions
- **PATCH (0.0.X)** - Backward-compatible bug fixes

### Backward Compatibility Promise

**For v1.0+:**
- MINOR versions: 100% backward compatible
- MAJOR versions: Breaking changes allowed, but migration guide provided
- PATCH versions: Drop-in replacement (no code changes needed)

**For v0.x:**
- Breaking changes allowed with community notice
- Signaled via RFC process
- Migration guidance provided

### Deprecation Policy

**Deprecation timeline:**
1. **Announcement** - Feature marked deprecated in CHANGELOG
2. **Warning period** - Minimum 6 months (v1.0+), 2 months (v0.x)
3. **Removal** - Next MAJOR version only

**Example:**
```
v1.2.0: Feature X deprecated (use Y instead)
v1.3.0-v1.9.x: Feature X works but emits warnings
v2.0.0: Feature X removed
```

---

## Migration Resources

### Official Resources

- **CHANGELOG.md** - Detailed change log for each version
- **RELEASE_NOTES.md** - High-level overview of changes
- **RFC/README.md** - Proposals for future changes
- **GitHub Discussions** - Community migration experiences

### Community Resources

- **Migration examples** - Community-contributed examples (in `examples/migrations/` when available)
- **Stack Overflow** - Tag: `aifeels`
- **Discord/Slack** - Community chat (links TBD)

### Version-Specific Guides

When new versions release, version-specific guides will be published:

- `MIGRATION_0.1_to_0.2.md`
- `MIGRATION_0.x_to_1.0.md`
- `MIGRATION_1.x_to_2.0.md`

---

## Testing Migrations

### Conformance Tests

After migration:

1. **Run conformance suite** - Ensure all tests pass
2. **Verify output** - Check state transitions match expected
3. **Compare versions** - Run both old and new side-by-side
4. **Edge cases** - Test boundary conditions

**Command:**
```bash
git clone https://github.com/aifeels-org/aifeels-conformance-suite
cd aifeels-conformance-suite
./run-tests.sh <your-implementation>
```

### Regression Testing

**Recommended approach:**
1. Export state from old version
2. Import state into new version
3. Verify emotional state values match
4. Apply test events in both versions
5. Compare recommended actions

---

## Rollback Strategy

If migration causes issues:

### Immediate Rollback
- Revert to previous version
- Document issues in GitHub issue
- Wait for patch release

### Partial Migration
- Run old and new versions in parallel
- Gradually migrate traffic
- Monitor for discrepancies

### Version Pinning
- Pin to specific version in dependencies
- Monitor for security patches
- Plan migration at next maintenance window

**Example (Python):**
```python
# requirements.txt
aifeels==0.1.0  # Pinned to avoid breaking changes
```

---

## Breaking Change Impact Assessment

Before migrating to a MAJOR version, assess:

### 1. State Schema Changes
- Do field names change?
- Are fields added/removed?
- Do value ranges change?

### 2. Event Changes
- Are standard events renamed?
- Do event effects change?
- Are events deprecated?

### 3. Action Changes
- Do thresholds change?
- Is precedence reordered?
- Are new actions added?

### 4. MCP Tool Changes
- Do tool signatures change?
- Are tools added/removed?
- Do return formats change?

### 5. Decay Changes
- Does decay formula change?
- Does decay rate change?
- Are custom rates allowed?

**For each "yes":** Review impact on your implementation and plan accordingly.

---

## Migration Checklist

When migrating to a new version:

- [ ] Read CHANGELOG.md for version
- [ ] Read version-specific migration guide
- [ ] Review RFCs for breaking changes
- [ ] Update dependencies
- [ ] Update schemas (if changed)
- [ ] Update event handlers (if changed)
- [ ] Update action logic (if changed)
- [ ] Update MCP tools (if changed)
- [ ] Run conformance tests
- [ ] Update documentation
- [ ] Update certification (if certified)
- [ ] Deploy to staging
- [ ] Monitor for issues
- [ ] Deploy to production

---

## Getting Help

**Migration questions:**
- [GitHub Discussions](https://github.com/aifeels-org/aifeels-spec/discussions) - Tag: "migration"
- [GitHub Issues](https://github.com/aifeels-org/aifeels-spec/issues) - If you find migration bugs

**Urgent migration issues:**
- governance@aifeels.org

**Community support:**
- Join community chat (links TBD)
- Ask on Stack Overflow (tag: `aifeels`)

---

## Version Support Policy

See [RELEASE_PROCESS.md](RELEASE_PROCESS.md) for detailed support policy.

**Summary:**
- **Pre-1.0 (v0.x):** Last minor version only
- **Post-1.0 (v1.x, v2.x):** Last 2 minor versions + 2 years per major version

**Example:**
```
v1.5.0 released: Jan 2027
v2.0.0 released: Jan 2028

Support:
- v1.5.x: Until Jan 2029 (2 years after last 1.x)
- v1.4.x: Until Jan 2028 (when 2.0 ships)
- v2.0.x: Until Jan 2030 (minimum 2 years)
```

---

## Contributing Migration Guides

Help others migrate by:

1. Document your migration experience
2. Share code examples
3. Report migration issues
4. Suggest improvements to migration process

**Submit to:** `examples/migrations/<version>/`

---

*Last Updated: 2025-02-07*  
*Migration Guide Version: 1.0*
