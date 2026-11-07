---
title: "CoreDNS troubleshooting"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CoreDNS_troubleshooting"
---

CoreDNS is a core add\-on that provides DNS resolution capabilities within VKE clusters. It is applicable to scenarios such as Pods accessing Services, external domain names, and service discovery within clusters. This topic describes methods for diagnosing common CoreDNS failures and troubleshooting procedures, including DNS configuration checks, add\-on status checks, connectivity verification, log analysis, and network packet capture.

<span id="jkH1ugaq"></span>
## Background

<span id="JTaPGiQz"></span>
### Troubleshooting approach

The difficulty in troubleshooting CoreDNS often does not lie in the use of troubleshooting commands, but in failing to effectively categorize issues. If you treat all “resolution failures” as CoreDNS issues from the start, you are likely to repeatedly troubleshoot unrelated areas and may even resort to inefficient measures such as scale\-out or restart.

Before starting troubleshooting, we recommend confirming the following items:


1. Does the issue fall into one of the following categories: a non‑existent domain, a misconfigured domain, requests failing to reach the DNS server, or requests being sent but responses timing out?

2. Are the affected domain names in\-cluster domain names, out\-of\-cluster domain names, or domain names of a specific type?

3. Is the failure consistently reproducible, or does it only occur occasionally during peak hours, application releases, CoreDNS restarts, or node scaling?


During actual diagnosis, narrow down the scope layer by layer along the path: "business Pod → NodeLocal DNS or kube\-dns → CoreDNS → upstream DNS". Verify where the failure occurs and then use system features such as DNS service observability and node diagnosis to further determine whether the issue extends beyond CoreDNS and exists in node networks, upstream DNS, service forwarding, or client‑side configuration.

<span id="xSktneGH"></span>
### Quick failure diagnosis


|**Issue phenomenon** |**Common errors** |Possible cause |
|---|---|---|
|The domain name does not exist |`NXDOMAIN`, `no such host`, and `Name or service not known` |* The domain name is invalid.<br><br>* The namespace name is invalid.<br><br>* The Headless Service or Endpoints are abnormal.<br><br>* Upstream DNS resolution is missing. |
|Unable to connect to the DNS server |`i/o timeout`、`no servers could be reached` |* The Pod cannot connect to kube\-dns/node\-local\-dns.<br><br>* CoreDNS is abnormal.<br><br>* Upstream DNS is unreachable.<br><br>* Network policy, CNI, and security group issues. |
|Exceptions only occur during peak hours or occasional timeouts |High latency, occasional timeouts, and jitters during release periods |* The CoreDNS load is high.<br><br>* The DNS request is amplified.<br><br>* NodeLocal DNS does not take effect.<br><br>* Exceptions occur in IPVS + UDP sessions. |
|Only the external domain name is invalid. |In‑cluster Service domains can be resolved, but public and private domains fail to be resolved. |* Upstream DNS is abnormal.<br><br>* The egress path is abnormal.<br><br>* Exceptions occur in the node DNS.<br><br>* Exceptions occur in the forwarding configuration. |
|Only the resolution of in\-cluster domain names is abnormal |Internal domains such as "`kubernetes.default`" fail to be resolved |Exceptions occur in the CoreDNS, Service/Endpoints, API access, and Pod DNS configurations. |


<span id="RKQeatVm"></span>
### Typical failure scenarios

<span id="Zo6GwzWR"></span>
#### Capacity and request amplification

If the issue only occurs during peak hours, check whether DNS requests are significantly amplified due to client\-side behavior first. The following table describes typical scenarios.


