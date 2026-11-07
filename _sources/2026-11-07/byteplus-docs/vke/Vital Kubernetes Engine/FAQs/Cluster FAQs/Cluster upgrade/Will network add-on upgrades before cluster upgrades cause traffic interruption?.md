---
title: "Will network add-on upgrades before cluster upgrades cause traffic interruption?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Does-upgrading-network-add-ons-before-upgrading-a-cluster-cause-traffic-interruption"
---

The pre\-check for upgrading clusters prompts that you need to upgrade the core\-dns add\-on or the ingress\-nginx add\-on. When you upgrade these types of network traffic add\-ons, the causes for traffic interruption differ by add\-on type.


* **core\-dns**

   CoreDNS instances of the add\-on provide services through a Service. Therefore, when the number of instance replicas changes, some requests may be affected. The specific impact depends on how the Service is provided.

   * If the cluster uses the Flannel network model: In common scenarios, no errors will be reported for requests. However, when IPVS is used as the kube\-proxy working mode, errors will be reported for a small number of requests, which will persist for several seconds after CoreDNS is fully ready. When QPS is low, the errors can persist for up to 5 minutes, which is the default session timeout period for IPVS.

   * If the cluster uses the VPC\-CNI network model: Errors will be reported for a small number of requests, which will persist for several seconds after CoreDNS is fully ready.

* **ingress\-nginx**

   Impacts vary based on the specific type of add\-on upgrade.

   * If the upgrade only involves configuration changes, ingress\-nginx will update the worker process configurations of the data plane Nginx. Nginx supports hot configuration updates. Therefore, business traffic will not be affected in common scenarios. However, in exceptional scenarios, some requests will receive 5XX responses that last for several seconds.

   * If the upgrade involves changes to the image tag or instance type, the ingress\-nginx instances will be recreated. After the instances are started as expected, clients may receive 5XX error responses, which last for several seconds.
