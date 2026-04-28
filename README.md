# Kubernetes Homelab

Personal homelab running a GitOps-managed Kubernetes cluster with self-hosted applications,
automated dependency updates, and external access via Cloudflare tunnels.

---

## Hardware

### Kubernetes Nodes

| Host | Model | CPU | RAM |
|------|-------|-----|-----|
| ubuntu-control-plane | Dell OptiPlex 7040 | i5-6500T @ 2.50GHz | 16GB |
| ubuntu-worker-node01 | Dell OptiPlex 7040 | i5-6500T @ 2.50GHz | 16GB |
| ubuntu-worker-node02 | Dell OptiPlex 7040 | i5-6600T @ 2.70GHz | 16GB |

### NAS
- **Ugreen NAS** — 4TB RAID1

---

## Kubernetes Cluster

**Cluster name:** Careus  
**GitOps:** Flux CD v2.8.3, reconciling from `github.com/kevinmorrisnet/homelab` (`main` branch)  
**Ingress:** Traefik (internal) + Cloudflare tunnels (external)  
**Load balancer:** MetalLB — IP pool `192.168.1.201–192.168.1.254`  
**Storage:** Local storage class, 5× 2Gi PersistentVolumes on `ubuntu-worker-node01` (`/mnt/pv1`–`/mnt/pv5`)  
**Secrets:** SOPS + age encryption  
**Dependency updates:** Renovate bot (hourly CronJob, automerges lock file updates)  

---

## Applications

| App | Version | URL | Description |
|-----|---------|-----|-------------|
| Audiobookshelf | 2.34.0 | audiobooks.kevin-morris.net | Audiobook library |
| Homepage | 1.12.3 | kevinhomepage.net | Personal dashboard |
| Linkding | 1.45.0 | linkding.kevin-morris.net | Bookmark manager |
| Mealie | 3.16.0 | mealie.kevin-morris.net | Recipe manager |
| Grafana | 81.2.2 (kube-prometheus-stack) | grafana.kevin-morris.net | Cluster monitoring |

---

## Monitoring

kube-prometheus-stack (Prometheus + Grafana + Alertmanager) deployed via Helm.  
Grafana exposed at `grafana.kevin-morris.net` with TLS.

---

## Backups

All backups run nightly via Restic to the Ugreen NAS over SFTP.

| Target | What |
|--------|------|
| ubuntu-control-plane | etcd snapshot + full system |
| ubuntu-worker-node01 | full system |
| ubuntu-worker-node02 | full system |
