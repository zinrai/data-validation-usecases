# app-config

Application configuration validation example.

## Validation Rules

- `name`: Lowercase alphanumeric with hyphens
- `port`: 1-65535
- `enabled`: Boolean
- `environment`: One of `development`, `staging`, `production`
- `replicas`: 1-10 (optional)
- `resources`: CPU and memory limits (optional)

## Usage

```bash
# Valid configuration
cue vet -d '#Config' schema.cue valid.json

# Invalid configuration (shows errors)
cue vet -d '#Config' schema.cue invalid.json
```

## Files

- `schema.cue` - CUE schema definition
- `valid.json` - Valid configuration example
- `invalid.json` - Invalid configuration (for testing error output)
