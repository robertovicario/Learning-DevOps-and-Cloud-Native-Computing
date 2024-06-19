# Istio Observability

## Overview

Istio generates detailed telemetry for all service communications within a mesh. This telemetry provides observability of service behavior, empowering operators to troubleshoot, maintain, and optimize their applications – without imposing any additional burdens on service developers. Through Istio, operators gain a thorough understanding of how monitored services are interacting, both with other services and with the Istio components themselves.

## Metrics

Istio generates a set of service metrics based on the four “golden signals” of monitoring (latency, traffic, errors, and saturation). Istio also provides detailed metrics for the mesh control plane. A default set of mesh monitoring dashboards built on top of these metrics is also provided.

- Proxy-level metrics: Istio metrics collection begins with the sidecar proxies (Envoy). Each proxy generates a rich set of metrics about all traffic passing through the proxy (both inbound and outbound). The proxies also provide detailed statistics about the administrative functions of the proxy itself, including configuration and health information.
- Service-level metrics: In addition to the proxy-level metrics, Istio provides a set of service-oriented metrics for monitoring service communications. These metrics cover the four basic service monitoring needs: latency, traffic, errors, and saturation. Istio ships with a default set of dashboards for monitoring service behaviors based on these metrics.
- Control plane metrics: The Istio control plane also provides a collection of self-monitoring metrics. These metrics allow monitoring of the behavior of Istio itself (as distinct from that of the services within the mesh).

## Distributed Traces

Istio generates distributed trace spans for each service, providing operators with a detailed understanding of call flows and service dependencies within a mesh.

<img src="../services/img/5.png" alt="Distributed Traces" width=256>

## Access Logs

As traffic flows into a service within a mesh, Istio can generate a full record of each request, including source and destination metadata. This information enables operators to audit service behavior down to the individual workload instance level.

<img src="../services/img/6.png" alt="Access Logs" width=256>

## References

- [istio.io/docs](https://istio.io/latest/docs/)