|Typical failure scenarios |Scenario description |
|---|---|
|An external domain name does not use a fully qualified domain name (FQDN), triggering search concatenation. |Multiple search domains (such as `default.svc.cluster.local`, `svc.cluster.local`, and `cluster.local`) are configured in the `/etc/resolv.conf` in a Kubernetes Pod. If the domain name in the business code does not include a full suffix (for example, using "`login`" instead of "`login.example.com`"), the system treats it as an in\-cluster service name and appends each search domain in sequence to form FQDNs to query.<br><br>For example: A business Pod needs to access an external site, but the domain name written in the code is "`login`". In this case, the system first queries domains such as "`login.default.svc.cluster.local`" and "`login.svc.cluster.local`". It proceeds to the next step only after all queries fail. Under high concurrency, a single DNS resolution may escalate into multiple queries, significantly amplifying the request volume. |
|The default `ndots:5` setting causes a large number of invalid queries. |The `ndots` parameter defines a threshold for the number of dots in a domain name. If the queried name contains fewer dots than this value, the resolver will treat it as a relative name and append search domain names to it before attempting to query it as an absolute domain name. In Kubernetes, the default value of `ndots` is 5. This means that for an external domain name such as `www.example.com` (which contains only 2 dots), it will first be treated as a relative name, triggering a series of domain concatenation queries, all of which are destined to fail.<br><br>For example: A business Pod needs to frequently request `www.example.com`. When `ndots is set to 5`, it sequentially queries domain names such as `www.example.com.default.svc.cluster.local` and `www.example.com.svc.cluster.local`, `NXDOMAIN` is returned each time, and the actual `www.example.com` is finally queried. The original 1 query becomes 4 to 5 queries. |
|Excessive short\-lived connections, which cause each request to trigger a new DNS resolution. |If your business does not reuse connections (without connection pools) and lacks effective DNS caches either in the application or at the runtime level, it ends up with a pattern where every request triggers a new DNS resolution. Under high concurrency, the business QPS is roughly equal to the DNS QPS, which causes the processing load of CoreDNS to quickly increase and potentially hit its capacity limit.<br><br>For example, a business Pod initiates 50,000 requests per second to `payment.example.com`, each time creating a connection without any caching. As a result, about 50,000 DNS queries are generated per second, placing significant processing load on CoreDNS during peak hours. |
|Some base images or resolvers exhibit different behaviors that can further amplify the DNS request volume. |Different images use different resolver libraries (such as glibc, musl, and language‑runtime built‑in resolvers). These libraries differ in details such as cache policies, concurrent query merging (singleflight), IPv4/IPv6 query order (A/AAAA), and retries after timeouts. With the same business code, simply switching to a different base image or runtime version may lead to a significant increase in DNS query volume.<br><br>For example, the resolver in the old image instead of the new image merges a large number of concurrent resolutions occurring at the same time. This causes 10,000 concurrent requests to directly trigger 10,000 DNS resolutions. Alternatively, the resolver queries AAAA records first and then A records by default, but your business only uses IPv4. Therefore, each resolution generates 2 queries. |
|NodeLocal DNS is not enabled, or it is enabled, but the business does not point to the local cache. |NodeLocal DNS is used to provide a local DNS cache on each node. It allows the queries of Pods to preferentially hit the local cache, thereby reducing the centralized pressure on CoreDNS. However, if NodeLocal DNS is not deployed in the cluster, or if it is deployed but the nameserver of Pods still points to the ClusterIP of CoreDNS instead of the local address, the traffic will not be redirected to the local cache as expected.<br><br>For example, NodeLocal DNS is deployed in the cluster, but the `nameserver` entry in the `/etc/resolv.conf` configuration of some business Pods is still the CoreDNS Service IP. As a result, DNS requests will fail to hit the local cache. Those requests will still be sent to CoreDNS, and the local cache mechanism will not function as expected. |


You can enable [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability?lang=en) in the cluster and use the following metrics or dashboards to confirm whether capacity or request is amplified.


* core\-dns/node\-local\-dns request volume.

* Response latency and error code.

* Cache hit ratio.

* Upstream forwarding latency and failure rate.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In high‑QPS or high‑jitter scenarios, first evaluate the applicability and effectiveness of NodeLocal DNS. If CoreDNS still exhibits a clear capacity bottleneck, scale out CoreDNS and fine‑tune its parameters based on monitoring results.</div>


<span id="FpLqeOyL"></span>
#### IPVS + UDP occasional timeout

DNS queries typically use UDP. When kube\-proxy is running in IPVS mode, forwarding from a Service to its backend Pods relies on the UDP session and scheduling states maintained by IPVS. Therefore, as long as the session state persists, subsequent packets of the same type within a certain period may continue to be sent to the same backend, rather than reselecting a healthy backend for each new request.

When a CoreDNS Pod exits due to CoreDNS rolling updates, restarts, scale‑in, or node scaling, Kubernetes updates the endpoints, and kube‑proxy refreshes the IPVS backend list. However, this process is not instantaneously consistent across all nodes and all session states. Before the update is complete, previously established UDP session states may still point to the CoreDNS Pod that just exited. This results in a small number of requests being forwarded to unreachable backends during the window, which manifests as occasional DNS query timeouts.

To address this type of issue, the recommended approaches are as follows:


* Prioritize enabling NodeLocal DNS. It offloads DNS caching and forwarding to each local node, significantly reducing the proportion of business Pod requests that directly traverse the CoreDNS Service (the IPVS load‑balancing endpoint). Business Pod requests first hit the local NodeLocal cache. If the cache fails to be hit, NodeLocal forwards the requests to the upstream CoreDNS.

* Evaluate whether to adjust the IPVS UDP session persistence duration in kube\-proxy. Appropriately shortening the UDP session timeout can shorten the window during which "exited backends are pointed".


<span id="MSIBfEjQ"></span>
## Troubleshooting process

<span id="75JCpa0M"></span>
### Step 1: Confirm the scope of impact


