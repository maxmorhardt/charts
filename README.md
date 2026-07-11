# Helm Charts

![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)

Helm charts for deploying applications to Kubernetes.

## Overview

This repository contains Helm charts for deploying and managing applications on Kubernetes clusters. Each chart includes production-ready configurations with support for autoscaling, Gateway API routing, and pod disruption budgets.

## Setup

Required for deployment:
- Kubernetes cluster (1.19+)
- Helm 3.x installed
- `kubectl` configured to access your cluster

## Usage

To install a chart from this repository:

```bash
# Install from local directory
helm install <release-name> ./squares-api

# Install with custom values
helm install <release-name> ./squares-api -f custom-values.yaml

# Upgrade an existing release
helm upgrade <release-name> ./squares-api
```

## Available Charts

### Application Charts
- **squares** - Frontend application chart
- **squares-api** - API service chart

Each chart includes:
- Deployment with configurable replicas
- Service configuration
- Horizontal Pod Autoscaler (HPA)
- Gateway API (HTTPRoute) support
- Pod Disruption Budget (PDB)
- Prometheus Rules
- Service Monitor

## License
Helm charts in this repo are licensed under Apache 2.0.
However, some Docker images deployed by these charts are licensed under
PolyForm Noncommercial 1.0.0 and may not be used for commercial purposes.