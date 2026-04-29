# CRI-O (cri-o)

CRI-O is a CNCF graduated, lightweight container runtime built specifically for Kubernetes. It implements the Kubernetes Container Runtime Interface (CRI) gRPC API and uses any OCI-compatible runtime, including runc and crun, as the underlying container executor. CRI-O integrates with the containers/image and containers/storage libraries, the conmon container monitor, and CNI plugins to deliver a minimal kubelet-facing runtime surface, while also exposing an HTTP status API and Prometheus metrics endpoint for operations and observability.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/cri-o/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Provider
- **Access:** Public
- **x-type:** opensource

## Tags

- Apache 2.0, CNCF, Cloud Native, conmon, Container Runtime, Containers, CRI, Go, Graduated, Kubernetes, OCI, Open Source, Prometheus, runc

## Timestamps

- **Created:** 2025-01-01
- **Modified:** 2026-04-28

## APIs

### CRI-O CRI gRPC API

The Kubernetes Container Runtime Interface implementation served over a Unix domain socket. Provides RuntimeService and ImageService for pod sandbox, container, image, and runtime status management.

- [Documentation](https://kubernetes.io/docs/concepts/architecture/cri/)
- [Specification](https://github.com/kubernetes/cri-api)
- [GitHub](https://github.com/cri-o/cri-o)

### CRI-O Status API

HTTP server exposing /info, /config, /containers/{id}, /pause/{id}, /unpause/{id}, and /debug endpoints for runtime introspection, container inspection, lifecycle control, and golang debugging.

- [Documentation](https://github.com/cri-o/cri-o)
- [OpenAPI](openapi/cri-o-status-openapi.yml)
- [Rules](rules/cri-o-status-rules.yml)
- [Capabilities](capabilities/cri-o-status-capabilities.yml)

### CRI-O Metrics API

Prometheus-compatible metrics endpoint exposing CRI-O operation counters, image pull telemetry, and error rates on the configured metrics port (default 9090) at the /metrics path.

- [Documentation](https://github.com/cri-o/cri-o/blob/main/docs/metrics.md)
- [OpenAPI](openapi/cri-o-metrics-openapi.yml)
- [Rules](rules/cri-o-metrics-rules.yml)
- [Capabilities](capabilities/cri-o-metrics-capabilities.yml)

## Common Properties

- [Website](https://cri-o.io/)
- [Documentation](https://github.com/cri-o/cri-o/tree/main/docs)
- [Getting Started](https://github.com/cri-o/cri-o/blob/main/install.md)
- [GitHub](https://github.com/cri-o/cri-o)
- [License (Apache 2.0)](https://github.com/cri-o/cri-o/blob/main/LICENSE)
- [CNCF Project Page](https://www.cncf.io/projects/cri-o/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