1. Run the following command in the business Pod to test whether the Pod can resolve in\-cluster domain names and out\-of\-cluster domain names as expected.

   ```Bash
   nslookup kubernetes.default.svc.cluster.local
   nslookup example.com
   ```
   

   The expected result is as follows: under normal circumstances, the Pod can resolve in\-cluster domain names and out\-of\-cluster domain names as expected.

   ```Bash
   Server:         1xx.xxx.xxx.xxx
   Address:        1xx.xxx.xxx.xxx#53
   
   Name:   example.com
   Address: 1xx.xxx.xxx.xxx
   Name:   example.com
   Address: 1xx.xxx.xxx.xxx
   Name:   example.com
   Address: 1xx.xxx.xxx.xxx
   Name:   example.com
   Address: 1xx.xxx.xxx.xxx
   ```
   

   If the Pod cannot resolve domain names, record the following information in the test results:

   * Abnormal domain name.

   * Exception start time.

   * Whether the issue only affects a specific namespace, a certain type of node, or a particular app.

   * Whether the issue only occurs during the release, scaling, or node fluctuation period.

   * Typical error log.

2. (Optional) If no debugging tool exists in the business image, run the following command to create a Pod for debugging.

   ```Bash
   kubectl run -it --rm dns-debug \
     --image=nicolaka/netshoot \
     --restart=Never \
     -- sh
   ```
   


<span id="XuUVqTLw"></span>
### Step 2: Check the DNS configuration


