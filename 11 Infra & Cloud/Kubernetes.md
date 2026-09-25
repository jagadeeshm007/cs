---
tags: [infra, kubernetes]
phase: 4
---
# ☸️ Kubernetes

## Core → Advanced
- [ ] Architecture: API server, etcd, scheduler, controller manager, kubelet, kube-proxy; the **reconciliation loop** ⭐
- [ ] Workloads: Pod, ReplicaSet, **Deployment**, StatefulSet, DaemonSet, Job/CronJob
- [ ] Networking: Service (ClusterIP/NodePort/LoadBalancer), DNS, **Ingress** vs **Gateway API** ⭐, NetworkPolicy, CNI (Cilium awareness)
- [ ] Config: ConfigMaps, Secrets (+ External Secrets Operator / Sealed Secrets)
- [ ] Health: liveness vs readiness vs startup probes (and how wrong probes cause outages)
- [ ] Resources: requests vs limits, QoS classes, OOMKilled, CPU throttling
- [ ] Scaling: HPA (CPU/custom metrics), **KEDA** (scale on Kafka lag ⭐), VPA, Cluster Autoscaler / Karpenter
- [ ] Storage: PV, PVC, StorageClass
- [ ] Rollouts: rolling update strategy, PodDisruptionBudgets, Argo Rollouts (canary)
- [ ] RBAC, ServiceAccounts, Pod Security Standards
- [ ] Packaging: **Helm** (and Kustomize)
- [ ] Operators & CRDs (build one with kubebuilder: advanced)
- [ ] Debugging: `kubectl describe/logs/events/exec/debug`, **k9s**
- [ ] Local clusters: **kind** / k3d / minikube

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 kind cluster; deploy with Helm; k9s
- [ ] 🟡 Probes + `preStop` + graceful shutdown: 0 errors during a rollout under k6
- [ ] 🔴 KEDA autoscaling of workers on queue depth / Kafka lag
- [ ] 🔴 A **kubebuilder operator**: `OrbitWorkerPool` CRD
- [ ] ⚫ Kubernetes the Hard Way

## 🧠 Cognitive tasks
- [ ] Trace `kubectl apply` through every component (write it, then verify it)
- [ ] Symptom → hypotheses: "1% 502s for 20 s after every deploy"

## 🛰️ Orbit integration
- [ ] [[Orbit v3 - Cloud Native]] runs entirely on K8s

> [!info] Go deeper
> ⚙️ [[Kubernetes Internals]] · [[Container Internals]] · 🧩 [[Distributed & Cloud Patterns]] (operator, sidecar)

## Resources
- kubernetes.io docs ⭐ · *Kubernetes Up & Running* 3e · *Kubernetes in Action* (Lukša)
- KodeKloud CKAD course · Kelsey Hightower's *Kubernetes the Hard Way* · learnk8s.io articles ⭐
