# Aifeels Examples

This directory contains example JSON data demonstrating Aifeels concepts.

## Files

### `state-initialization.json`
Shows the default initial state (all zeros, stable, full confidence)

### `event-sequence.json`
Demonstrates how state evolves through a sequence of events

### `action-selection.json`
Shows action selection logic with different emotional states

## Usage

These examples are **non-normative** (not part of the spec) but illustrate correct usage.

**Validation:**
```bash
# Validate state examples
jsonschema -i state-initialization.json ../schemas/state.schema.json

# Validate event examples
jsonschema -i event-sequence.json ../schemas/event.schema.json
```

**In tests:**
Use these examples as test fixtures for your implementation.

## Contributing Examples

Have a useful example? Submit a PR with:
- Clear description
- Validation against schemas
- Explanation of what it demonstrates
