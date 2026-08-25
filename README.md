# Jenkins CI/CD to Kubernetes — Portfolio Modernization

This repository contains a historical Jenkins/Kubernetes pipeline example. The original pipeline is preserved for reference; the portfolio extension adds a modern CI-oriented Jenkinsfile and explains how Jenkins fits alongside GitOps delivery.

## What the original project demonstrates

- application build and local tests
- Docker image packaging
- Helm packaging
- multi-environment Kubernetes deployment
- smoke testing

## Modern portfolio direction

For current platform engineering, CI and CD responsibilities are separated:

```text
Jenkins CI
  checkout
    -> tests
    -> Docker build
    -> image scan
    -> Helm lint/template
    -> publish immutable artifact

GitOps CD
  Git change
    -> Argo CD reconciliation
    -> Kubernetes
```

The historical `Jenkinsfile` performs direct cluster deployment and uses old Helm 2-era commands. It is intentionally retained as legacy reference. `Jenkinsfile.modern` demonstrates the preferred CI structure without embedding Kubernetes deployment credentials in the application pipeline.

## Security improvements represented

- Jenkins credentials binding instead of plaintext credentials
- immutable image tag derived from Git commit
- no direct production deployment stage in CI
- container vulnerability scanning hook
- Helm lint/template validation before publishing
- explicit cleanup in `post` blocks

## Related project

See `Evgenz-mr/gitops-lab` for the Argo CD / Helm / Kubernetes delivery side with NGINX, Python and Java microservices.

## Attribution

The original example predates this portfolio extension and is preserved as historical/reference material. The modernization files and documentation describe the portfolio-specific design direction rather than claiming authorship of the original upstream example.
