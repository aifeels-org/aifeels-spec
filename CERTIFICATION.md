# Aifeels Implementation Certification

**Version:** 1.0  
**Last Updated:** 2025-02-07

## Overview

The Aifeels certification program recognizes implementations that demonstrate full conformance to the specification.

Certified implementations can display the **"Aifeels v0.1 Certified"** badge.

## Benefits

- ✅ **Trust** - Users know your implementation follows the standard
- ✅ **Visibility** - Listed in official certified implementations registry
- ✅ **Badge** - Display certification badge in your README
- ✅ **Community** - Join network of conformant implementations

## Requirements

To be certified for Aifeels v0.1.0, implementations MUST:

### 1. Pass All Conformance Tests

Run the [official conformance test suite](https://github.com/aifeels-org/aifeels-conformance-suite):

```bash
git clone https://github.com/aifeels-org/aifeels-conformance-suite
cd aifeels-conformance-suite/validators/<language>
./<validator> /path/to/your/implementation
```

**Required:** 10/10 tests passing (100%)

### 2. Open Source License

Must use a permissive open source license:
- ✅ Apache 2.0 (recommended)
- ✅ MIT
- ✅ BSD (2-clause or 3-clause)
- ❌ GPL (not permissive for certification)

### 3. Documentation

Must include:
- ✅ README with usage examples
- ✅ Installation instructions
- ✅ API documentation
- ✅ Link to Aifeels specification

### 4. Active Maintenance

Must demonstrate:
- ✅ Responds to issues within 30 days
- ✅ Commit activity in last 6 months
- ✅ Clear maintainer contact information

## Certification Process

### Step 1: Self-Test

Run conformance tests locally and ensure 10/10 pass.

### Step 2: Generate Conformance Report

Create report in [standard format](https://github.com/aifeels-org/aifeels-conformance-suite/blob/main/reports/REPORT_FORMAT.md).

Example: [`implementations/certified/aifeels-reference-0.1.0.json`](implementations/certified/aifeels-reference-0.1.0.json)

### Step 3: Submit for Review

1. Fork [aifeels-spec](https://github.com/aifeels-org/aifeels-spec)
2. Add conformance report to `implementations/certified/`
3. Filename: `<implementation-name>-<version>.json`
4. Open Pull Request titled: `[CERTIFICATION] <name> v<version>`

### Step 4: Maintainer Review

Maintainers will (within 14 days):
- ✅ Verify conformance report accuracy
- ✅ Check license compatibility
- ✅ Review documentation quality
- ✅ Run conformance tests independently (if possible)

### Step 5: Approval

Once approved:
- ✅ Added to certified implementations registry
- ✅ Can display certification badge
- ✅ Listed on aifeels.org (when available)
- ✅ Announced in Discussions

## Certification Badge

Once certified, add to your README:

**Markdown:**
```markdown
[![Aifeels v0.1 Certified](https://img.shields.io/badge/Aifeels-v0.1%20Certified-blue)](https://github.com/aifeels-org/aifeels-spec/blob/main/implementations/certified/<your-impl>.json)
```

**Replace `<your-impl>`** with your implementation filename.

## Maintaining Certification

### For Patch Updates (v0.1.0 → v0.1.1)
- Re-run conformance tests
- Update conformance report
- Submit PR to update certification record

### For Minor Updates (v0.1.x → v0.2.x)
- Full re-certification required
- New conformance tests may exist
- Specification may have additive changes

### For Major Updates (v0.x → v1.x)
- Full re-certification required
- Breaking changes expected
- Migration path must be documented

## Revocation

Certification may be revoked if:
- ❌ Implementation found non-conformant
- ❌ Project abandoned (>6 months no activity)
- ❌ License changed to non-permissive
- ❌ Maintainer requests removal

Maintainers will contact before revocation.

## Questions?

- **Certification questions:** certification@aifeels.org
- **Technical questions:** [Discussions](https://github.com/aifeels-org/aifeels-spec/discussions)
- **Issues:** [GitHub Issues](https://github.com/aifeels-org/aifeels-spec/issues)

---

**Ready to get certified?** Start with the [conformance suite](https://github.com/aifeels-org/aifeels-conformance-suite)!
