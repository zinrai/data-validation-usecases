# k8s-like-config

Kubernetes-style application configuration validation example.

This is an example of static validation for YAML files, suitable for CI pipelines.

## Validation Rules

- `name`: Lowercase alphanumeric with hyphens
- `version`: Semantic versioning (e.g., `v1.2.3`)
- `replicas`: 1-10 (optional)
- `environment`: One of `development`, `staging`, `production`
- `resources`: CPU (e.g., `100m`) and memory (e.g., `256Mi`) limits
- `ports`: Port number 1-65535, protocol TCP or UDP
- `healthCheck`: Interval and timeout in seconds format (e.g., `30s`)

## Usage

```bash
# Valid configuration
cue vet -d '#Config' schema.cue valid.yaml

# Invalid configuration (shows errors)
cue vet -d '#Config' schema.cue invalid.yaml
```

## CI Integration

```yaml
# GitHub Actions example
- name: Validate config
  run: cue vet -d '#Config' schema.cue config.yaml
```

## Files

- `schema.cue` - CUE schema definition
- `valid.yaml` - Valid configuration example
- `invalid.yaml` - Invalid configuration (for testing error output)
