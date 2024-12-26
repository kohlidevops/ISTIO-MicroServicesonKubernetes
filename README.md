# ISTIO-MicroServicesonKubernetes

➤ On Kubernetes we can deploy a variety of Applications.

➤ Those services could be Stand Alone Services that nothing to do with Other Services or Micro-Services, some small services that make an Application.

➤ Micro-Service Architecture is very Popular in these days and widely being used in Top IT Firms.

➤ Micro-Service Facilitate Developer to Split Application multiple chunks and individual processing capacity.

**Simple Micro Service**

![image](https://github.com/user-attachments/assets/5bf85533-447d-45be-9073-8899b42507b8)

**Complicated Micro services**

![image](https://github.com/user-attachments/assets/410cd5b5-e503-4c07-9cbc-51876ee085d6)

## Challenges with Microservices:

➤ No Encryption

➤ No Load Balancing

➤ No Failover / Auto Retries

➤ Routing Decisions

➤ Load Metrics/ Logs

➤ Access Control to Services

**How this challenges are resolove? With the help of Istio we can resolve or address this issues.**

➤ Istio service mesh provides several capabilities for traffic monitoring, access control, discovery, security, resiliency, and other useful things to a bundle of services.

➤ Istio deployed for Micro Services without any change in code of Micro Service.

➤ To make this possible, Istio deploys an Istio proxy (called an Istio sidecar) next to each service.

➤ All of the traffic meant for assistance is directed to the proxy, which uses policies to decide how, when, or if that traffic should be deployed to the service.

## How Istio Works With Containers and Kubernetes

➤ Istio service mesh, as suggested, uses a sidecar container implementation of the features and functions required mainly for microservices.

![image](https://github.com/user-attachments/assets/e3206222-1d69-41ee-9406-bb6f89137912)

**1. Services (Service A and Service B)**
   
Each service (such as svcA and svcB) is running inside a Kubernetes pod.

The communication between these services (HTTP, gRPC, TCP) is routed through Envoy proxies.

**2. Envoy Proxy**

Envoy is a sidecar proxy that is deployed alongside each service within its pod. 

It handles:

Service-to-service communication: Intercepts all inbound and outbound traffic for the service, allowing Istio to manage and secure the communication.

Traffic control: Supports routing rules, retries, timeouts, and circuit breakers.

Observability: Collects telemetry data on service traffic (latency, traffic volume, etc.).

Security: Enforces security policies, such as mutual TLS between services.

**3. Control Plane**

The Control Plane is responsible for managing the proxies (Envoys) and enforcing policies across the service mesh. 

It consists of several components:

Pilot: Distributes configuration and routing rules to Envoy proxies. It ensures that each proxy has the necessary information for traffic management.

Mixer: Handles policy checks and telemetry collection, ensuring that traffic complies with the defined policies and collecting data on the traffic.

Istio-Auth (now replaced by Citadel in recent versions): Manages security policies and generates TLS certificates for secure communication between services.

**4. How It Works with Kubernetes**

Sidecar Injection: Istio automatically injects the Envoy proxy as a sidecar container into every pod when the pod is created in the Kubernetes cluster.

Routing Traffic: The traffic to and from the service (e.g., svcA and svcB) passes through the Envoy proxy, which applies any Istio-defined policies, performs routing, and collects telemetry.

Security: Istio ensures mutual TLS encryption between services by issuing certificates via Istio-Auth (or Citadel), which are provided to the Envoy proxies.

**5. Communication Flow**

When svcA wants to communicate with svcB, the request first goes through the Envoy proxy in svcA's pod.

The Envoy proxy checks with the control plane (Pilot, Mixer, etc.) for the necessary routing and policy information.

The request is then forwarded to the Envoy proxy in svcB's pod, which forwards the request to the actual svcB service.

This communication can happen with or without TLS, depending on the policies enforced by Istio.