1. Run the following command to view the `dnsPolicy` and `dnsConfig` configuration in the business Pod configuration. `${pod-name}` is the name of the business Pod, and `${namespace}` is the namespace where the business Pod is located.

   ```Bash
   kubectl get pod ${pod-name} -n ${namespace} -o yaml
   ```
   

   The expected output is as follows:

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     annotations:
       vke.volcengine.com/cello-pod-evict-policy: allow
   ...
   spec:
     containers:
     - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
       imagePullPolicy: IfNotPresent
       name: nginx
       ports:
       - containerPort: 80
         protocol: TCP
     dnsConfig:
       nameservers:
       - 1xx.xxx.xxx.xxx
       - 172.24.128.10
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
     dnsPolicy: ClusterFirst
   ...
   ```
   

   Pay special attention to the following items:

   * For normal Pods, the default DNS policy needs to be `ClusterFirst`, that is `dnsPolicy: ClusterFirst`.

   * If the `hostNetwork` parameter in the Pod is set to `true`, it means the Pod directly uses the network namespace of the node where it resides, instead of an independent Pod network. In this case, you need to explicitly configure `dnsPolicy: ClusterFirstWithHostNet`. Otherwise, the Pod will inherit the DNS configuration of the node, which results in failures in resolving cluster domain names such as `kubernetes.default.svc.cluster.local`.

   * If NodeLocal DNS is enabled in the cluster, confirm that `nameserver` actually points to the local cache address of the node, not just to CoreDNS.

   * Check whether the `search` and `ndots` settings are explicitly overridden, which results in unnecessary query amplification.

2. Run the following command to view the `/etc/resolv.conf` configuration of the business Pod. `${pod-name}` is the name of the business Pod, and `${namespace}` is the namespace where the business Pod is located.

   ```Bash
   kubectl exec -it ${pod-name} -n ${namespace} -- cat /etc/resolv.conf
   ```
   

   The expected result is as follows: Confirm that the DNS server used by the cluster Pod matches the configuration.

   ```Bash
   search default.svc.cluster.local svc.cluster.local cluster.local
   nameserver 1xx.xxx.xxx.xxx
   nameserver 172.24.128.10
   options timeout:1 ndots:3 attempts:2
   ```
   


<span id="GueTlPL3"></span>
### Step 3: Confirm the type of abnormal domain names


<Tabs>
<Tab zoneid="HfKZcN2rqf" title="Only in-cluster domain names are abnormal">
<TabTitle>Only in-cluster domain names are abnormal</TabTitle>

If only the resolution of in\-cluster domain names are abnormal, we recommend performing the following checks:


* Whether the kube\-dns Service exists and whether the ClusterIP functions as expected.

* Whether the CoreDNS Pod is in the `Running` or `Ready` state.

* Whether the Endpoints corresponding to the Service are complete.

* Whether the Service name, subdomain, and namespace of the Headless Service/StatefulSet match.


Recommended commands:

```Bash
kubectl -n kube-system get svc kube-dns
kubectl -n kube-system get endpoints kube-dns
kubectl -n kube-system get pods -o wide | egrep 'coredns|node-local-dns'
kubectl get svc,endpoints -n ${namespace} | grep ${service-name}
```





</Tab>
<Tab zoneid="JzRLlJEarl" title="Only the resolution of out-of-cluster domain names is abnormal">
<TabTitle>Only the resolution of out-of-cluster domain names is abnormal</TabTitle>

If only the resolution of in\-cluster domain names are abnormal, we recommend performing the following checks:


* Whether CoreDNS can forward queries to the upstream DNS server as expected.

* Check whether the upstream DNS is reachable or times out.

* Whether the DNS and egress path of the node function as expected.

* Whether the issue affects only certain nodes. If so, this suggests node‑specific network or route issues.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Common causes for such issues include: unreachable upstream DNS, node network exceptions, misconfigured VPC routes, security group or subnet ACL restrictions, or abnormal DNS settings on the node.</div>



</Tab>
<Tab zoneid="uMdLgfR59F" title="Only Headless Service/StatefulSet domain names are abnormal">
<TabTitle>Only Headless Service/StatefulSet domain names are abnormal</TabTitle>

If only Headless Service/StatefulSet domain names fail to be resolved, we recommend performing the following checks:


* Check whether the Service is configured with the `clusterIP: None` field.

* Check whether the corresponding Endpoints or EndpointSlice exists.

* Check whether the StatefulSet `serviceName` matches the Headless Service.

* Whether the client uses an invalid namespace or an incomplete domain name.


</Tab>
</Tabs>


<span id="IJLFiRR3"></span>
### Step 4: Check the status of the CoreDNS and NodeLocal add\-ons


1. Run the following command to check the status of the CoreDNS and NodeLocal DNS add\-ons in the cluster.

   ```Bash
   kubectl -n kube-system get pods -o wide | egrep 'coredns|node-local-dns'
   ```
   

   The expected result is as follows. Pay special attention to whether the following issues exist:

   * Whether the Pod restarts frequently.

   * Whether obvious OOM errors, probe failures, or configuration errors exist.

   * Whether NodeLocal DNS is missing or unhealthy on the affected node.

   ```Bash
   coredns-bcf4***                             1/1     Running     0               5h32m   192.168.2.82   192.168.2.77   <none>           <none>
   coredns-bcf4***                             1/1     Running     0               5h32m   192.168.2.78   192.168.2.77   <none>           <none>
   node-local-dns-5c***                        1/1     Running     0               5h12m   192.168.2.77   192.168.2.77   <none>           <none>
   node-local-dns-admission-86dd***            1/1     Running     1 (5h12m ago)   5h12m   192.168.2.89   192.168.2.77   <none>           <none>
   node-local-dns-admission-86dd***            1/1     Running     0               5h12m   192.168.2.90   192.168.2.77   <none>           <none>
   ```
   

2. Run the following command to check the resource usage of CoreDNS and NodeLocal DNS add\-ons.

   ```Bash
   kubectl -n kube-system top pod | egrep 'coredns|node-local-dns'
   ```
   

   The expected result is as follows: Check whether the CPU/memory of the Pods remains high when an issue occurs.

   ```Bash
   coredns-bcf4***                             2m           22Mi            
   coredns-bcf4***                             2m           22Mi            
   node-local-dns-5c***                        1m           11Mi            
   node-local-dns-admission-86dd***            1m           8Mi             
   node-local-dns-admission-86dd***            1m           7Mi   
   ```
   

3. For intermittent failures, run the following command to view add\-on logs and check whether the failures coincide with CoreDNS releases, scale‑in, or node scaling. `${coredns-pod-name}` is the Pod name of the CoreDNS add\-on, and `${node-local-dns-pod-name}` is the Pod name of the NodeLocal DNS add\-on.

   ```Bash
   kubectl -n kube-system logs --tail=200 ${coredns-pod-name}
   kubectl -n kube-system logs --tail=200 ${node-local-dns-pod-name}
   ```
   


<span id="jpjdY8G8"></span>
### Step 5: Enable DNS query logging

If Pod status, basic logs, and connectivity tests are insufficient to determine the root cause, temporarily enable CoreDNS query logging to observe whether requests actually reach CoreDNS, what domains are queried, what response codes are, and whether latency is abnormal. For example:


* Suspect the actual queried domain by the client differs from the expected domain due to `search`/`ndots` amplification.

* Suspect a certain type of domain returns `NXDOMAIN` or `SERVFAIL`, but business logs are incomplete.

* Suspect that the request has reached CoreDNS, but an issue occurs during either upstream forwarding or response delivery.

* You need to determine whether the intermittent exception is caused by requests failing to reach CoreDNS or by requests that reach CoreDNS but fail to be processed.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">We recommend temporarily enabling the log plugin in the CoreDNS Corefile and raising the log level to debug for more detailed observation if necessary. After the issue is identified, disable the plugin to prevent it from collecting additional logs and generating additional performance overhead.</div>



1. Run the following command to edit the CoreDNS configuration.

   ```Bash
   kubectl -n kube-system edit configmap coredns
   ```
   

2. In the Corefile configuration, set the log level to log. Raise the level to debug if necessary.

   ```Bash
   # Please edit the object below. Lines beginning with a '#' will be ignored,
   # and an empty file will abort the edit. If an error occurs while saving this file will be
   # reopened with the relevant failures.
   #
   apiVersion: v1
   data:
     Corefile: |
       .:53 {
           log # Change the log level to log, and raise the level to debug if necessary.
           health {
              lameduck 5s
           }
           ready
           kubernetes cluster.local in-addr.arpa ip6.arpa {
              pods insecure
              fallthrough in-addr.arpa ip6.arpa
              ttl 30
           }
           prometheus :9153
           forward . /etc/resolv.conf {
              max_concurrent 10000
           }
           cache 30
           loop
           reload
           loadbalance
       }
   kind: ConfigMap
   metadata:
     annotations:
       meta.helm.sh/release-name: core-dns
       meta.helm.sh/release-namespace: kube-system
     creationTimestamp: "2026-08-11T02:59:18Z"
     labels:
       app.kubernetes.io/managed-by: Helm
     name: coredns
     namespace: kube-system
     resourceVersion: "487"
     uid: b21a3f9b-921***
   ```
   

3. After the configuration change, wait for the configuration to reload and take effect, and then run the following command to view CoreDNS logs. `${coredns-pod-name}` is the Pod name of the CoreDNS add\-on.

   ```Bash
   kubectl -n kube-system logs --tail=200 -f ${coredns-pod-name}
   ```
   

   Pay special attention to the following items:

   * Whether the query logs for the problematic requests can be viewed.

   * Whether the actual queried names match expectations, and whether a large number of invalid queries caused by search concatenation exist.

   * Whether the response code is `NOERROR`, `NXDOMAIN`, or `SERVFAIL`.

   * Whether obvious upstream forwarding latencies, retries, or errors are concentrated on a certain type of domain.

   Common failures and troubleshooting approaches:

   * If the business side reports errors, but the corresponding queries are completely absent from CoreDNS logs, suspect that requests do not reach CoreDNS and focus on the path from the Pod to kube\-dns/NodeLocal DNS.

   * If a large number of unexpected queried names are displayed, first check the client‑side domain name format as well as the `search` and `ndots` settings.

   * If queries reach CoreDNS but fail during upstream forwarding in most cases, first check upstream DNS reachability and external DNS resolution paths.

   * If slow queries or error accumulation only exist in specific replicas, check single‑Pod hotspots, UDP packet loss, or node‑side networking first.


<span id="cwgubTgj"></span>
### Step 6: Check the connectivity from the business Pod to the DNS add\-on


1. Run the following command to obtain the kube\-dns Service IP and Pod IP.

   ```Bash
   kubectl -n kube-system get svc kube-dns
   kubectl -n kube-system get pod -o wide | grep coredns
   ```
   

2. Perform layered verification in the business Pod or debugging Pod.

   ```Bash
   dig kubernetes.default.svc.cluster.local @${kube-dns-cluster-ip}
   dig kubernetes.default.svc.cluster.local @${coredns-pod-ip}
   dig example.com @${kube-dns-cluster-ip}
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If NodeLocal DNS is enabled, we recommend testing directly against the local cache address.   </div>
   

   The expected output is as follows:

   ```Bash
   ; <<>> DiG 9.16.50-Debian <<>> kubernetes.default.svc.cluster.local @172.24.128.10
   ;; global options: +cmd
   ;; Got answer:
   ;; WARNING: .local is reserved for Multicast DNS
   ;; You are currently testing what happens when an mDNS query is leaked to DNS
   ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27832
   ;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
   ;; WARNING: recursion requested but not available
   
   ;; OPT PSEUDOSECTION:
   ; EDNS: version: 0, flags:; udp: 4096
   ; COOKIE: 96ed91ee1a746219 (echoed)
   ;; QUESTION SECTION:
   ;kubernetes.default.svc.cluster.local. IN A
   
   ;; ANSWER SECTION:
   kubernetes.default.svc.cluster.local. 30 IN A   172.24.128.1
   
   ;; Query time: 1 msec
   ;; SERVER: 172.24.128.10#53(172.24.128.10)
   ;; WHEN: Tue Aug 11 08:52:43 UTC 2026
   ;; MSG SIZE  rcvd: 129
   ```
   

   Possible issues and causes during verification:

   * The Pod cannot access kube\-dns: Check Service forwarding, kube\-proxy, network policies, or CNI first.

   * The Pod can access the CoreDNS Pod but cannot access kube\-dns: Check Service/forwarding tables first.

   * Internal domain resolution works, but external domain resolution times out: Check the upstream DNS or egress path.


