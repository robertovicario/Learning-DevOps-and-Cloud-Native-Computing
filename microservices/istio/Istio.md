## Istio

## Overview

Istio is an open-source service mesh that provides a uniform way to secure, connect, and observe microservices. It enables developers to manage traffic flow between microservices, enforce access policies, and aggregate telemetry data, all without requiring changes to the microservice code. Istio achieves this by deploying a sidecar proxy to each service instance, which intercepts all network communication between microservices.

## Architecture

Istio's architecture consists of two main components: the data plane and the control plane. 

### Data Plane

The data plane is responsible for the actual traffic management between microservices. It includes the following key component:

- **Envoy:** Envoy is a high-performance proxy developed by Lyft. In Istio, Envoy is deployed as a sidecar alongside each microservice. Envoy intercepts all incoming and outgoing traffic to the microservice, providing a layer of abstraction that allows Istio to manage traffic, enforce policies, and collect telemetry data. Envoy handles tasks such as load balancing, circuit breaking, and retries.

### Control Plane

The control plane is responsible for managing and configuring the proxies to route traffic. It ensures that the data plane operates correctly and efficiently. The control plane consists of several components:

- **Istiod:** This component consolidates the functionalities of Pilot, Citadel, and Galley from previous Istio versions. Istiod is responsible for managing the configuration of the Envoy proxies, security, and policy enforcement.
- **Mixer:** (Deprecated in newer versions) Mixer was responsible for policy control and telemetry collection. It enforced access control and usage policies across the service mesh and gathered telemetry data from the Envoy proxies. In newer versions of Istio, Mixer’s functionality has been integrated into the Envoy proxies themselves to reduce latency and simplify the architecture.
- **Pilot:** Pilot was responsible for configuring the Envoy proxies. It managed service discovery, load balancing, and routing rules, translating high-level routing rules into configurations that Envoy could understand. In newer versions, its functionality is integrated into Istiod.
- **Citadel:** Citadel provided strong service-to-service and end-user authentication using mutual TLS, helping to secure service communication and manage service identities and certificates. Its functionality has also been integrated into Istiod.
- **Galley:** Galley was responsible for validating, processing, and distributing configuration changes across the service mesh. It ensured that the configurations applied to the data plane were correct and consistent. Galley's functions are now part of Istiod.
