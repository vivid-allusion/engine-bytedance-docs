---
title: "Using NodeLocal DNSCache as a DNS caching proxy"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache"
---

NodeLocal DNSCache cache solution provides a DNS cache proxy for nodes, improving DNS service discovery performance and stability across the entire cluster. This topic describes how to configure NodeLocal DNSCache in a cluster.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

In large\-scale applications, overwhelming DNS requests place significant pressure on CoreDNS, resulting in increased DNS latency and adversely affecting business performance. To improve performance, users often need to upgrade CoreDNS specifications or perform scale\-out, which increases operation and maintenance complexity, yet delivers a disappointing result.

To address the above issues, Kubernetes officially provides the NodeLocal DNSCache solution, which can effectively improve DNS performance and stability in large\-scale clusters. In a VKE cluster, the node\-local\-dns add\-on can be used as the NodeLocal DNSCache for the cluster. This add\-on runs in a DaemonSet on each node in the cluster, working as a DNS cache proxy on nodes to improve the performance and stability of DNS service discovery in the cluster.

DNS cache configuration is injected into pods as soon as node\-local\-dns add\-on is installed in the cluster. After that, the DNS resolution will take the following steps:


1. **NodeLocal DNSCache resolution**: Pods first send queries to NodeLocal DNSCache (169.254.20.10) on their nodes. If NodeLocal DNSCache is unreachable or a cache miss occurs, the queries are sent to CoreDNS in the cluster.

2. **CoreDNS resolution**: If NodeLocal DNSCache does not have a cached response for the query, the query is sent to CoreDNS (10.0.0.10) through the kube\-dns service for resolution.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7242231e8dad8de796a1a713a5fa2c67.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details on NodeLocal DNSCache, see <a href="https://kubernetes.io/docs/tasks/administer-cluster/nodelocaldns/">Kubernetes documentation</a>.</div>


<span id=".57uE5Lu26K-05piO"></span>
## Limits


* When a VCI\-type Pod uses the NodeLocal DNSCache feature, the node\-local\-dns add\-on must first be upgraded to v0.3.1 or later. For details, see [Add-on release record](https://docs.byteplus.com/en/docs/vke/node-local-dns).

* NodeLocal DNSCache requires the vpc\-cni add\-on v1.3.0 or later. For details, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/vpc-cni).

* After the node\-local\-dns add\-on is installed in the cluster and NodeLocal DNSCache is enabled, NodeLocal DNSCache takes effect only for newly created Pods.


<span id=".5a6J6KOFLW5vZGVsb2NhbC1kbnNjYWNoZQ=="></span>
## Prerequisites

The node\-local\-dns add\-on has been installed. For details, see [node-local-dns](https://docs.byteplus.com/en/docs/vke/node-local-dns-add-on).

<span id=".5Zyo5bqU55So5Lit5L2_55SoLW5vZGVsb2NhbC1kbnNjYWNoZQ=="></span>
## Application scenarios

<span id=".5L2_55So6Ieq5Yqo5rOo5YWl"></span>
### Scenario 1: Use automatic injection

After node\-local\-dns add\-on is installed, the newly created pods in a cluster will be injected with the dnsConfig settings by the system to enable access to NodeLocal DNSCache.

Except for the following types of pods:


* Pods belong to the kube\-system and kube\-public namespaces.

* Pods with namespaces or labels that contain `dns-config-injection=disable`.

* Pods that are running on hostNetwork and have DNSPolicy set to `ClusterFirstWithHostNet`, or those not running on hostNetwork and have DNSPolicy set to `ClusterFirst`.


Taking the pods with the default namespace as an example, the following dnsConfig settings are injected by the system.

```YAML
...
    dnsConfig:
        nameservers:
        - 169.254.20.10 
        - 10.0.10.1 
        options:
        - name: ndots
          value: "3"
        - name: attempts
          value: "2"
        - name: timeout
          value: "1"
        searches:
        - default.svc.cluster.local
        - svc.cluster.local
        - cluster.local
    dnsPolicy: None
...
```


To ensure maximum availability of DNS service, the ClusterIP address (10.0.10.1) of kube\-dns will also be added to the `nameservers` as a backup DNS server.

<span id=".56aB55So6Ieq5Yqo5rOo5YWl"></span>
### Scenario 2: Disable automatic injection

If necessary, you can disable NodeLocal DNSCache with the following methods.


<Tabs>
<Tab zoneid="GofekHUvXb" title="Namespace dimension">
<TabTitle>Namespace dimension</TabTitle>

Execute the following command to disable the dnsConfig setting for all newly created pods in the specified namespace.

```Bash
kubectl label namespace <namespace name> dns-config-injection=disable
```





</Tab>
<Tab zoneid="UnaFeMjgpo" title="Pod dimension">
<TabTitle>Pod dimension</TabTitle>

Add the following label to pods to disable their dnsConfig settings.

```YAML
···
  labels:
    dns-config-injection: disable
···
```





</Tab>
</Tabs>


<span id=".5omL5Yqo6YWN572u"></span>
### Scenario 3: Configure manually

You can configure NodeLocal DNSCache if the automatic injection does not meet your requirements. Procedure:


1. For how to disable automatic injection to pods, see [Disabli automatic injection](https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache#.56aB55So6Ieq5Yqo5rOo5YWl).

2. Manually configure NodeLocal DNSCache for pods. The following are example settings for the pods in the default namespace.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: nginx
   spec:
     containers:
     - image: nginx:latest
       name: container-0
     dnsPolicy: None
     dnsConfig:
       nameservers: ["169.254.20.10","172.21.0.10"] # DNS server IP addresses
       searches: # Complete domain names to be used when only partial domain names are found in requests
       - default.svc.cluster.local
       - svc.cluster.local
       - cluster.local
       options:
       - name: ndots # Metric to determine if a domain name is complete. If the number of dots in a domain name exceeds the value, DNS resolution starts immediately. If the number of dots in a domain name is less than the value, the domains under the searches are used accordingly to fulfill DNS resolution.
         value: "3"
       - name: attempts # Number of retry attempts when the DNS resolution fails
         value: "2"
       - name: timeout # Timeout for a single DNS resolution request, measured in seconds
         value: "1"
     imagePullSecrets:
     - name: default-secret
   ...
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also use kubelet with the <code>--cluster-dns</code> and <code>--cluster-domain</code> parameters to globally control pod dnsConfig. However, this is not a recommended method. If you find it necessary to use that method, you can submit a ticket for consultation.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [How do I determine if a node-local-dns add-on is used?](https://docs.byteplus.com/en/docs/vke/How-do-I-confirm-that-the-node-local-dns-add-on-is-used)
