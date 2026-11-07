---
title: "Ingress overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Ingress-overview"
---

Ingress, as an independent resource within a Kubernetes cluster, is used to define forwarding rules for external access traffic, and traffic is forwarded to one or more Services through the Ingress controller. This topic introduces the Ingress types that VKE supports, and their differences.

<span id="alb-ingress"></span>
## ALB Ingress

Application Load Balancer (ALB) is dedicatedly designed for Layer 7 and delivers exceptional business processing performance. For large\-scale traffic distribution scenarios such as application\-layer websites and audio/video applications, it can provide precise and balanced traffic scheduling, eliminating the impact of a single point of failure. BytePlus ALB is compatible with multiple application\-layer protocols, including HTTP, HTTPS, HTTP/2, WebSocket, and QUIC, capable of satisfying the requirements of various business types.


1. VKE provides ALBInstance resources for configuring ALB instances and listeners. With ALBInstance resources created, the system in turn creates ALB instances and the corresponding listeners according to the configuration.

2. Ingress is a standard Kubernetes resource object used to manage HTTP and HTTPS access from outside the cluster to the internal services running in the cluster. For example, requests can be forwarded to different services based on the hosts and URL.

3. ALB Ingress controller is an add\-on in VKE clusters, responsible for listening to and resolving the configurations of ALBInstance and Ingress resources. If relevant resources are increased, deleted, or modified, the listeners and forwarding rules on the ALB side will be refreshed based on the corresponding configuration.

4. When users access services running in the cluster from outside through the ALB, the ALB instance forwards traffic according to listener configurations and forwarding policies. The traffic is sent to corresponding service ports on backend servers and eventually to associated workloads.


<span id="clb-ingress"></span>
## CLB Ingress

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ALB Ingresses offer richer features and higher reliability. To ensure the security and stability of your business, we recommend that you select ALB Ingresses for business deployments in clusters.</div>


CLB is a service that distributes incoming traffic to multiple backend servers based on policies. It helps the system enhance its service capability, eliminate single points of failure, and improve overall availability.


1. Ingress is a standard Kubernetes resource object used to manage HTTP and HTTPS access from outside the cluster to the internal services running in the cluster. For example, requests can be forwarded to different services based on the hosts and URL.

2. Ingress controller is an add\-on in VKE clusters, responsible for listening to and resolving the configurations of Ingress resources. If relevant resources are increased, deleted, or modified, the listeners and forwarding rules on the CLB side will be refreshed based on the corresponding configuration.

3. When users access the services running in the cluster from outside through the CLB, the CLB instance forwards traffic to the corresponding service ports on the backend servers as configured in listeners and forwarding policies, and eventually to the associated workloads.


<span id="nginx-ingress"></span>
## Nginx Ingress

Nginx Ingress is a Kubernetes controller that uses Nginx as a reverse proxy and load balancer. You can achieve 7\-layer load balancing by deploying the Nginx Ingress add\-on provided by VKE within the cluster.


1. Ingress is a standard Kubernetes resource object used to manage HTTP and HTTPS access from outside the cluster to the internal services running in the cluster. For example, requests can be forwarded to different services based on the hosts and URL.

2. Ingress\-nginx is an add\-on in VKE clusters, responsible for listening to and resolving the configurations of Ingress resources. With the add\-on installed in the cluster, an Ingress Nginx controller instance runs correspondingly on the nodes.

3. When traffic is coming, CLB first forwards it to the Ingress Nginx Controller instance in the cluster. The controller then passes it on to the corresponding workloads based on the forwarding rules.


<span id="apig-ingress"></span>
## APIG Ingress

API Gateway (APIG) is a managed cloud\-native gateway service with high scalability and availability on the cloud. Built on traditional traffic gateways, APIG integrates rich features to provide service discovery and service governance capabilities, enabling communication between internal and external networks within microservice architecture, and ensuring fast and secure communication between services and between services and clients. BytePlus APIG is compatible with application\-layer protocols, including HTTP and HTTPS, capable of satisfying the requirements of various business types.


1. VKE provides APIGInstance resources for configuring APIG instances and listeners. With ALBInstance resources created, the system in turn creates ALB instances and enables Ingress synchronization according to the configuration.

2. Ingress is a standard Kubernetes resource object used to manage HTTP and HTTPS access from outside the cluster to the internal services running in the cluster. For example, requests can be forwarded to different services based on the hosts and URL.

3. APIG Ingress controller is an add\-on in VKE clusters, responsible for listening to and resolving the configurations of APIGInstance and Ingress resources. If relevant resources are increased, deleted, or modified, the listeners and forwarding rules on the APIG side will be refreshed based on the corresponding configuration.

4. When users access the services running in the cluster from outside through APIG, the APIG instance forwards traffic to the corresponding service ports on the backend servers according to the Ingress and upstream configuration, and eventually to the associated workloads.
