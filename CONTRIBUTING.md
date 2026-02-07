# Contributing to Aifeels

Thank you for your interest in contributing to the Aifeels specification!

## How to Contribute

### Reporting Issues

Use GitHub Issues for:
- **Spec ambiguities** — Unclear language that could lead to different implementations
- **Errors** — Incorrect formulas, typos, broken examples
- **Missing test vectors** — Cases that should be covered in conformance tests

**When reporting:**
1. Reference specific section (e.g., "SPEC.md Section 5.1")
2. Describe the problem clearly
3. Suggest a fix (if you have one)

### Proposing Changes

#### Small Changes (typos, clarifications, examples)
Submit a PR directly with:
- Clear commit message
- Reference to SPEC.md section being changed
- Explanation of why the change is needed

#### Large Changes (new features, breaking changes)
Submit an RFC first:
1. Copy `RFC/TEMPLATE.md`
2. Fill out all sections
3. Submit as PR to `RFC/` directory
4. Engage in community discussion

See [GOVERNANCE.md](GOVERNANCE.md) for full RFC process.

## What We're Looking For

✅ **High value:**
- Real-world use cases that expose spec gaps
- Implementation experiences (what was hard/confusing?)
- Test vectors that caught real bugs
- Clarifications based on attempted implementations

❌ **Low value:**
- Scope creep without strong justification
- Vendor-specific features
- Changes that break determinism
- "Wouldn't it be cool if..." without evidence

## Development Workflow

### For Spec Changes

1. Fork the repository
2. Create a branch: `git checkout -b fix/section-5-clarity`
3. Make changes to SPEC.md
4. Run validation (see below)
5. Commit with clear message
6. Submit PR

### For Documentation

1. Update relevant files (README, FAQ, examples)
2. Ensure links are valid
3. Check markdown rendering
4. Submit PR

## Validation Checklist

Before submitting a PR:

- [ ] No typos (run spell check)
- [ ] All section references are correct
- [ ] JSON examples validate against schemas
- [ ] No vendor mentions (grep for "Workrush", "Human-work", "Airprint")
- [ ] Markdown renders correctly
- [ ] Links work (or are marked "coming soon")

## Code of Conduct

- Be respectful and constructive
- Focus on technical merit
- Assume good faith
- No personal attacks

## Questions?

- **Spec questions:** See [docs/FAQ.md](docs/FAQ.md)
- **Process questions:** See [GOVERNANCE.md](GOVERNANCE.md)
- **Everything else:** Open a [Discussion](https://github.com/aifeels-org/aifeels-spec/discussions)

## License

By contributing, you agree that your contributions will be licensed under Apache 2.0.
