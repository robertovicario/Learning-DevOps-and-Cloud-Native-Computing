# Istio Traffic Management

Istio uses a service discovery system to find endpoints in a mesh network and directs traffic accordingly. Envoy proxies handle traffic distribution among service instances. Istio offers advanced traffic management features like A/B testing, custom load balancing, and traffic rules through its traffic management API.

## Virtual Services

Virtual services, in conjunction with destination rules, form the foundation of Istio's traffic routing. They allow configuration of request routing within an Istio service mesh, enhancing basic connectivity and discovery. Each virtual service comprises routing rules that Istio evaluates sequentially to direct requests to specific destinations within the mesh. The complexity of your mesh determines whether you need multiple virtual services or none at all.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: reviews
spec:
  hosts:
  - reviews
  http:
  - match:
    - headers:
        end-user:
          exact: jason
    route:
    - destination:
        host: reviews
        subset: v2
  - route:
    - destination:
        host: reviews
        subset: v3
```

## Destination Rules

Destination rules complement virtual services in Istio's traffic routing. While virtual services determine how traffic is routed to a destination, destination rules configure what happens to traffic for that destination. They are applied after virtual service routing rules, influencing traffic to the "real" destination. Destination rules specify named service subsets, such as grouping instances by version, which can then be used in virtual service routing rules to control traffic. Additionally, destination rules allow customization of Envoy's traffic policies for the entire destination service or specific service subsets, including load balancing, TLS security, and circuit breaker settings.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: my-destination-rule
spec:
  host: my-svc
  trafficPolicy:
    loadBalancer:
      simple: RANDOM
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2
    trafficPolicy:
      loadBalancer:
        simple: ROUND_ROBIN
  - name: v3
    labels:
      version: v3
```

## Gateways

Gateways in Istio manage inbound and outbound traffic for a mesh, controlling which traffic enters or leaves. Unlike Kubernetes Ingress APIs, Istio gateways offer more flexibility in traffic routing. They focus on layer 4-6 load balancing properties and are bound to regular virtual services for application-layer traffic routing. Gateways primarily handle ingress traffic but can also configure egress gateways for controlling outbound traffic. Istio provides preconfigured gateway proxy deployments, but users can customize or deploy their own gateways as needed.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: ext-host-gwy
spec:
  selector:
    app: my-gateway-controller
  servers:
  - port:
      number: 443
      name: https
      protocol: HTTPS
    hosts:
    - ext-host.example.com
    tls:
      mode: SIMPLE
      credentialName: ext-host-cert
```

## Service Entries

Service entries in Istio enable adding entries to the internal service registry, allowing Envoy proxies to direct traffic to services as if they were part of the mesh. They facilitate managing traffic for services external to the mesh, including redirecting and forwarding traffic, defining retry policies, and incorporating services from legacy infrastructure or virtual machines into the mesh. While Istio's default configuration allows passthrough requests to unknown services, service entries are necessary for leveraging Istio features to control traffic to external destinations registered in the mesh.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: ServiceEntry
metadata:
  name: svc-entry
spec:
  hosts:
  - ext-svc.example.com
  ports:
  - number: 443
    name: https
    protocol: HTTPS
  location: MESH_EXTERNAL
  resolution: DNS
```

## Sidecars

Istio's default configuration allows every Envoy proxy to accept traffic on all associated workload ports and reach every workload in the mesh. However, sidecar configurations enable fine-tuning of these settings, including specifying the ports and protocols accepted by an Envoy proxy and limiting the services it can reach. This is particularly useful in larger applications to prevent potential performance issues caused by high memory usage. Sidecar configurations can be applied universally to all workloads in a namespace or selectively using workload selectors.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Sidecar
metadata:
  name: default
  namespace: bookinfo
spec:
  egress:
  - hosts:
    - "./*"
    - "istio-system/*"

```

## Network Testing

- Timeouts: A timeout is the amount of time that an Envoy proxy should wait for replies from a given service, ensuring that services don’t hang around waiting for replies indefinitely and that calls succeed or fail within a predictable timeframe. The Envoy timeout for HTTP requests is disabled in Istio by default.

- Retries: A retry setting specifies the maximum number of times an Envoy proxy attempts to connect to a service if the initial call fails. Retries can enhance service availability and application performance by making sure that calls don’t fail permanently because of transient problems such as a temporarily overloaded service or network. The interval between retries (25ms+) is variable and determined automatically by Istio, preventing the called service from being overwhelmed with requests. The default retry behavior for HTTP requests is to retry twice before returning the error.

- Circuit Breakers: Circuit breakers are another useful mechanism Istio provides for creating resilient microservice-based applications. In a circuit breaker, you set limits for calls to individual hosts within a service, such as the number of concurrent connections or how many times calls to this host have failed. Once that limit has been reached the circuit breaker “trips” and stops further connections to that host. Using a circuit breaker pattern enables fast failure rather than clients trying to connect to an overloaded or failing host.

- Fault Injection: After you’ve configured your network, including failure recovery policies, you can use Istio’s fault injection mechanisms to test the failure recovery capacity of your application as a whole. Fault injection is a testing method that introduces errors into a system to ensure that it can withstand and recover from error conditions. Using fault injection can be particularly useful to ensure that your failure recovery policies aren’t incompatible or too restrictive, potentially resulting in critical services being unavailable.

## References

- [istio.io/docs](https://istio.io/latest/docs/)
