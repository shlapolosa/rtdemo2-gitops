# rtdemo2 GitOps Repository

This repository contains the GitOps deployment manifests for the rtdemo2 application container.

## Structure

```
rtdemo2-gitops/
├── apps/                    # ArgoCD Applications
│   ├── app-of-apps.yaml    # Main App of Apps
│   └── environments/       # Environment-specific configs
├── oam/                     # OAM Applications and Components
│   ├── applications/        # OAM Applications (edit here)
│   ├── components/          # Generated OAM Components
│   └── workflows/           # Workflow definitions
├── manifests/               # Kubernetes manifests per service
│   ├── service-1/          # Each microservice directory
│   └── service-2/
└── .github/workflows/       # GitOps automation
```

## Deployment Flow

1. Source repository CI/CD builds and pushes images
2. Source CI/CD sends repository_dispatch to this repo
3. GitOps workflow updates manifest files with new image tags
4. ArgoCD detects changes and deploys to cluster

## ArgoCD Applications

- **App of Apps**:  - Main application managing all microservices
- **ApplicationSet**: Automatically creates ArgoCD apps for each service in 

## Adding New Services

When ApplicationClaim creates a new microservice, it automatically:
1. Creates a directory in manifests/[service-name]/
2. Generates Knative service and OAM component manifests
3. Updates the ApplicationSet to include the new service