<span id="sPLdnZ3v"></span>
### Step 7: Use observability and diagnosis

When troubleshooting has narrowed down to the node or network layer, we recommend using the following system features:


* Enable [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability?lang=en): View the request, latency, error, and cache metrics of core\-dns and node\-local\-dns.

* Use [node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis?lang=en): Confirm node DNS resolution, node load, network exception, and CNI status.

* Manage add\-ons: Confirm whether core\-dns and node\-local\-dns are installed and whether the versions meet expectations.


If the final evidence indicates that the issue exists in the node network, VPC\-CNI, route, or security group, subsequent troubleshooting needs to shift away from CoreDNS.

<span id="szlTHYrh"></span>
### Step 8: Use the network packet capture feature

If the add\-on status, query logs, connectivity verification, and observability diagnostics in the preceding steps still cannot determine the root cause or the failed link, we recommend using the packet capture feature to confirm whether DNS requests are sent, whether they reach CoreDNS, whether responses are returned, and where the failure or exception occurs.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Monitoring center** \> **Packet capture** to perform packet capture separately for the client and the server.

   * Client: Business Pod encountering DNS exceptions.

   * Server: The corresponding CoreDNS Pod.


When you capture packets, we recommend narrowing down the scope as much as possible and focusing on DNS resolution packets. This prevents excessive unrelated traffic that may affect analysis efficiency. Pay special attention to the following items:


