# infra-template

This repository serves as a GitHub template for infrastructure manifests designed to integrate seamlessly with the existing example GitOps process managed by ArgoCD.
It provides a standardized structure and files to help deploy services to the EKS cluster efficiently.

## Table of Contents

- [Folder Structure](#folder-structure)
- [Checklist](#checklist)
- [Integrating with GitOps process for Deployment](#Integrating-with-GitOps-process-for-Deployment)

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

## Integrating with GitOps process for Deployment

To deploy a new service to the EKS cluster using this template and integrate it with the GitOps process managed by ArgoCD, follow these steps:

### 1. Create and Customize the Infrastructure Repository

- [ ] Use this template to create an infrastructure repository for your service.
- [ ] Modify the placeholders (`template`) and configurations to suit your service's requirements (e.g., update environment variables, secrets, and deployment configurations).
- [ ] Ensure ArgoCD has access to the newly created repository so it can use it as the source (`HEAD`) for syncing.

### 2. Configure Continuous Integration (CI)

- [ ] Update GitHub Actions in your project repository to:
  - Build the service image.
  - Push the built image to the Amazon Elastic Container Registry (ECR).

### 3. Configure Secrets (if required)

- [ ] Create secrets for each environment as needed, following the naming convention:
  - Example: `example-api-dev`, `example-api-test`, `example-api-uat`.
- [ ] Update the policies of the respective `example-eks-{env}-secretsmanager` IAM roles to grant your service access to the required secrets.

### 4. Configure AWS Resource Access (if required)

- [ ] Create an AWS IAM role with the least privileges your service requires. Use a naming convention such as `example-eks-uat-myapi`.
- [ ] Ensure the ARN of the newly created IAM roles are referenced in all related `serviceaccount.yaml` files across environments to bind the role to your pods.

### 5. Configure Continuous Deployment (CD)

- [ ] Add an application manifest for your service to an `infra` GitOps repository. 
- [ ] **Verify Deployment:** Once committed, ArgoCD will automatically attempt to spin up and manage an instance of your application.


---
