---
title: 'Kubernetes v1.36: Pod-Level Resource Managers (Alpha)'
url: https://kubernetes.io/blog/2026/05/01/kubernetes-v1-36-feature-pod-level-resource-managers-alpha/
date: '2026-05-01'
author: ''
feed_url: https://kubernetes.io/feed.xml
---
Kubernetes v1.36 introduces Pod-Level Resource Managers as an alpha feature, bringing a more flexible and powerful resource management
model to performance-sensitive workloads. This enhancement extends the kubelet's
Topology, CPU, and Memory Managers to support pod-level resource specifications
( .spec.resources ), evolving them from a strictly per-container allocation
model to a pod-centric one. Why do we need pod-level resource managers? When running performance-critical workloads such as machine learning (ML)
training, high-frequency trading applications, or low-latency databases, you
often need exclusive, NUMA-aligned resources for your primary application
containers to ensure predictable performance. However, modern Kubernetes pods rarely consist of just one container. They
frequently include sidecar containers for logging, monitoring, service meshes,
or data ingestion. Before this feature, this created a trade-off, to get NUMA-aligned, exclusive
resources for your main application, you had to allocate exclusive,
integer-based CPU resources to every container in the pod. This might be
wasteful for lightweight sidecars. If you didn't do this, you forfeited the
pod's Guaranteed Quality of Service (QoS) class entirely, losing the performance
benefits. Introducing pod-level resource managers Enabling pod-level resources support for the resource managers (via the PodLevelResourceManagers and PodLevelResources feature gates) allows the
kubelet to create hybrid resource allocation models . This brings flexibility
and efficiency to high-performance workloads without sacrificing NUMA alignment. Real-world use cases Here are a few practical scenarios demonstrating how this feature can be
applied, depending on the configured Topology Manager scope: 1. Tightly-coupled database (Topology manager's pod scope) Consider a latency-sensitive database pod that includes a main database
container, a local metrics exporter, and a backup agent sidecar. When configured with the pod Topology Manager scope, the kubelet performs a
single NUMA alignment based on the entire pod's budget. The database container
gets its exclusive CPU and memory slices from that NUMA node. The remaining
resources from the pod's budget form a new pod shared pool . The metrics
exporter and backup agent run in this pod shared pool. They share resources with
each other, but they are strictly isolated from the database's exclusive slices
and the rest of the node. This allows you to safely co-locate auxiliary containers on the same NUMA node
as your primary workload without wasting dedicated cores on them. apiVersion : v1 kind : Pod metadata : name : tightly-coupled-database spec : # Pod-level resources establish the overall budget and NUMA alignment size. resources : requests : cpu : "8" memory : "16Gi" limits : cpu : "8" memory : "16Gi" initContainers : - name : metrics-exporter image : metrics-exporter:v1 restartPolicy : Always - name : backup-agent image : backup-agent:v1 restartPolicy : Always containers : - name : database image : database:v1 # This Guaranteed container gets an exclusive 6 CPU slice from the pod's budget. # The remaining 2 CPUs and 4Gi memory form the pod shared pool for the sidecars. resources : requests : cpu : "6" memory : "12Gi" limits : cpu : "6" memory : "12Gi" 2. ML workload with infrastructure sidecars (Topology manager's container scope) Imagine a pod running a GPU-accelerated ML training workload alongside a generic
service mesh sidecar. Under the container Topology Manager scope, the kubelet evaluates each
container individually. You can grant the ML container exclusive, NUMA-aligned
CPUs and Memory for maximum performance. Meanwhile, the service mesh sidecar
doesn't need to be NUMA-aligned; it can run in the general node-wide shared
pool. The collective resource consumption is still safely bounded by the overall
pod limits, but you only allocate NUMA-aligned, exclusive resources to the
specific containers that actually require them. apiVersion : v1 kind : Pod metadata : name : ml-workload spec : # Pod-level resources establish the overall budget constraint. resources : requests : cpu : "4" memory : "8Gi" limits : cpu : "4" memory : "8Gi" initContainers : - name : service-mesh-sidecar image : service-mesh:v1 restartPolicy : Always containers : - name : ml-training image : ml-training:v1 # Under the 'container' scope, this Guaranteed container receives exclusive, # NUMA-aligned resources, while the sidecar runs in the node's shared pool. resources : requests : cpu : "3" memory : "6Gi" limits : cpu : "3" memory : "6Gi" CPU quotas (CFS) and isolation When running these mixed workloads within a pod, isolation is enforced
differently depending on the allocation: Exclusive containers: Containers granted exclusive CPU slices have their
CPU CFS quota enforcement disabled at the container level, allowing them to
run without being throttled by the Linux scheduler. Pod shared pool containers: Containers falling into the pod shared pool
have CPU CFS quotas enforced at the pod level, ensuring they do not consume
more than the leftover pod budget. How to enable Pod-Level Resource Managers Using this feature requires Kubernetes v1.36 or newer. To enable it, you must
configure the kubelet with the appropriate feature gates and policies: Enable the PodLevelResources and PodLevelResourceManagers feature gates . Configure the Topology Manager with a policy other than none (i.e., best-effort , restricted , or single-numa-node ). Set the Topology Manager scope to either pod or container using the topologyManagerScope field in the KubeletConfiguration . Configure the CPU Manager with
the static policy. Configure the Memory Manager with the Static policy. Observability To help cluster administrators monitor and debug these new allocation models, we
have introduced several new kubelet metrics when the feature gate is enabled: resource_manager_allocations_total : Counts the total number of exclusive
resource allocations performed by a manager. The source label ("pod" or
"node") distinguishes between allocations drawn from the node-level pool
versus a pre-allocated pod-level pool. resource_manager_allocation_errors_total : Counts errors encountered during
exclusive resource allocation, distinguished by the intended allocation source ("pod" or "node"). resource_manager_container_assignments : Tracks the cumulative number of
containers running with specific assignment types. The assignment_type label ("node_exclusive", "pod_exclusive", "pod_shared") provides visibility
into how workloads are distributed. Current limitations and caveats While this feature opens up new possibilities, there are a few things to keep in
mind during its alpha phase. Be sure to review the Limitations and caveats in the official documentation for full details on compatibility, requirements,
and downgrade instructions. Getting started and providing feedback For a deep dive into the technical details and configuration of this feature,
check out the official concept documentation: Pod-level resource managers To learn more about the overall pod-level resources feature and how to assign
resources to pods, see: Assign Pod-level CPU and memory resources As this feature moves through Alpha, your feedback is invaluable. Please report
any issues or share your experiences via the standard Kubernetes communication
channels: Slack: #sig-node Mailing list Open Community Issues/PRs
