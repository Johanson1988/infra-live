# Infrastructure Live (infra-live)

Kubernetes manifests for all applications and infrastructure components.

## Structure

```
infra-live/
├── apps/
│   ├── hello-gitops/          # Hello GitOps demo app
│   ├── production/            # Production apps
│   └── staging/               # Staging apps
└── shared/
    └── base/                  # Shared resources
```

## GitOps Workflow

1. Application code changes in `hello-gitops-app` repository
2. GitHub Actions builds new Docker image
3. Image pushed to GitHub Container Registry with tag
4. Update `apps/hello-gitops/deployment.yaml` with new image tag
5. Commit and push to this repository
6. ArgoCD detects change and deploys automatically

## Deployment

All applications are managed by ArgoCD. Changes to this repository trigger automatic deployments.

## Adding New Applications

1. Create directory: `apps/your-app-name/`
2. Add Kubernetes manifests (deployment, service, ingress)
3. Create ArgoCD Application
4. Push to repository

## Image Tag Updates

When updating application versions:

```bash
# Update image tag in deployment.yaml
sed -i 's|hello-gitops:main|hello-gitops:v1.1.0|' apps/hello-gitops/deployment.yaml

# Commit and push
git add apps/hello-gitops/deployment.yaml
git commit -m "Update hello-gitops to v1.1.0"
git push
```

ArgoCD will automatically deploy the new version.
