# CRI-O (cri-o)

CRI-O is a CNCF graduated, lightweight container runtime built specifically for Kubernetes. It implements the Kubernetes Container Runtime Interface (CRI) gRPC API and uses any Open Container Initiative (OCI) compatible runtime, including runc and crun, as the underlying container executor. CRI-O integrates with the containers/image and containers/storage libraries, the conmon container monitor, and CNI plugins to deliver a minimal kubelet-facing runtime surface, while also exposing an HTTP status API and Prometheus metrics endpoint for operations and observability.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cri-o/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cri-o/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Provider
- **Access:** Public

## Tags

- Apache 2.0
- CNCF
- Cloud Native
- conmon
- Container Runtime
- Containers
- CRI
- Go
- Graduated
- Kubernetes
- OCI
- Open Source
- Prometheus
- runc

## Timestamps

- **Created:** 2025-01-01
- **Modified:** 2026-05-19

## APIs

### CRI-O CRI gRPC API

CRI-O implements the Kubernetes Container Runtime Interface (CRI) gRPC API that the kubelet uses to manage pod sandboxes, containers, image lifecycle, and runtime status. The CRI gRPC API is served over a Unix domain socket (default /var/run/crio/crio.sock) and includes services for RuntimeService and ImageService as defined by the upstream CRI protobuf specification.

- **Human URL:** [https://kubernetes.io/docs/concepts/architecture/cri/](https://kubernetes.io/docs/concepts/architecture/cri/)

#### Tags

- CRI
- gRPC
- Kubelet
- Kubernetes

#### Properties

- [Documentation](https://kubernetes.io/docs/concepts/architecture/cri/)
- [Specification](https://github.com/kubernetes/cri-api)
- [GitHub Repository](https://github.com/cri-o/cri-o)
- [Postman Collection](collections/cri-o-metrics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cri-o-metrics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/cri-o-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cri-o-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CRI-O Status API

The CRI-O Status API is an HTTP server exposed by the cri-o daemon for runtime introspection, container inspection, and lifecycle control. It provides /info and /config endpoints for daemon configuration, /containers/{id} for live container inspection, /pause/{id} and /unpause/{id} to control container execution, and /debug endpoints for golang debugging. As noted upstream, this API is not considered stable for production use.

- **Human URL:** [https://github.com/cri-o/cri-o](https://github.com/cri-o/cri-o)
- **Base URL:** `http://localhost`

#### Tags

- Debugging
- HTTP
- Lifecycle
- Status

#### Properties

- [Documentation](https://github.com/cri-o/cri-o)
- [OpenAPI](openapi/cri-o-status-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cri-o-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cri-o-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Rules](rules/cri-o-status-rules.yml)
- [Capabilities](capabilities/cri-o-status-capabilities.yml)

### CRI-O Metrics API

The CRI-O metrics endpoint exposes Prometheus-compatible metrics for operation counts, container lifecycle, image pulls, and errors. It is enabled with the --enable-metrics flag and served on the configured port (default 9090) at the /metrics path. The endpoint can also be served over a Unix socket and secured with TLS for cluster-grade observability.

- **Human URL:** [https://github.com/cri-o/cri-o/blob/main/docs/metrics.md](https://github.com/cri-o/cri-o/blob/main/docs/metrics.md)
- **Base URL:** `http://localhost:9090`

#### Tags

- Metrics
- Monitoring
- Observability
- Prometheus

#### Properties

- [Documentation](https://github.com/cri-o/cri-o/blob/main/docs/metrics.md)
- [OpenAPI](openapi/cri-o-metrics-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cri-o-metrics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cri-o-metrics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Rules](rules/cri-o-metrics-rules.yml)
- [Capabilities](capabilities/cri-o-metrics-capabilities.yml)

## Common Properties

- [Website](https://cri-o.io/)
- [Documentation](https://github.com/cri-o/cri-o/tree/main/docs)
- [Getting Started](https://github.com/cri-o/cri-o/blob/main/install.md)
- [GitHub Organization](https://github.com/cri-o)
- [GitHub Repository](https://github.com/cri-o/cri-o)
- [Blog](https://cri-o.io/#blog)
- [Changelog](https://github.com/cri-o/cri-o/releases)
- [Community](https://github.com/cri-o/cri-o#getting-started)
- [License](https://github.com/cri-o/cri-o/blob/main/LICENSE)
- [C N C F](https://www.cncf.io/projects/cri-o/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
