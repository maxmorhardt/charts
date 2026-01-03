# Helm Charts Repository

This repository contains Helm charts and associated workflows for deploying applications.

## Available Charts

### maxstash/squares-api

API service chart located in `maxstash/squares-api/`.

## Usage

### Prerequisites

- Kubernetes cluster (1.19+)
- Helm 3.x installed
- `kubectl` configured to access your cluster

### Installing a Chart

```bash
# Install from local directory
helm install <release-name> ./maxstash/squares-api

# Install with custom values
helm install <release-name> ./maxstash/squares-api -f custom-values.yaml
```

### Upgrading a Release

```bash
helm upgrade <release-name> ./maxstash/squares-api
```

### Uninstalling a Release

```bash
helm uninstall <release-name>
```

## Development

### Linting Charts

```bash
helm lint ./maxstash/squares-api
```

### Testing Template Rendering

```bash
helm template <release-name> ./maxstash/squares-api
```

### Packaging Charts

```bash
helm package ./maxstash/squares-api
```

## Chart Structure

Each chart follows the standard Helm structure:
- `Chart.yaml` - Chart metadata
- `values.yaml` - Default configuration values
- `templates/` - Kubernetes manifest templates

## License

See [LICENSE](LICENSE) for details.