* Whether the client actually sends a DNS request.

* Whether the CoreDNS Pod receives the corresponding UDP/TCP 53 packet.

* Whether CoreDNS returns a resolution response.

* Whether requests and responses only appear on one side. The typical indicators are mid\-path packet drop, forwarding exception, or response delivery failure.


Diagnosis method:


* If requests are sent from the client but the CoreDNS Pod does not receive the packets, check for a link issue from the client to CoreDNS first.

* If the CoreDNS Pod receives requests but does not respond as expected, check CoreDNS, upstream forwarding, or the UDP receive path within the Pod first.

* If the CoreDNS Pod already sends a response but the client does not receive it, check for the return path, node network, conntrack, or Service forwarding issues first.


<span id="3OOmJW5Q"></span>
## Typical failures

<span id="inKEoXsG"></span>
### Example 1: The node conntrack table is full, resulting in DNS resolution failures and CoreDNS health check failures.

<span id="GtdeKzU7"></span>
#### Issue phenomenon


* Business Pods on the same node simultaneously encounter DNS timeouts, with errors mostly being "`i/o timeout`" and "`no servers could be reached`".

* Access to both the kube\-dns service and the CoreDNS Pod IPs may become unstable.

* CoreDNS Pods have low CPU and memory usage, but probe failures, restarts, or repeated Ready state flapping in a short period may occur.

* The issue often occurs during sudden connection spikes, short\-lived connection storms, high node load, or concentrated business bursts on the node.


The possible cause is that after the nf_conntrack table of the node is full, new connection tracking entries cannot be created. As a result, UDP requests sent from business Pods to DNS are dropped. In addition, health check requests from kubelet on the node to CoreDNS Pods may also time out, causing CoreDNS to be marked as unhealthy.

<span id="62FZ623n"></span>
#### Troubleshooting method

```Bash
# Check conntrack usage on the node.
sysctl net.netfilter.nf_conntrack_count
sysctl net.netfilter.nf_conntrack_max

# Check the kernel logs of the node for traces of full tables.
dmesg | grep -i conntrack

# View whether CoreDNS has probe failures or restarts
kubectl -n kube-system describe pod <coredns-pod-name>
kubectl -n kube-system get pod -o wide | grep coredns
```


If logs similar to "`nf_conntrack: table full, dropping packet`" are observed, and the abnormal period coincides with DNS timeouts and CoreDNS probe failures, the issue can generally be narrowed down to conntrack table capacity.

<span id="pAFxrAAE"></span>
#### Handling suggestions


* Relieve node connection pressure first, and check for abnormal short\-lived connections or ineffective DNS amplification.

* Evaluate enabling NodeLocal DNS to reduce cross\-node access and some conntrack pressure.

* Evaluate whether to adjust `nf_conntrack_max` based on the node specification and connection scale.

* If only a small number of hotspot nodes are abnormal, we recommend distributing workloads or scaling out nodes first, rather than simply increasing the number of CoreDNS replicas.


<span id="rPyS1mn2"></span>
### Example 2: CoreDNS Pod UDP receive buffer is insufficient, causing buffer overflow and packet loss

<span id="ohj2vhmf"></span>
#### Issue phenomenon


* The CoreDNS Pod is in the `Running` state, and CPU utilization may not necessarily reach the upper limit, but obvious DNS timeouts may still occur on the business side.

* Timeouts mainly occur in UDP queries. Switching to TCP queries or retries results in a higher success rate.

* The issue is more likely to occur in scenarios with sudden high QPS, concentrated single\-Pod pressure, or large and quickly returned upstream response packets.

* CoreDNS logs may not directly report "`buffer overflow`", and if such packet loss occurs within the network namespace of the CoreDNS Pod or socket buffer, node\-level UDP statistics may not directly reflect this exception.


In this scenario, the bottleneck may not lie in CoreDNS logic processing, but rather in the UDP receive queue of the DNS socket within the CoreDNS Pod or the packet receive path of its network namespace. As a result, packets have been delivered to the Pod but cannot be read by the application in time, leading to packet loss and timeouts.

<span id="nuTreciQ"></span>
#### Troubleshooting method

