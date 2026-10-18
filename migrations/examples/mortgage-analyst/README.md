# Reference manifests: Mortgage Analyst

Kustomize layout for the topology in [mortgage-analyst.md](../../apps/mortgage-analyst.md). One base, one overlay per cloud. Argo CD points at an overlay.

```
base/                 Deployment, Service, HTTPRoute, HPA, PDB, migration Job, ingestion CronJob, ExternalSecret
overlays/prod-aws/    Gateway class, secret store and service account for EKS
overlays/prod-azure/  Gateway class, secret store and workload identity for AKS
```

Render without applying:

```bash
kubectl kustomize overlays/prod-aws
kubectl kustomize overlays/prod-azure
```

## Code changes these manifests assume

The image is the one built by the repository's `Dockerfile`. Two small changes are needed in the app before the Job and the CronJob work as written:

1. **A switch to disable scheduling**: `@ConditionalOnProperty(name = "mortgagearb.scheduling.enabled", matchIfMissing = true)` on `SchedulingConfiguration`. The web pods and the Jobs set it to `false`, so `@Scheduled` methods never run inside a replica.
2. **A run-once entry point**: an `ApplicationRunner` active under `mortgagearb.run-once=<job>` that executes one job (for example `euribor-ingestion`) and exits. With `SPRING_MAIN_WEB_APPLICATION_TYPE=none` the process ends when the runner returns, and the Kubernetes Job records success or failure.

The migration Job needs neither: with no web server and scheduling disabled, Spring Boot starts, Liquibase applies the changelog, and the process exits.
