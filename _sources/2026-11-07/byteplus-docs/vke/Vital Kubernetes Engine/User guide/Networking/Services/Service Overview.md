---
title: "Service Overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Service-overview"
---

<span id=".cG9kLeeahOiuv-mXrumXrumimA=="></span>
## Issues regarding pod access

After workloads are created, multiple pods are running. Because pods support auto\-scaling, accessing pods can cause the following issues:


* Uncertain results of pod access. Pods are created or deleted at any time by controllers such as Deployment. As a result, it is not stable to access pods directly.

* The IP address of a pod is assigned only after the pod starts. The IP address is unknown before the pod starts.

* Because a workload consists of a group of pods running the same image, accessing pods one by one can cause issues.


<span id=".5L2_55SoLXNlcnZpY2Ut6Kej5YazLXBvZC3nmoTorr_pl67pl67popg="></span>
## Using service to avoid the issues

The service object in Kubernetes is designed to solve the issues described above. Each service has a fixed IP address, so you can access workloads by accessing the service. A service selects pods according to labels and forwards traffic to the pods. Additionally, a service also provides load balancing for pods.

<span id=".c2VydmljZS3nmoTnsbvlnos="></span>
## Service types

There are several service types applicable to different scenarios.  


* [ClusterIP](https://docs.byteplus.com/en/docs/vke/ClusterIP): Exposes workloads to other workloads in the same cluster and allows access by using **internal domain names**.

* [NodePort](https://docs.byteplus.com/en/docs/vke/NodePort): It exposes a static port on each node so external clients can access the Service. External users can access the Service by sending requests to **NodeIP:NodePort**.

* [ExternalName](https://docs.byteplus.com/en/docs/vke/ExternalName?TagIDs=2,255&lang=en): It maps an internal service name to an external domain name within a cluster, allowing Pods in the cluster to access the external domain name using the Service name.

* [LoadBalancer](https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_overview): By using an external load balancer, traffic can be distributed across multiple Pods in the cluster. When a LoadBalancer Service is created, the system creates or reuses an external Load Balancer instance to expose the service to the public or internal network.
