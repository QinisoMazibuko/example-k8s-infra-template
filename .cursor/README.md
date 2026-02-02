# Cursor AI Configuration

This directory contains rules and agents to enhance your workflow when working with this Kubernetes infrastructure template.

## How It Works

Cursor automatically applies context-aware guidance based on which files you're editing:

| Editing... | Cursor applies... |
|------------|-------------------|
| `networkpolicy.yaml`, `secret.yaml`, `serviceaccount.yaml` | Security best practices |
| `kustomization.yaml`, `base/*.yaml`, `variants/**` | Kustomize patterns |
| `envs/**/*.yaml`, `deployment.yaml`, `ingress.yaml` | GitOps/deployment guidance |
| Any `*.yaml` file | Code generation standards |

## Directory Structure

```
.cursor/rules/
├── agents/           # Context-triggered specialists
│   ├── infra-security.mdc
│   ├── kustomize-expert.mdc
│   └── gitops-reviewer.mdc
└── guidelines/       # Always-applied standards
    ├── project-overview.mdc
    └── code-generation.mdc
```

## Quick Tips

1. **Just start editing** — relevant rules apply automatically
2. **Ask questions** — Cursor understands the project structure and conventions
3. **Use `@` mentions** — invoke agents directly: `@infra-security-auditor`, `@kustomize-expert`, `@gitops-reviewer`
4. **Follow the header pattern** — all YAML files should include Purpose + Checklist comments

## Common Workflows

### Creating a new manifest
Ask Cursor to create it — the code generation guidelines ensure proper headers and formatting.

### Security review
Edit any security-related file (networkpolicy, secrets, serviceaccount) and ask Cursor to review it.

### Environment promotion
When working in `envs/`, Cursor will help validate consistency across dev → test → uat.

## Customizing Rules

- Edit files in `rules/agents/` to adjust specialist behavior
- Edit files in `rules/guidelines/` to change project standards
- Add new `.mdc` files to extend coverage
