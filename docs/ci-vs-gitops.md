# CI vs GitOps CD

## Decision

Use Jenkins for build/test/security validation and artifact publishing. Use Argo CD for Kubernetes reconciliation.

## Why

Direct deployment from Jenkins couples application CI to cluster credentials and imperative release logic. GitOps keeps desired state versioned, provides drift detection and separates artifact production from environment reconciliation.

## Jenkins responsibilities

- compile/test
- static analysis
- container build
- vulnerability scan
- Helm validation
- artifact publish

## Argo CD responsibilities

- observe desired state in Git
- synchronize cluster resources
- prune removed resources
- self-heal drift
- expose deployment health and sync status
