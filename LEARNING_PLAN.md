# GitOps & Kubernetes Learning Plan

## Overview

This document tracks my learning journey with GitOps, Kubernetes, Helm, and ArgoCD.

---

## ✅ Completed Topics

### Docker & Multi-Architecture Builds
- [x] Building Docker images
- [x] Multi-arch builds with `docker buildx` (linux/amd64, linux/arm64)
- [x] QEMU emulation for cross-platform builds
- [x] Docker Hub rate limits and authentication
- [x] Using `imagePullSecrets` in Kubernetes

### GitOps Fundamentals
- [x] GitOps flow: Code → Image → Manifest → ArgoCD → Cluster
- [x] Separation of application code and configuration repos
- [x] Automated deployments triggered by git commits

### Kubernetes Basics
- [x] Deployments and ReplicaSets
- [x] Services (NodePort)
- [x] Namespaces for environment separation
- [x] Pod lifecycle and states

### Kubernetes Debugging
- [x] `kubectl get pods` - List pods and their status
- [x] `kubectl describe pod` - Detailed pod info and events
- [x] `kubectl logs` - View container logs
- [x] `kubectl get events` - Cluster events
- [x] Common errors: `ImagePullBackOff`, `ErrImagePull`, `CrashLoopBackOff`

### Helm
- [x] Helm concepts: Charts, Templates, Values, Releases
- [x] Chart structure: `Chart.yaml`, `values.yaml`, `templates/`
- [x] Templating with `{{ .Values.x }}`
- [x] Default values vs environment-specific overrides
- [x] Deploying with `helm upgrade --install`
- [x] Dry-run with `helm template`
- [x] Created Helm chart for UI
- [x] Created Helm chart for API

### ArgoCD
- [x] ArgoCD architecture (repo-server, application-controller, server)
- [x] Application CRD configuration
- [x] Sync policies (automated, selfHeal, prune)
- [x] ArgoCD with Helm charts
- [x] Debugging ArgoCD sync issues
- [x] Force sync and cache clearing
- [x] Separate ArgoCD apps for UI and API

### CI/CD with GitHub Actions
- [x] Building and pushing Docker images
- [x] Updating Kubernetes manifests with `sed`
- [x] Separate workflows for build vs promote
- [x] Environment-specific deployments (dev auto-deploy, staging/prod manual)

---

## ✅ Recently Completed

- [x] Create Helm chart for API (same pattern as UI)
- [x] Separate ArgoCD applications for UI and API
- [x] Delete old manifest folders (`development/`, `staging/`, `production/`)
- [x] Clean project structure with Helm charts
- [x] Add `imagePullSecrets` to Helm templates (avoid Docker rate limits)
- [x] Update CI/CD to use `yq` for Helm values updates
- [x] Ingress & Networking
- [x] ConfigMaps - Environment-specific configuration

---

## 🔄 In Progress

(Pick your next topic!)

---

## 📚 Next Topics to Learn

### Level 1: Essential Kubernetes Features

#### ~~Ingress & Networking~~ ✅
- [x] Ingress controllers (nginx-ingress)
- [x] Ingress resources and routing rules
- [x] Host-based and path-based routing
- [ ] TLS/SSL termination (optional - requires cert-manager)
- [x] Local development with `/etc/hosts`

#### Configuration Management
- [x] ConfigMaps - Non-sensitive configuration
- [ ] Secrets - Sensitive data (passwords, API keys)
- [x] Environment variables from ConfigMaps/Secrets
- [ ] Mounting as files vs environment variables

#### Health & Reliability
- [ ] Liveness probes - Is the container alive?
- [ ] Readiness probes - Is the container ready for traffic?
- [ ] Startup probes - For slow-starting containers
- [ ] Resource requests and limits (CPU/memory)
- [ ] Quality of Service (QoS) classes

### Level 2: Scaling & Advanced Deployments

#### Auto-Scaling
- [ ] Horizontal Pod Autoscaler (HPA)
- [ ] Scaling based on CPU/memory
- [ ] Custom metrics scaling
- [ ] Vertical Pod Autoscaler (VPA)

#### Deployment Strategies
- [ ] Rolling updates (default)
- [ ] Blue/Green deployments
- [ ] Canary deployments
- [ ] Rollbacks with `kubectl rollout`

#### Storage
- [ ] Persistent Volumes (PV)
- [ ] Persistent Volume Claims (PVC)
- [ ] Storage Classes
- [ ] StatefulSets for stateful applications

### Level 3: Production Readiness

#### Monitoring & Observability
- [ ] Prometheus - Metrics collection
- [ ] Grafana - Dashboards and visualization
- [ ] Alertmanager - Alerting rules
- [ ] Application metrics instrumentation
- [ ] Service mesh basics (Istio/Linkerd)

