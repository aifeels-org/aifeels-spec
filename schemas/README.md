# Aifeels JSON Schemas

This directory contains JSON schemas for validating Aifeels data structures.

## Files

### `state.schema.json`
Validates emotional state objects (SPEC.md Section 3.4.1)

**Usage:**
```bash
# Validate a state file
jsonschema -i state-example.json state.schema.json
```

### `event.schema.json`
Validates event objects (SPEC.md Section 4)

**Usage:**
```bash
jsonschema -i event-example.json event.schema.json
```

## Schema URLs

Schemas are hosted at:
- `https://aifeels.org/schemas/state/v0.1.0`
- `https://aifeels.org/schemas/event/v0.1.0`

## Validation Tools

**Command line:**
```bash
pip install jsonschema
jsonschema -i yourfile.json state.schema.json
```

**In code (Python):**
```python
import json
import jsonschema

with open('state.schema.json') as f:
    schema = json.load(f)

with open('yourdata.json') as f:
    data = json.load(f)

jsonschema.validate(instance=data, schema=schema)
```

**In code (JavaScript):**
```javascript
const Ajv = require('ajv');
const ajv = new Ajv();

const schema = require('./state.schema.json');
const data = require('./yourdata.json');

const valid = ajv.validate(schema, data);
if (!valid) console.log(ajv.errors);
```

## Versioning

Schemas are versioned with the specification:
- `v0.1.0` - Initial release
- Future versions will have new schema files
