---
tags: [internals, kubernetes]
week: W15
---
# ☸️ Kubernetes Internals (important parts only)

## 1. The core idea: declarative state + reconciliation
You write **desired state** into the API server. **Controllers** keep watching and drive **actual state** toward it. They are *level-triggered* (they reconcile the full state, not individual events), so missed events self-heal.

## 2. API server & etcd
- The API server is the **only** component that talks to etcd
- Request pipeline: **authentication → authorization (RBAC) → mutating admission (webhooks, defaults) → schema validation → validating admission → persist to etcd**
- Every object has a `resourceVersion` → **optimistic concurrency** (a conflict returns 409; clients retry)
- **Watch**: etcd watch → API server watch cache → clients stream changes
- **etcd**: a Raft-replicated KV with MVCC revisions; needs compaction/defrag; keep it small and fast (latency-sensitive disks)

## 3. Controllers & informers (client-go)
- **Informer** = list + watch → a local **cache** (indexer) → event handlers → push keys to a **rate-limited work queue** → workers call `Reconcile(key)`
- Shared informers avoid N controllers hammering the API server
- **Owner references** + the garbage collector: deleting a Deployment cascades to its ReplicaSets and Pods
- Chain: Deployment controller → ReplicaSet → RS controller → Pods (unscheduled)

## 4. Scheduler
- Watches Pods with no `nodeName` → **filter** (resources fit, taints/tolerations, affinity, volume topology) → **score** (spread, least-allocated, image locality) → **bind**
- Scheduling uses **requests**, not limits. Priority classes + **preemption**

## 5. kubelet & the node
- Watches Pods bound to its node → **CRI** (containerd) → creates the sandbox (**pause container** holds the network namespace) → the **CNI** plugin wires the network (veth, IP) → **CSI** mounts volumes → init containers → app containers
- Runs **probes**; reports status; **evicts** Pods under memory/disk pressure
- Enforces resources via **cgroups**: CPU limit = CFS quota → **throttling** (latency spikes!) · memory limit → **OOMKilled**
- QoS classes (Guaranteed / Burstable / BestEffort) decide eviction order

## 6. Service networking
- Every Pod gets a routable IP (flat network via CNI)
- **Service** = a stable virtual IP + DNS name; **EndpointSlices** list the ready Pod IPs (**readiness** decides membership)
- **kube-proxy** programs iptables/IPVS (or eBPF with Cilium) to DNAT the VIP → a Pod IP; conntrack keeps connections sticky
- ⚠️ Long-lived connections (gRPC/HTTP2) stick to one Pod → no load balancing → use L7 (Envoy/mesh) or client-side LB

## 7. Pod termination (a classic source of 502s)
Delete → Pod marked Terminating → **in parallel**: (a) endpoints removed, which propagates to kube-proxy/LBs, and (b) `preStop` hook → **SIGTERM** → grace period → SIGKILL
→ Race: traffic still arrives after SIGTERM → add a short `preStop` sleep + graceful shutdown in the app

## 8. The full journey of `kubectl apply -f deploy.yaml`
kubectl → API server (authn/authz/admission) → etcd → Deployment controller creates an RS → RS controller creates Pods → scheduler binds → kubelet → containerd/runc + CNI → probes pass → EndpointSlice updated → kube-proxy/Envoy routes traffic

## 🔬 Prove it
- [ ] `kubectl get --raw /api/v1/namespaces/default/pods | jq` and `kubectl get pods -w -v=8` (see the watch HTTP calls)
- [ ] Write down the full `kubectl apply` journey, then verify it with `kubectl get events --sort-by=.lastTimestamp`
- [ ] Two clients update the same ConfigMap with a stale `resourceVersion` → observe the 409
- [ ] CPU throttling: a CPU-hungry pod with a 200m limit → watch `container_cpu_cfs_throttled_periods_total` and latency
- [ ] Remove `preStop` + fast shutdown → run k6 during a rollout → count 5xx → fix it → 0 errors
- [ ] `iptables-save | grep KUBE-SVC` on a kind node: find your Service's DNAT rules
- [ ] Build a controller with kubebuilder (`OrbitWorkerPool`) → [[Assignments - Phase 4]]

## Interview questions #interview-q
What happens on `kubectl apply` · how Services route traffic · readiness vs liveness · requests vs limits (CPU throttling, OOM) · how controllers work · why gRPC doesn't load-balance behind a ClusterIP · graceful shutdown in K8s
