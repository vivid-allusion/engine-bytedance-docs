---
title: "CoreDNS FAQs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CoreDNS_FAQs"
---

<span id="5sxwdFOU"></span>
## **How do I troubleshoot the DNS resolution failure (nslookup kubernetes.default.svc.cluster.local) within a cluster?** 

When the `nslookup kubernetes.default.svc.cluster.local` resolution fails, we recommend performing troubleshooting in the following order:


1. First, check the `/etc/resolv.conf` configuration of the Pod and whether it points to the cluster DNS (kube\-dns/NodeLocal DNS).

2. Then, check whether the kube\-dns service is reachable and whether the CoreDNS Pod is ready and does not restart unexpectedly.

3. If the link from the Pod to kube\-dns is down, first check the DNS access path (networks, routes, and policies) instead of starting with the upstream DNS. "


<span id="v3kRzMNl"></span>
## Is it always a CoreDNS failure when **NXDOMAIN/no such host occurs**?

Not necessarily. In most cases, NXDOMAIN indicates that "the requested domain name does not exist or cannot be resolved at this time". We recommend performing troubleshooting in the following order:


1. Check whether the domain name spelling is correct, whether the namespace is correct, and whether the FQDN is used.

2. If a headless service is accessed, you also need to check that the corresponding endpoints are generated and are ready.

3. If the preceding items are normal, then check the CoreDNS log to determine whether it is a resolution chain failure.


<span id="wreyQ6Fs"></span>
## **How do I troubleshoot i/o timeout/no servers could be reached?** 

This type of error usually means that the DNS request does not receive a response within the timeout period. We recommend performing troubleshooting in the following order:


1. Check connectivity from the Pod to kube\-dns/NodeLocal DNS.

2. Check whether the CoreDNS process is healthy and whether the load is too high.

3. Check connectivity and forwarding configuration from CoreDNS to upstream DNS.

4. Check the node network, kube\-proxy, CNI, network policy, security group, and other factors that may affect UDP/TCP DNS.


<span id="zZeDcmiw"></span>
## **How do I troubleshoot the issue where only external domain names fail to be resolved while internal cluster resolution is normal?** 

This usually means CoreDNS can still resolve in\-cluster services, but encounters exceptions when forwarding requests to upstream DNS. We recommend focusing on checking the following items: whether nodes can connect to external networks, whether the upstream DNS is reachable and responds stably, whether the forwarding configurations of CoreDNS (forward/proxy) meet expectations, and whether the DNS configurations of the nodes are overwritten by other add\-ons.

<span id="eYfibWuy"></span>
## **How do I troubleshoot the issue where DNS exceptions occur only during peak hours?** 

Peak‑hour issues are more often caused by amplified DNS request volume (such as frequent resolution from short‑lived connections and multiple retries due to ndots/search settings) than by "insufficient CoreDNS performance". We recommend first evaluating the client‑side request pattern and the impact of ndots/search, and deciding whether NodeLocal DNS cache can be enabled. Only then consider increasing CoreDNS replicas or adjusting resources.

<span id="VzZAktju"></span>
## **How do I troubleshoot the issue where NodeLocal DNS remains abnormal after being enabled?** 

Common causes include:


1. The Pod does not use the local listening address of NodeLocal DNS (injection is missing or ineffective).

2. NodeLocal DNS is not ready or is unhealthy on the affected node.

3. The root cause is not in the cache layer, but lies in the upstream DNS, node network, or client request pattern.


<span id="JKSfHxyb"></span>
## Can increasing CoreDNS replicas solve all DNS timeout issues?

No. Scaling out CoreDNS only alleviates the issue where CoreDNS is overloaded. If the root cause is request increase due to ndots/search, UDP session/forwarding issues on the node, missing NodeLocal DNS, or slow upstream DNS responses, simply adding replicas usually only reduces the probability of occurrence, but does not eliminate the issue. We recommend first identifying the bottleneck and then choosing the appropriate method.

<span id="hacJM0SB"></span>
## Is HPA suitable as the default scaling solution for CoreDNS?

We do not recommend using HPA as the default solution. CoreDNS load is affected not only by CPU but also by the cache hit ratio, upstream DNS response quality, client request pattern, and more. A more reliable approach is to use observability data (request volume, timeout rate, cache hit ratio, and upstream latency) to set a manual scale\-out baseline and reserve some headroom.

<span id="M3IkvvCa"></span>
## How do I decide whether to escalate an issue to the network/platform side?

If any of the following conditions are met, escalate the issue to the network/platform side for joint root cause analysis:


* The Pod cannot connect to the kube\-dns Service.

* NodeLocal DNS or CoreDNS is unhealthy on the affected node.

* Node diagnostics already indicate DNS, network, or CNI exceptions.

* Only certain nodes, subnets, or workloads are consistently abnormal.

* Connectivity from CoreDNS to upstream DNS is unstable.
