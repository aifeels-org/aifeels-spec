# Aifeels Implementations

This directory tracks implementations of the Aifeels specification.

## Certified Implementations (v0.1.0)

These implementations have passed all conformance tests:

| Implementation | Language | Version | Certification Date | Maintainer |
|---------------|----------|---------|-------------------|------------|
| [aifeels-reference](certified/aifeels-reference-0.1.0.json) | Python | 0.1.0 | 2025-02-07 | Aifeels Maintainers |

## Community Implementations

Implementations in development or not yet certified:

*None yet - be the first! Submit a PR to add your implementation.*

## Submit Your Implementation

### For Certification

See [CERTIFICATION.md](../CERTIFICATION.md) for the certification process.

**Requirements:**
- Pass all 10 conformance tests
- Open source license (Apache 2.0, MIT, BSD)
- Complete documentation
- Active maintenance

### For Community Listing

To list an uncertified implementation:

1. Fork this repository
2. Add entry to Community Implementations table above
3. Include: name (with repo link), language, status, maintainer
4. Open Pull Request

**Format:**
```markdown
| [impl-name](https://github.com/org/repo) | Language | In Development | @maintainer |
```

## Conformance Report Template

See [`certified/aifeels-reference-0.1.0.json`](certified/aifeels-reference-0.1.0.json) for example.

**Required fields:**
- implementation (name, version, language, repository, license)
- spec_version
- test_results (total, passed, failed)
- certification_date
- maintainer (name, email, organization)

Save as: `certified/<implementation-name>-<version>.json`

## Resources

- [Aifeels Specification](../SPEC.md)
- [Conformance Test Suite](https://github.com/aifeels-org/aifeels-conformance-suite)
- [Certification Process](../CERTIFICATION.md)

## Contact

- **Certification:** certification@aifeels.org
- **Questions:** [Discussions](https://github.com/aifeels-org/aifeels-spec/discussions)
