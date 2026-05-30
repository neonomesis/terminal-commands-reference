# Docker & Kubernetes — Command Reference

Comprehensive command reference for Docker (containers) and Kubernetes (orchestration).
Covers images, containers, volumes, networks, registries, kubectl, pods, deployments, services, and more.

---

## Table of Contents

- [Docker](#docker)
  - [Images](#images)
  - [Containers](#containers)
  - [Volumes](#volumes)
  - [Networks](#networks)
  - [Registry & Distribution](#registry--distribution)
  - [Docker Compose](#docker-compose)
  - [System & Cleanup](#system--cleanup)
  - [Build (Dockerfile)](#build-dockerfile)
- [Kubernetes — kubectl](#kubernetes--kubectl)
  - [Context & Config](#context--config)
  - [Pods](#pods)
  - [Deployments](#deployments)
  - [Services & Networking](#services--networking)
  - [ConfigMaps & Secrets](#configmaps--secrets)
  - [Storage — PV & PVC](#storage--pv--pvc)
  - [Namespaces](#namespaces)
  - [Jobs & CronJobs](#jobs--cronjobs)
  - [Logs & Debugging](#logs--debugging)
  - [Resource Management](#resource-management)
  - [Rollouts & Updates](#rollouts--updates)
  - [Helm](#helm)
- [Quick Reference Tables](#quick-reference-tables)

---

## Docker

### Images

```bash
# --- Build ---
docker build -t <name>:<tag> .                      # Build image from Dockerfile in current dir
docker build -t <name>:<tag> -f Dockerfile.prod .   # Use a specific Dockerfile
docker build --no-cache -t <name> .                 # Build without layer cache
docker build --build-arg KEY=val -t <name> .        # Pass build-time variables
docker build --target <stage> -t <name> .           # Multi-stage: stop at a named stage
docker buildx build --platform linux/amd64,linux/arm64 -t <name> . --push  # Multi-arch build

# --- List & Inspect ---
docker images                                       # List all local images
docker images -a                                    # Include intermediate layers
docker image ls --filter dangling=true              # List untagged (dangling) images
docker inspect <image>                              # Full JSON metadata
docker history <image>                              # Show layer history and sizes

# --- Tag & Remove ---
docker tag <image> <new-name>:<tag>                 # Tag an image
docker rmi <image>                                  # Remove image (fails if in use)
docker rmi -f <image>                               # Force remove
docker image prune                                  # Remove all dangling images
docker image prune -a                               # Remove all unused images

# --- Save & Load ---
docker save -o image.tar <image>                    # Export image to tar archive
docker load -i image.tar                            # Import image from tar archive
docker export <container> -o container.tar          # Export container filesystem
docker import container.tar <name>:<tag>            # Create image from exported fs
```

---

### Containers

```bash
# --- Run ---
docker run <image>                                  # Run container (foreground)
docker run -d <image>                               # Run detached (background)
docker run -it <image> bash                         # Interactive terminal
docker run --name <name> <image>                    # Assign a name
docker run --rm <image>                             # Auto-remove on exit
docker run -p 8080:80 <image>                       # Map host:container port
docker run -p 127.0.0.1:8080:80 <image>             # Bind to localhost only
docker run -e KEY=value <image>                     # Set environment variable
docker run --env-file .env <image>                  # Load env vars from file
docker run -v /host/path:/container/path <image>    # Bind mount
docker run -v <vol-name>:/container/path <image>    # Named volume mount
docker run --network <net> <image>                  # Attach to network
docker run --cpus="1.5" --memory="512m" <image>     # Resource limits
docker run --restart unless-stopped <image>         # Restart policy
docker run --user 1000:1000 <image>                 # Run as specific UID:GID
docker run --read-only <image>                      # Read-only root filesystem

# --- Manage ---
docker ps                                           # List running containers
docker ps -a                                        # List all containers (incl. stopped)
docker ps --filter status=exited                    # Filter by status
docker start <container>                            # Start a stopped container
docker stop <container>                             # Graceful stop (SIGTERM → SIGKILL)
docker stop -t 5 <container>                        # Stop with 5s timeout
docker kill <container>                             # Force kill (SIGKILL)
docker restart <container>                          # Stop + start
docker pause <container>                            # Freeze processes (SIGSTOP)
docker unpause <container>                          # Resume frozen container
docker rm <container>                               # Remove stopped container
docker rm -f <container>                            # Force remove running container
docker container prune                              # Remove all stopped containers
docker rename <old> <new>                           # Rename a container

# --- Inspect & Exec ---
docker logs <container>                             # Show stdout/stderr
docker logs -f <container>                          # Follow (tail) logs
docker logs --tail 100 <container>                  # Last 100 lines
docker logs --since 10m <container>                 # Logs from last 10 minutes
docker exec -it <container> bash                    # Open interactive shell
docker exec <container> <cmd>                       # Run command in running container
docker attach <container>                           # Attach to container's main process
docker top <container>                              # Show running processes
docker stats                                        # Live resource usage (all containers)
docker stats <container>                            # Resource usage for one container
docker inspect <container>                          # Full JSON metadata
docker port <container>                             # Show port mappings
docker diff <container>                             # Show filesystem changes since start
docker cp <container>:/path/file ./local            # Copy file out of container
docker cp ./local <container>:/path/file            # Copy file into container
docker commit <container> <image>:<tag>             # Create image from container state
```

---

### Volumes

```bash
# --- Create & List ---
docker volume create <name>                         # Create a named volume
docker volume ls                                    # List all volumes
docker volume inspect <name>                        # Show volume details (mount path, etc.)
docker volume rm <name>                             # Remove volume
docker volume prune                                 # Remove all unused volumes

# --- Usage ---
docker run -v <vol>:/data <image>                   # Mount named volume
docker run -v $(pwd):/app <image>                   # Bind mount current directory
docker run --mount type=bind,src=$(pwd),dst=/app <image>   # Explicit bind mount
docker run --mount type=tmpfs,dst=/tmp <image>      # In-memory tmpfs mount
```

---

### Networks

```bash
# --- Create & List ---
docker network create <name>                        # Create bridge network
docker network create --driver overlay <name>       # Overlay network (Swarm)
docker network create --subnet 172.20.0.0/16 <name> # Custom subnet
docker network ls                                   # List networks
docker network inspect <name>                       # Show network details
docker network rm <name>                            # Remove network
docker network prune                                # Remove all unused networks

# --- Connect / Disconnect ---
docker network connect <net> <container>            # Attach running container to network
docker network disconnect <net> <container>         # Detach container from network
docker run --network <name> <image>                 # Connect at start time
docker run --network host <image>                   # Use host network (no isolation)
docker run --network none <image>                   # Completely isolated (no network)
```

---

### Registry & Distribution

```bash
# --- Login / Logout ---
docker login                                        # Login to Docker Hub
docker login registry.example.com                  # Login to private registry
docker logout                                       # Logout

# --- Push / Pull ---
docker pull <image>:<tag>                           # Pull image from registry
docker pull <image>@sha256:<digest>                 # Pull by digest (immutable)
docker push <name>:<tag>                            # Push image to registry
docker search <term>                                # Search Docker Hub

# --- Tags for private registries ---
docker tag <image> registry.example.com/project/<image>:<tag>
docker push registry.example.com/project/<image>:<tag>
```

---

### Docker Compose

```bash
# --- Basic Lifecycle ---
docker compose up                                   # Start services (foreground)
docker compose up -d                                # Start detached
docker compose up --build                           # Rebuild images before starting
docker compose up --force-recreate                  # Recreate containers even if unchanged
docker compose up <service>                         # Start only one service
docker compose down                                 # Stop and remove containers + networks
docker compose down -v                              # Also remove named volumes
docker compose down --rmi all                       # Also remove images
docker compose stop                                 # Stop without removing
docker compose start                                # Start stopped services
docker compose restart <service>                    # Restart one service

# --- Inspect ---
docker compose ps                                   # List containers
docker compose logs -f                              # Follow all logs
docker compose logs -f <service>                    # Follow one service
docker compose top                                  # Show running processes
docker compose config                               # Print merged resolved config

# --- Exec & Run ---
docker compose exec <service> bash                  # Shell into running service
docker compose run --rm <service> <cmd>             # One-off command (new container)

# --- Build & Images ---
docker compose build                                # Build all services
docker compose build <service>                      # Build one service
docker compose pull                                 # Pull all service images

# --- Scale ---
docker compose up -d --scale <service>=3            # Run 3 replicas of a service
```

---

### System & Cleanup

```bash
docker system df                                    # Show disk usage (images, containers, volumes)
docker system df -v                                 # Verbose breakdown
docker system prune                                 # Remove stopped containers, unused networks, dangling images
docker system prune -a                              # Also remove unused images
docker system prune -a --volumes                    # Also remove unused volumes
docker system info                                  # Docker daemon info
docker version                                      # Client & server version
docker events                                       # Real-time event stream from daemon
```

---

### Build (Dockerfile)

```dockerfile
# Common Dockerfile instructions
FROM ubuntu:22.04                    # Base image
FROM node:20-alpine AS builder       # Named stage for multi-stage builds

WORKDIR /app                         # Set working directory (creates if missing)

COPY package*.json ./                # Copy files from build context
COPY --from=builder /app/dist ./dist # Copy from another stage

RUN apt-get update && apt-get install -y curl   # Run commands (each RUN = one layer)
RUN --mount=type=cache,target=/root/.cache ...  # BuildKit layer cache mount

ENV NODE_ENV=production              # Set environment variable (baked into image)
ARG VERSION=1.0                      # Build-time variable (not in final image)

EXPOSE 3000                          # Document the port (informational only)

VOLUME ["/data"]                     # Declare mount point

USER node                            # Switch to non-root user

ENTRYPOINT ["node"]                  # Fixed executable (cannot be overridden by docker run args)
CMD ["server.js"]                    # Default args (overridden by docker run <args>)

HEALTHCHECK --interval=30s --timeout=5s CMD curl -f http://localhost/ || exit 1
```

---

## Kubernetes — kubectl

### Context & Config

```bash
# --- Contexts ---
kubectl config get-contexts                         # List all contexts
kubectl config current-context                      # Show active context
kubectl config use-context <name>                   # Switch context
kubectl config delete-context <name>                # Remove a context
kubectl config rename-context <old> <new>           # Rename context

# --- Clusters & Credentials ---
kubectl config view                                 # Show full kubeconfig
kubectl config view --minify                        # Show current context only
kubectl config set-cluster <name> --server=<url>    # Add/update cluster
kubectl config set-credentials <user> --token=<t>  # Set credentials

# --- Shorthand ---
kubectx                                             # External tool: interactive context switcher
kubens                                              # External tool: interactive namespace switcher
```

---

### Pods

```bash
# --- List & Inspect ---
kubectl get pods                                    # List pods in current namespace
kubectl get pods -n <namespace>                     # Specific namespace
kubectl get pods -A                                 # All namespaces
kubectl get pods -o wide                            # Include node, IP
kubectl get pods -o yaml                            # Full YAML spec
kubectl get pod <name> -o jsonpath='{.status.phase}' # Extract specific field
kubectl describe pod <name>                         # Detailed status, events, conditions
kubectl get pod <name> --watch                      # Watch status changes live

# --- Run & Delete ---
kubectl run <name> --image=<image>                  # Create a pod imperatively
kubectl run -it --rm debug --image=busybox -- sh    # Ephemeral debug pod (auto-deleted)
kubectl delete pod <name>                           # Delete pod (restarted if in Deployment)
kubectl delete pod <name> --grace-period=0          # Force immediate deletion

# --- Shell & Copy ---
kubectl exec -it <pod> -- bash                      # Interactive shell
kubectl exec -it <pod> -c <container> -- bash       # Shell into specific container
kubectl exec <pod> -- <cmd>                         # Run command in pod
kubectl cp <pod>:/remote/path ./local               # Copy from pod
kubectl cp ./local <pod>:/remote/path               # Copy to pod

# --- Logs ---
kubectl logs <pod>                                  # Pod logs
kubectl logs <pod> -c <container>                   # Multi-container pod
kubectl logs -f <pod>                               # Follow (stream)
kubectl logs --tail=100 <pod>                       # Last N lines
kubectl logs --since=1h <pod>                       # Logs from last hour
kubectl logs -l app=myapp                           # Logs from pods matching label
kubectl logs <pod> --previous                       # Logs from last crashed container
```

---

### Deployments

```bash
# --- Create & Apply ---
kubectl create deployment <name> --image=<image>    # Imperative create
kubectl apply -f deployment.yaml                    # Declarative apply (create or update)
kubectl apply -f ./k8s/                             # Apply all manifests in directory
kubectl apply -k ./overlays/prod                    # Apply Kustomize overlay

# --- Inspect ---
kubectl get deployments                             # List deployments
kubectl describe deployment <name>                  # Events, replicas, strategy
kubectl get deployment <name> -o yaml               # Full YAML

# --- Scale ---
kubectl scale deployment <name> --replicas=3        # Scale manually
kubectl autoscale deployment <name> --min=2 --max=10 --cpu-percent=60  # HPA

# --- Update & Delete ---
kubectl set image deployment/<name> <container>=<image>:<tag>  # Update image
kubectl delete deployment <name>                    # Delete deployment
kubectl delete -f deployment.yaml                   # Delete from manifest

# --- ReplicaSets ---
kubectl get replicasets                             # List replica sets
kubectl describe rs <name>                          # Inspect a replica set
```

---

### Services & Networking

```bash
# --- Create ---
kubectl expose deployment <name> --port=80 --target-port=3000 --type=ClusterIP
kubectl expose deployment <name> --port=80 --type=NodePort
kubectl expose deployment <name> --port=80 --type=LoadBalancer
kubectl apply -f service.yaml

# --- Inspect ---
kubectl get services                                # List all services (svc)
kubectl get svc -o wide                             # Include endpoints, selector
kubectl describe svc <name>                         # Detailed info + endpoints
kubectl get endpoints <name>                        # Pod IPs behind service

# --- Port Forward (local testing) ---
kubectl port-forward svc/<name> 8080:80             # Forward local 8080 → service 80
kubectl port-forward pod/<name> 8080:3000           # Forward to a specific pod
kubectl port-forward deployment/<name> 8080:80      # Forward to a deployment

# --- Ingress ---
kubectl get ingress                                 # List Ingress resources
kubectl describe ingress <name>                     # Show rules, backend services
kubectl apply -f ingress.yaml
```

---

### ConfigMaps & Secrets

```bash
# --- ConfigMaps ---
kubectl create configmap <name> --from-literal=KEY=val
kubectl create configmap <name> --from-file=config.properties
kubectl create configmap <name> --from-env-file=.env
kubectl get configmap <name> -o yaml                # View contents
kubectl edit configmap <name>                       # Edit in-place
kubectl delete configmap <name>

# --- Secrets ---
kubectl create secret generic <name> --from-literal=password=s3cr3t
kubectl create secret generic <name> --from-file=tls.key --from-file=tls.crt
kubectl create secret tls <name> --cert=cert.pem --key=key.pem   # TLS secret
kubectl create secret docker-registry regcred \
  --docker-server=<registry> --docker-username=<user> --docker-password=<pass>
kubectl get secret <name> -o yaml                   # Base64-encoded values
kubectl get secret <name> -o jsonpath='{.data.password}' | base64 -d  # Decode
kubectl delete secret <name>
```

---

### Storage — PV & PVC

```bash
# --- PersistentVolumes ---
kubectl get pv                                      # List cluster-wide PVs
kubectl describe pv <name>                          # Capacity, access modes, reclaim policy
kubectl delete pv <name>

# --- PersistentVolumeClaims ---
kubectl get pvc                                     # List PVCs in namespace
kubectl get pvc -n <namespace>
kubectl describe pvc <name>                         # Bound PV, capacity, access mode
kubectl delete pvc <name>

# --- StorageClasses ---
kubectl get storageclass                            # List available storage classes
kubectl get sc                                      # Short alias
kubectl describe sc <name>                          # Provisioner, reclaim policy
```

---

### Namespaces

```bash
kubectl get namespaces                              # List all namespaces (ns)
kubectl create namespace <name>                     # Create namespace
kubectl delete namespace <name>                     # Delete namespace + all its resources
kubectl config set-context --current --namespace=<ns>  # Set default namespace for context

# Use -n <namespace> with any kubectl command to target a specific namespace
kubectl get pods -n kube-system                     # System pods
kubectl get all -n <namespace>                      # All resources in namespace
```

---

### Jobs & CronJobs

```bash
# --- Jobs ---
kubectl create job <name> --image=<image>           # Run a one-off job
kubectl get jobs                                    # List jobs
kubectl describe job <name>                         # Parallelism, completions, status
kubectl delete job <name>

# --- CronJobs ---
kubectl create cronjob <name> --image=<image> --schedule="*/5 * * * *" -- <cmd>
kubectl get cronjobs                                # List cron jobs (cj)
kubectl describe cronjob <name>                     # Schedule, last run, active jobs
kubectl delete cronjob <name>

# --- Trigger manually ---
kubectl create job --from=cronjob/<name> <manual-job-name>   # Run a cron job now
```

---

### Logs & Debugging

```bash
# --- Events ---
kubectl get events                                  # Cluster events (sorted by time)
kubectl get events --sort-by='.lastTimestamp'       # Explicit sort
kubectl get events -n <namespace>
kubectl describe pod <name>                         # Events section at bottom

# --- Debugging pods ---
kubectl run debug --rm -it --image=nicolaka/netshoot -- bash   # Full network debug toolbox
kubectl debug -it <pod> --image=busybox --copy-to=debug-pod    # Non-intrusive debug copy
kubectl get pod <name> -o yaml | grep -A5 "containerStatuses"  # Check container state

# --- Node issues ---
kubectl get nodes                                   # List nodes + status
kubectl get nodes -o wide                           # Include OS, kubelet version, IPs
kubectl describe node <name>                        # Conditions, capacity, allocated resources
kubectl cordon <node>                               # Mark node unschedulable
kubectl uncordon <node>                             # Re-enable scheduling
kubectl drain <node> --ignore-daemonsets            # Evict all pods (for maintenance)
kubectl top nodes                                   # CPU/memory usage per node (needs metrics-server)
kubectl top pods                                    # CPU/memory usage per pod
```

---

### Resource Management

```bash
# --- Apply & Diff ---
kubectl apply -f <file|dir>                         # Create or update resources
kubectl diff -f <file>                              # Show what would change before applying
kubectl apply --dry-run=client -f <file>            # Validate without touching cluster
kubectl apply --dry-run=server -f <file>            # Server-side dry run (more accurate)

# --- Edit & Patch ---
kubectl edit <resource> <name>                      # Open live resource in $EDITOR
kubectl patch deployment <name> -p '{"spec":{"replicas":3}}'   # JSON patch
kubectl patch deployment <name> --type=merge -p '...'          # Merge patch

# --- Labels & Annotations ---
kubectl label pod <name> env=prod                   # Add/update label
kubectl label pod <name> env-                       # Remove label
kubectl annotate pod <name> note="text"             # Add annotation
kubectl get pods -l app=myapp,env=prod              # Select by label

# --- Explain (built-in docs) ---
kubectl explain deployment                          # Field reference for resource type
kubectl explain deployment.spec.strategy            # Nested field docs
kubectl api-resources                               # List all resource types + short names
kubectl api-versions                                # List all API versions
```

---

### Rollouts & Updates

```bash
# --- Status ---
kubectl rollout status deployment/<name>            # Wait until rollout completes
kubectl rollout history deployment/<name>           # Show revision history
kubectl rollout history deployment/<name> --revision=2  # Details for a revision

# --- Undo ---
kubectl rollout undo deployment/<name>              # Roll back to previous revision
kubectl rollout undo deployment/<name> --to-revision=2  # Roll back to specific revision

# --- Pause / Resume ---
kubectl rollout pause deployment/<name>             # Pause mid-rollout (canary-style)
kubectl rollout resume deployment/<name>            # Resume paused rollout

# --- Restart ---
kubectl rollout restart deployment/<name>           # Rolling restart (zero-downtime)
```

---

### Helm

```bash
# --- Repos ---
helm repo add <name> <url>                          # Add chart repository
helm repo update                                    # Refresh repo index
helm repo list                                      # List added repos
helm repo remove <name>                             # Remove repo
helm search repo <keyword>                          # Search added repos
helm search hub <keyword>                           # Search Artifact Hub

# --- Install & Upgrade ---
helm install <release> <chart>                      # Install chart with generated name
helm install <release> <chart> -n <namespace>       # Into specific namespace
helm install <release> <chart> --create-namespace   # Create namespace if missing
helm install <release> <chart> -f values.yaml       # Custom values file
helm install <release> <chart> --set key=val        # Override single value
helm install <release> <chart> --dry-run            # Preview manifests
helm upgrade <release> <chart> -f values.yaml       # Upgrade existing release
helm upgrade --install <release> <chart>            # Install if not exists, else upgrade

# --- Inspect ---
helm list                                           # List installed releases
helm list -A                                        # All namespaces
helm status <release>                               # Release status + notes
helm get values <release>                           # Values used for release
helm get manifest <release>                         # Rendered manifests
helm history <release>                              # Revision history

# --- Rollback & Uninstall ---
helm rollback <release> <revision>                  # Roll back to a revision
helm uninstall <release>                            # Remove release
helm uninstall <release> --keep-history             # Remove but keep history

# --- Package & Lint ---
helm lint ./mychart                                 # Validate chart
helm template <release> ./mychart                  # Render templates locally
helm package ./mychart                              # Package into .tgz
```

---

## Quick Reference Tables

### Docker Run — Common Flags

| Flag | Purpose |
|------|---------|
| `-d` | Detached (background) |
| `-it` | Interactive + TTY |
| `--rm` | Auto-remove on exit |
| `-p host:container` | Port mapping |
| `-e KEY=val` | Environment variable |
| `-v src:dst` | Volume / bind mount |
| `--name` | Container name |
| `--network` | Attach to network |
| `--restart` | Restart policy (`no`, `always`, `unless-stopped`, `on-failure`) |
| `--cpus` / `--memory` | Resource limits |
| `--user` | Run as UID:GID |
| `--read-only` | Immutable root fs |

---

### kubectl — Resource Short Names

| Resource | Short Name |
|----------|-----------|
| `pods` | `po` |
| `services` | `svc` |
| `deployments` | `deploy` |
| `replicasets` | `rs` |
| `namespaces` | `ns` |
| `nodes` | `no` |
| `configmaps` | `cm` |
| `persistentvolumeclaims` | `pvc` |
| `persistentvolumes` | `pv` |
| `cronjobs` | `cj` |
| `horizontalpodautoscalers` | `hpa` |
| `ingresses` | `ing` |
| `storageclasses` | `sc` |
| `serviceaccounts` | `sa` |

---

### Service Types

| Type | Accessibility |
|------|--------------|
| `ClusterIP` | Internal only (cluster-local DNS) |
| `NodePort` | Exposed on every node's IP at a static port (30000–32767) |
| `LoadBalancer` | External load balancer (cloud provider) |
| `ExternalName` | DNS alias to external hostname |

---

### Container Restart Policies

| Policy | Behavior |
|--------|---------|
| `no` | Never restart (default) |
| `always` | Always restart, including on daemon start |
| `unless-stopped` | Restart always, except when manually stopped |
| `on-failure[:N]` | Restart only on non-zero exit, up to N times |
