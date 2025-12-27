# data-validation-usecases

Use cases for validating structured data (JSON, YAML) using [CUE](https://cuelang.org/) and `cue vet`.

## Overview

This repository provides practical examples of data validation using CUE schemas.

**Two validation patterns:**

| Pattern | Data Source | Timing | Example |
|---------|-------------|--------|---------|
| Static | Files in repository | CI pipeline | Kubernetes manifests, config files |
| Dynamic | HTTP API responses | Runtime / Migration | Consul cluster state, API health checks |

## Prerequisites

- [CUE](https://cuelang.org/docs/introduction/installation/)

```bash
# Verify installation
cue version
```

## Basic Usage

```bash
cue vet -d '#Config' schema.cue data.json
cue vet -d '#Config' schema.cue data.yaml
```

- `-d '#Config'`: Specifies the CUE definition to validate against
- Exit code `0`: Valid
- Exit code `1`: Invalid (with error details)

## Use Cases

### JSON

| Use Case | Description |
|----------|-------------|
| [app-config](json/app-config/) | Application configuration validation |
| [consul-raft](json/consul-raft/) | Dynamic validation of Consul Raft API response |

### YAML

| Use Case | Description |
|----------|-------------|
| [k8s-like-config](yaml/k8s-like-config/) | Kubernetes-style resource configuration |

## License

This project is licensed under the [MIT License](./LICENSE).
