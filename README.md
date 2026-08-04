# CRI-O (cri-o)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
