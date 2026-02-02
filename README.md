# infra-template

This repository serves as a GitHub template for infrastructure manifests designed to integrate seamlessly with the existing example GitOps process managed by ArgoCD.
It provides a standardized structure and files to help deploy services to an EKS cluster efficiently.

## Table of Contents

- [Folder Structure](#folder-structure)
- [Checklist](#checklist)

---

## Folder Structure

```
└── 📁infra-template
     └── 📁base
        └── configmap.yaml
        └── deployment.yaml
        └── external-secrets.yaml
        └── ingress.yaml
        └── keda.yaml
        └── kustomization.yaml
        └── networkpolicy.yaml
        └── pdb.yaml
        └── post-sync-tests.yaml
        └── secret.yaml
        └── service.yaml
    └── 📁envs
        └── 📁dev
            └── 📁jobs
                └── cronjob.yaml
                └── dbupdatejob.yaml
            └── kustomization.yaml
            └── serviceaccount.yaml
        └── 📁test
            └── configmap.yaml
            └── external-secrets-keys.yaml
            └── kustomization.yaml
            └── serviceaccount.yaml
        └── 📁uat
            └── configmap.yaml
            └── external-secrets-keys.yaml
            └── kustomization.yaml
            └── serviceaccount.yaml
    └── 📁variants
        └── 📁dev
            └── configmap.yaml
            └── kustomization.yaml
        └── 📁test
            └── configmap.yaml
            └── kustomization.yaml
        └── 📁uat
            └── configmap.yaml
            └── kustomization.yaml
    └── .gitignore
    └── README.md
```

### Key Folders:

- **base**: Contains environment-agnostic configuration files such as `deployment.yaml`, `ingress.yaml`, and `networkpolicy.yaml`.
- **envs**: Contains environment-specific configurations (e.g., `dev`, `test`, `uat`). Each environment can have its own `kustomization.yaml` and overrides.
- **variants**: Contains additional configurations for specific environments, such as custom `ServiceAccount` files.

---

## Checklist

### General

- [ ] Replace `template` with the service name in all files.
- [ ] Update the namespace in `kustomization.yaml` if necessary.

### Environment-Specific

- [ ] Adjust environment variables in `configmap.yaml` and `external-secrets-keys.yaml`.
- [ ] Update image tags in `kustomization.yaml`.

### Deployment

- [ ] Set appropriate resource requests and limits in `deployment.yaml`.
- [ ] Update `livenessProbe` and `readinessProbe` paths if needed.

### Networking

- [ ] Configure `ingress.yaml` for external access if applicable.
- [ ] Ensure `networkpolicy.yaml` reflects the required ingress and egress rules.

### Authentication

- [ ] Update `ServiceAccount` in `envs` with the appropriate IAM role.
- [ ] Add or remove sensitive environment variables in `secret.yaml`.

### Clean up

- [ ] Each file in this repo has a checklist to ensure all config is removed or ammended as needed
- [ ] Ensure you Delete any files or configurations that are not relevant for your service.

---
---