```Bash
# Check whether an obvious single-Pod hotspot exists in CoreDNS replicas.
kubectl -n kube-system top pod | grep coredns

# Nsenter into the network namespace of the CoreDNS process on the node.
# Check the node where the CoreDNS Pod is located first.
kubectl -n kube-system get pod <coredns-pod-name> -o wide

# After logging in to the node, first find the CoreDNS container via the Pod sandbox and then obtain the container PID.
crictl pods | grep <coredns-pod-name>
crictl ps --pod <pod-sandbox-id>
crictl inspect <coredns-container-id> | grep '"pid"'
nsenter -t <coredns-container-pid> -n

# After entering the namespace, run UDP/socket statistics.
netstat -su
ss -u -n -a -i | grep ':53'
```


Pay special attention to and check the following items:


* "`packet receive errors`" and "`receive buffer errors`" continuously increase.

* A specific CoreDNS Pod may encounter more obvious exceptions, but other Pods on the same node or other CoreDNS replicas do not necessarily exhibit the same symptoms simultaneously.

* If switching queries from UDP to TCP significantly improves the success rate, it suggests the issue lies in the UDP packet receive path rather than the domain being nonexistent.


<span id="e5koKstT"></span>
#### Handling suggestions


* Check for single\-Pod hotspots or uneven load distribution first. Increase the number of replicas and ensure a more even distribution of traffic if necessary.

* Reduce ineffective DNS queries and traffic spikes first, rather than attributing the issue solely to the server\-side buffer.

* Review node\-level network stack parameters to evaluate whether UDP buffer configurations are too small.

* For high\-QPS scenarios, evaluate NodeLocal DNS first to intercept and cache requests on the node side as much as possible.


<span id="a1wmmoIm"></span>
### Example 3: Only out\-of\-cluster domain name resolution is abnormal

<span id="t080bV1a"></span>
#### Issue phenomenon


* In\-cluster domain names, such as kubernetes.default.svc.cluster.local, are resolved as expected.

* Only public domain names, private authoritative domain names, or other out\-of\-cluster domain names fail to be resolved.

* In the CoreDNS query logs, you can see that the request has arrived, but responses are SERVFAIL, timeouts, or significantly high upstream forwarding latency.


This type of issue usually indicates that in\-cluster service discovery of CoreDNS functions as expected. The root cause is more likely the upstream DNS server, the egress path, or issues with the DNS resolution result of external domains.

<span id="v86S8mR9"></span>
#### Troubleshooting method

If CoreDNS query logging is not enabled, first temporarily enable the log plugin by performing the "enabling DNS query logging for assisting troubleshooting if necessary" step before viewing the request logs.

```Bash
# Check whether an obvious single-Pod hotspot exists among CoreDNS replicas.
kubectl -n kube-system top pod | grep coredns

# Nsenter into the network namespace of the CoreDNS process on the node.
# Check the node where the CoreDNS Pod is located first.
kubectl -n kube-system get pod <coredns-pod-name> -o wide

# After logging in to the node, first find the CoreDNS container via the Pod sandbox and then obtain the container PID.
crictl pods | grep <coredns-pod-name>
crictl ps --pod <pod-sandbox-id>
crictl inspect <coredns-container-id> | grep '"pid"'
nsenter -t <coredns-container-pid> -n

# After entering the namespace, run UDP/socket statistics.
netstat -su
ss -u -n -a -i | grep ':53'
```


Pay special attention to and check the following items:


* Whether CoreDNS receives the request.

* Whether the response code is NOERROR, NXDOMAIN, or SERVFAIL.

* Whether the upstream DNS times out or the result is abnormal.

* Whether only a certain type of external domain name is affected, rather than all external domain names.


<span id="kcuqdfWY"></span>
#### Handling suggestions


* If the upstream DNS returns an abnormal result, first check the configuration of the external domain name or the upstream resolution path.

* If CoreDNS cannot connect to the upstream DNS, first check the node outbound network, VPC route, security group, or subnet ACL.

* If only a small number of external domain names are abnormal, avoid misjudging it as an overall CoreDNS fault.


<span id="NNJppotN"></span>
### Example 4: Security group or subnet ACL misconfiguration blocks DNS traffic

<span id="fDj0HD1p"></span>
#### Issue phenomenon


* Business Pods on some or all nodes encounter persistent DNS resolution failures.

* dig @<kube\-dns\-cluster\-ip\> and dig @<coredns\-pod\-ip\> may both time out.

* The CoreDNS Pod may be healthy, but the client does not receive a response.

* This often occurs after security group, subnet ACL, or network access policy adjustments.


Typical scenario: Access control policies on nodes, Pods, or related subnets block UDP port 53 traffic, causing packets from business Pods to CoreDNS, or from CoreDNS to upstream DNS, to be dropped midway.

<span id="TqjO1u3S"></span>
#### Troubleshooting method

```Bash
# First, verify from the business Pod side whether DNS queries to kube-dns/CoreDNS time out.
dig <domain> @<kube-dns-cluster-ip>
dig <domain> @<coredns-pod-ip>
```


