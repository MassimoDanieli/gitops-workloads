# GitOps Workloads Repo

Workloads deployed by Argo CD.

| Path | What |
|---|---|
| `argocd/projects/default-project.yaml` | `workloads` AppProject: only this repo, only `circle-api-*` namespaces |
| `argocd/apps/dev/circle-api.yaml` | `circle-api-dev` Application, auto-sync, Argo CD Image Updater writes the newest `sha-…` tag back to `values-dev.yaml` |
| `charts/circle-api/` | Helm chart for [circle-api](https://github.com/MassimoDanieli/circle-api) |

The chart exposes the app (uvicorn on port 8000 in the container) through a
Service on port 8080, with readiness/liveness probes on `/healthz`, resource
requests/limits and a non-root, no-privilege security context.

Every PR and push to `main` runs `helm lint` (with `values.schema.json`) and
validates the rendered manifests with kubeconform.
