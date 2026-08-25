# CI to GitOps handoff

The modern pipeline treats Jenkins as a CI system. It builds, validates, scans and publishes an immutable artifact; cluster reconciliation remains the responsibility of Argo CD or another GitOps controller.

## Contract

```text
source commit
    |
    v
Jenkins CI
  - test
  - build
  - scan
  - publish image:<git-sha>
    |
    v
Git change updates desired image tag
    |
    v
Argo CD reconciles Kubernetes
```

## Why this boundary matters

- Jenkins does not need permanent cluster-admin credentials.
- Deployment state remains reviewable in Git.
- Rollback is a desired-state change rather than an imperative CI action.
- Argo CD can detect and heal drift independently of Jenkins availability.
- Promotion policy can be reviewed separately from application compilation.

## Production options

The image-tag update can be performed by a dedicated automation identity, an image updater, or a pull request created by CI. Whichever method is chosen should preserve auditability and avoid committing registry passwords or cluster credentials.
