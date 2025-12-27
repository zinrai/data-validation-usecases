# consul-raft

Dynamic validation of Consul Raft configuration API response.

This is an example of validating HTTP API responses at runtime, useful for system migrations and health checks.

## Validation Rules

- At least one server in the cluster
- Exactly one leader (`Leader: true`)
- All servers have identical `LastIndex` values (cluster consistency)

## Prerequisites

- [Task](https://taskfile.dev/) - Task runner
- [curl](https://curl.se/) - HTTP client
- [jq](https://stedolan.github.io/jq/) - JSON processor
- [CUE](https://cuelang.org/) - Validation

Alternatives:
- Task runner: Make, just, shell scripts
- HTTP client: wget, HTTPie

## Usage

Start test Consul cluster:

```bash
docker compose up -d
```

Run validation with Task:

```bash
# Fetch and validate (default task)
task

# Fetch only
task fetch

# Validate (runs fetch automatically)
task validate

# Clean output directory
task clean
```

Clean up:

```bash
docker compose down -v
```

## Manual Validation

```bash
# Fetch and validate
curl -s localhost:8500/v1/operator/raft/configuration | \
  jq '.' > output.json
cue vet -d '#Config' schema.cue output.json
```

## Files

- `schema.cue` - CUE schema with validation rules
- `Taskfile.yml` - Workflow definition
- `docker-compose.yml` - 5-node Consul cluster for testing
- `example/raft-configuration.json` - Sample API response
