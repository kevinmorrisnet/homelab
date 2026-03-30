# Kubernetes Homelab

  Personal homelab running a GitOps-managed Kubernetes cluster with self-hosted applications,
  automated dependency updates, and external access via Cloudflare tunnels.

  ---

  ## Kubernetes Cluster

  **Cluster name:** Careus
  **GitOps:** Flux CD v2.8.3, reconciling from `github.com/kevinmorrisnet/homelab` (`main` branch)
  **Worker node:** `ubuntu-worker-node01`
  **Ingress:** Traefik (internal) + Cloudflare tunnels (external)
  **Load balancer:** MetalLB — IP pool `192.168.1.201–192.168.1.254`
  **Storage:** Local storage class, 5× 2Gi PersistentVolumes on `ubuntu-worker-node01` (`/mnt/pv1`–`/mnt/pv5`)
  **Secrets:** SOPS + age encryption
  **Dependency updates:** Renovate bot (hourly CronJob, automerges lock file updates)

  ---

  ## Applications

  | App | Version | URL | Description |
  |-----|---------|-----|-------------|
  | Audiobookshelf | 2.33.1 | audiobooks.kevin-morris.net | Audiobook library |
  | Homepage | 1.11.0 | kevinhomepage.net | Personal dashboard |
  | Linkding | 1.45.0 | linkding.kevin-morris.net | Bookmark manager |
  | Mealie | 3.13.1 | mealie.kevin-morris.net | Recipe manager |
  | Grafana | (kube-prometheus-stack 81.2.2) | grafana.kevin-morris.net | Cluster monitoring |

  ---

  ## Monitoring

  kube-prometheus-stack (Prometheus + Grafana + Alertmanager) deployed via Helm.
  Grafana exposed at `grafana.kevin-morris.net` with TLS.

  ---