#### Centralized Logging
- [ ] Logging architecture in Kubernetes
- [ ] ELK Stack (Elasticsearch, Logstash, Kibana)
- [ ] Loki + Grafana alternative
- [ ] Log aggregation patterns

#### Secrets Management
- [ ] Sealed Secrets
- [ ] External Secrets Operator
- [ ] HashiCorp Vault integration
- [ ] Secret rotation strategies

#### Security
- [ ] RBAC (Role-Based Access Control)
- [ ] Service Accounts
- [ ] Network Policies
- [ ] Pod Security Standards
- [ ] Security contexts

### Level 4: Advanced Topics

#### Multi-Cluster & GitOps at Scale
- [ ] ArgoCD ApplicationSets
- [ ] Multi-cluster deployments
- [ ] Cluster bootstrapping
- [ ] GitOps repository structures at scale

#### Kubernetes Internals
- [ ] How kube-scheduler works
- [ ] etcd and cluster state
- [ ] Controller pattern
- [ ] Custom Resource Definitions (CRDs)
- [ ] Operators

#### CI/CD Advanced
- [ ] GitOps with Flux CD (alternative to ArgoCD)
- [ ] Progressive delivery with Argo Rollouts
- [ ] Integration testing in pipelines
- [ ] Security scanning (container images, IaC)

---

## 📁 Current Project Structure

```
gitops-k8-config/
├── apps/                              # ArgoCD Application definitions
│   ├── api-development.yaml           # API app for dev
│   ├── api-staging.yaml               # API app for staging
│   ├── api-production.yaml            # API app for prod
│   ├── ui-development.yaml            # UI app for dev
│   ├── ui-staging.yaml                # UI app for staging
│   └── ui-production.yaml             # UI app for prod
├── charts/                            # Helm charts
│   ├── api/                           # API Helm chart
│   │   ├── Chart.yaml
│   │   ├── values.yaml                # Default values
│   │   ├── templates/
│   │   │   ├── deployment.yaml
│   │   │   └── service.yaml
│   │   └── environments/
│   │       ├── development/values.yaml
│   │       ├── staging/values.yaml
│   │       └── production/values.yaml
│   └── ui/                            # UI Helm chart
│       ├── Chart.yaml
│       ├── values.yaml                # Default values
│       ├── templates/
│       │   ├── deployment.yaml
│       │   └── service.yaml
│       └── environments/
│           ├── development/values.yaml
│           ├── staging/values.yaml
│           └── production/values.yaml
└── LEARNING_PLAN.md                   # This file
```

---

## 🛠️ Useful Commands Reference

### Kubectl Basics
```bash
kubectl get pods -n <namespace>              # List pods
kubectl describe pod <name> -n <namespace>   # Pod details
kubectl logs <pod-name> -n <namespace>       # View logs
kubectl logs -f <pod-name>                   # Follow logs
kubectl exec -it <pod-name> -- /bin/sh       # Shell into pod
kubectl delete pod <pod-name>                # Delete pod
```

### Helm
```bash
helm template <name> ./chart                 # Dry-run, see output
helm upgrade --install <name> ./chart        # Install or upgrade
helm list                                    # List releases
helm rollback <name> <revision>              # Rollback
```

### ArgoCD (via kubectl)
```bash
kubectl get applications -n argocd                    # List apps
kubectl delete application <name> -n argocd           # Delete app
kubectl apply -f apps/                                # Apply app definitions
kubectl describe application <name> -n argocd         # App details
```

### ArgoCD CLI (if installed)
```bash
argocd app list                              # List apps
argocd app sync <app-name>                   # Sync app
argocd app sync <app-name> --force --prune   # Force sync
argocd app get <app-name>                    # App details
```

---

## 📖 Resources

### Documentation
- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [Helm Official Docs](https://helm.sh/docs/)
- [ArgoCD Official Docs](https://argo-cd.readthedocs.io/)

### Tutorials
- [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [GitOps with ArgoCD](https://argoproj.github.io/argo-cd/getting_started/)

### Practice
- [Kubernetes Playground (Katacoda)](https://www.katacoda.com/courses/kubernetes)
- [Play with Kubernetes](https://labs.play-with-k8s.com/)

---

## 📝 Notes

- Rate limits on Docker Hub: 100 pulls/6h (anonymous), 200 pulls/6h (authenticated)
- Always test Helm templates with `helm template` before deploying
- ArgoCD caches Git repos - restart `argocd-repo-server` if stuck
- Multi-arch images are essential for ARM-based machines (Apple Silicon, AWS Graviton)
- Use separate ArgoCD Applications for each service (UI, API) for independent deployments
