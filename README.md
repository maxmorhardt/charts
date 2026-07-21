# Helm Charts

![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)

Helm charts for deploying applications to Kubernetes.

## Overview

This repository contains Helm charts for deploying and managing applications on Kubernetes clusters. Each chart includes production-ready configurations with support for autoscaling, Gateway API routing, and pod disruption budgets.

## Setup

Required to work on charts locally:
- Helm 3.x installed
- `kubectl` configured to access your cluster (for inspecting what Argo deployed)

## Deployment

Charts are **not** installed with `helm install`. CI publishes each chart as an OCI artifact to `ghcr.io/maxmorhardt/charts`, and [Argo CD](https://github.com/maxmorhardt/k8s/blob/main/argocd/SETUP.md) deploys it from an `Application` manifest that lives in the [k8s](https://github.com/maxmorhardt/k8s) repo under `argocd/apps/`:

```yaml
source:
  repoURL: ghcr.io/maxmorhardt/charts
  chart: squares
  targetRevision: 1.0.1      # chart version — this repo's CI commits this line
  helm:
    parameters:
      - name: image.tag
        value: 1.4.2         # each app repo's release workflow commits this line
```

Both lines are pinned exactly, and both are committed by CI:

- **A chart change ships** when its release tag lands. This repo's CI publishes the OCI chart, then commits the new `targetRevision` to the k8s repo. That covers changes with no image at all — bumping `cloudflare-cidr`'s python file is a chart release, and that release is the deploy.
- **An app image ships** when that app repo's CI commits a new `image.tag`.

Nothing rolls out on its own. A version reaching the cluster is always a commit you can read, review, and `git revert`. This repo holds chart *source* only; no deployment state lives here.

To render a chart locally while working on it:

```bash
helm template <release-name> ./charts/squares-api
helm template <release-name> ./charts/squares-api -f custom-values.yaml
```

## Available Charts

### Application Charts
- **squares** / **squares-api** - Squares frontend and API
- **olympics** / **olympics-api** - Olympics frontend and API
- **maxstash** - Maxstash frontend
- **maxstash-gateway** - Gateway API resources for the `maxstash.io` gateway
- **cloudflare-cidr** / **cloudflare-ddns** - Cloudflare CronJobs

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