Pay special attention to and check the following items:


* Whether the issue exists only in part of the nodes. It is more likely attributable to network policies or subnet\-level blocking.

* Whether security groups, subnet ACLs, network policies, or firewall configurations have been changed recently.

* Whether UDP 53 is explicitly denied. Check TCP 53 if necessary.


<span id="3itIL2hx"></span>
#### Handling suggestions


* Restore or allow UDP/TCP 53 communication required from business Pods to CoreDNS and from CoreDNS to upstream DNS.

* If the issue only occurs in a small number of nodes or subnets, narrow down the investigation by node/subnet dimension.


<span id="3A1oRFPm"></span>
### Example 5: High CoreDNS Pod load causes resolution timeouts during peak hours

<span id="meouTGnW"></span>
#### Issue phenomenon


* The exception mainly occurs during business peak hours.

* The kubectl top pod indicates that the CPU or memory usage of a CoreDNS replica is approaching its resource limit, or that the usage of one replica is significantly higher than the others.

* The DNS query latency and timeout ratio increase, but the issue is resolved during off\-peak hours.


This situation is usually not a configuration error, but rather CoreDNS is handling excessive requests or the load is unevenly distributed, causing individual replicas to reach the upper limit first.

<span id="acrklNaS"></span>
#### Troubleshooting method

```Plain Text
kubectl -n kube-system top pod | grep coredns
kubectl -n kube-system get pod -o wide | grep coredns
```


Pay special attention to and check the following items:


* Whether all replicas approach the resource upper limit.

* Whether a single\-Pod hotspot exists, which indicates uneven load distribution.

* Whether the exception coincides with business traffic spikes, releases, or cache hit ratio decreases.


<span id="zZFfcJB4"></span>
#### Handling suggestions


* Investigate request amplification issues first, such as those caused by search/ndots configurations, short\-lived connections, or ineffective external queries.

* For high\-QPS scenarios, evaluate NodeLocal DNS first to reduce traffic that is directly routed to the CoreDNS Service.

* If a capacity bottleneck is confirmed, increase replicas or adjust resource specifications based on monitoring results.


<span id="xgAJH3BT"></span>
### Example 6: Concurrent A and AAAA record resolution failures

<span id="6ymozpar"></span>
#### Common symptoms


* The issue occurs at a low frequency, but sporadic timeouts recur persistently.

* The same domain name occasionally fails to resolve, but this issue resolves after a retry.

* This tends to occur more often in clients that request both A and AAAA records simultaneously, with certain base images, or on earlier kernel versions.


Such issues are usually related to client resolver behavior and kernel UDP/conntrack processing details, rather than CoreDNS being unavailable. A typical scenario is the client concurrently initiating both A and AAAA queries, triggering source port conflicts or packet loss. This ultimately manifests as low\-probability DNS timeouts.

<span id="dDttdLm9"></span>
#### Troubleshooting method

```Bash
# In the problematic Pod, test A and AAAA queries separately.
dig <domain> A
dig <domain> AAAA
```


Pay special attention to and check the following items:


* Whether the issue is more reproducible only with dual\-stack queries or on certain images.

* Whether the issue is related to Alpine/musl, earlier kernel versions, or non‑standard resolver implementations.

* Whether querying A or AAAA records separately results in noticeably higher stability.


<span id="orhNxsQp"></span>
#### Handling suggestions


* Confirm whether the business requires AAAA queries first to avoid unnecessary concurrent resolution.

* For DNS\-sensitive business, validate the base image and resolver behavior first, and adjust the image or runtime if necessary.

* If node‑level conntrack pressure or UDP packet loss is also observed, then the conntrack table and UDP buffer settings as mentioned earlier need to be investigated together as part of the root cause analysis.


<span id="xasP0itm"></span>
## Common command list


|Common commands |Usage instructions |
|---|---|
|`kubectl exec -it <pod-name> -n <namespace> -- cat /etc/resolv.conf` |View the DNS configuration in the Pod. |
|`kubectl -n kube-system get svc kube-dns`<br><br>`kubectl -n kube-system get endpoints kube-dns` |View the Service and Endpoints information of the kube\-dns add\-on. |
|`kubectl -n kube-system get pods -o wide \| egrep 'coredns\|node-local-dns'`<br><br>`kubectl -n kube-system top pod \| egrep 'coredns\|node-local-dns'` |View the status of the CoreDNS or NodeLocal DNS add\-on. |
|`kubectl -n kube-system logs --tail=200 ${coredns-pod-name}`<br><br>`kubectl -n kube-system logs --tail=200 ${node-local-dns-pod-name}` |View the logs of the specified add\-on. |
|`dig kubernetes.default.svc.cluster.local ${kube-dns-cluster-ip}`<br><br>`dig example.com ${kube-dns-cluster-ip}`<br><br>`dig example.com ${node-local-dns-ip}` |Perform targeted query tests in the business Pod or debugging Pod. |
