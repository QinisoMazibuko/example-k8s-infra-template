## Summary
<!-- Briefly describe what this PR does and why -->

## Changes
<!-- List the key changes made -->
- 

## Checklist

### Code Quality
- [ ] I have reviewed all changes in this PR
- [ ] Manifests follow project conventions (header comments, checklists)
- [ ] `template` placeholders updated or intentionally preserved
- [ ] Changes tested locally with `kustomize build envs/<env>`

### Security
- [ ] Security context is properly configured (runAsNonRoot, drop capabilities)
- [ ] No secrets or credentials hardcoded
- [ ] NetworkPolicy updated if new ingress/egress required

### Documentation
- [ ] Header comments explain the purpose of new/modified resources
- [ ] Checklist items are actionable and complete
- [ ] README updated if structural changes made

## AI Assistance Disclosure
<!-- Transparency about AI tool usage -->
- [ ] No AI tools used
- [ ] AI-assisted — all suggestions reviewed and validated by me

## Environment Impact
<!-- Which environments are affected? -->
- [ ] dev only
- [ ] dev + test
- [ ] All environments (dev/test/uat)

## Testing
<!-- How were these changes validated? -->
```bash
# Example validation commands run:
kustomize build envs/dev
kustomize build envs/test
kustomize build envs/uat
```

## Related Issues
<!-- Link any related issues: Fixes #123, Relates to #456 -->
