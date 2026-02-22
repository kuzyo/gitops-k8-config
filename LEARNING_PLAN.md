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

### ArgoCD
- [x] ArgoCD architecture (repo-server, application-controller, server)
- [x] Application CRD configuration
- [x] Sync policies (automated, selfHeal, prune)
- [x] ArgoCD with Helm charts
- [x] Debugging ArgoCD sync issues
- [x] Force sync and cache clearing

### CI/CD with GitHub Actions
- [x] Building and pushing Docker images
- [x] Updating Kubernetes manifests with `sed`
- [x] Separate workflows for build vs promote
- [x] Environment-specific deployments (dev auto-deploy, staging/prod manual)

---

## 🔄 In Progress

### Complete Current Setup
- [ ] Create Helm chart for API (same pattern as UI)
- [ ] Add `imagePullSecrets` to Helm templates
- [ ] Update CI/CD to use `yq` for Helm values updates
- [ ] Delete old manifest folders (`development/`, `staging/`, `production/`)

---

## 📚 Next Topics to Learn

### Level 1: Essential Kubernetes Features

#### Ingress & Networking
- [ ] Ingress controllers (nginx-ingress)
- [ ] Ingress resources and routing rules
- [ ] Host-based and path-based routing
- [ ] TLS/SSL termination
- [ ] Local development with `/etc/hosts`

#### Configuration Management
- [ ] ConfigMaps - Non-sensitive configuration
- [ ] Secrets - Sensitive data (passwords, API keys)
- [ ] Environment variables from ConfigMaps/Secrets
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
├── apps/                           # ArgoCD Application definitions
│   ├── application-development.yaml
│   ├── application-staging.yaml
│   └── application-production.yaml
├── charts/                         # Helm charts
│   └── ui/
│       ├── Chart.yaml
│       ├── values.yaml             # Default values
│       ├── templates/
│       │   ├── deployment.yaml
│       │   └── service.yaml
│       └── environments/           # Environment-specific values
│           ├── development/
│           │   └── values.yaml
│           ├── staging/
│           │   └── values.yaml
│           └── production/
│               └── values.yaml
├── development/                    # OLD - To be deleted
├── staging/                        # OLD - To be deleted
└── production/                     # OLD - To be deleted
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

### ArgoCD
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