# Helm Charts Repository

This repository contains Helm charts and associated workflows for deploying applications.

## Available Charts

### squares
Frontend application chart located in `squares/`.

### squares-api
API service chart located in `squares-api/`.

## Usage

### Prerequisites

- Kubernetes cluster (1.19+)
- Helm 3.x installed
- `kubectl` configured to access your cluster

### Installing a Chart

```bash
# Install from local directory
helm install <release-name> ./squares-api

# Install with custom values
helm install <release-name> ./squares-api -f custom-values.yaml

# Add the Helm repository (after charts are released)
helm repo add maxstash https://github.com/<your-org>/charts/releases/download/index
helm repo update
helm install <release-name> maxstash/squares-api
```

### Upgrading a Release

```bash
helm upgrade <release-name> ./squares-api
```

### Uninstalling a Release

```bash
helm uninstall <release-name>
```

## CI/CD

This repository uses GitHub Actions for automated chart releases:

- **On tag push**: Charts are linted, packaged, and released with the tag
- **On pull request**: Charts are linted and tested

To create a new release:
```bash
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

## Development

### Linting Charts

```bash
helm lint ./squares
helm lint ./squares-api
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
