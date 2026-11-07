---
title: "How It Works"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/dWyQcY"
---

BytePlus GTM resolves DNS queries from a client to an appropriate address. After receiving the DNS response, the client directly access the address in the DNS response. Therefore, client traffic does not pass through BytePlus GTM.

<span id="how-does-byteplus-gtm-route-user-requests"></span>
## How does BytePlus GTM route user requests

When receiving a DNS query from the client, BytePlus GTM returns a response to the DNS query based on factors such as geolocation, ISP, access latency, and IDC capacity. In this way, user requests are routed to appropriate addresses.

Assuming your domain is `example.com` with multiple public IP addresses, you have added these to BytePlus GTM. You have created a CNAME record in a DNS service provider, mapping `example.com` to the CNAME `example.com.byteplus.com`.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2472c01db5689fb16469568d0d3a8d44.jpeg) </span>

The steps of BytePlus GTM routing user requests at the DNS level are as follows:


1. The client sends a DNS query to the recursive DNS server to query the domain `example.com`.

2. The recursive DNS server finds the authoritative DNS server for the domain `example.com` and sends a DNS query to that server. The authoritative DNS server returns a CNAME record. This CNAME record points to the CNAME `example.com.byteplus.com`.

3. The recursive DNS server finds the authoritative DNS server for the CNAME `example.com.byteplus.com`. The authoritative DNS server for the CNAME is provided by BytePlus GTM. The recursive DNS server sends a DNS query to the authoritative DNS server to query the domain `example.com.byteplus.com`.

4. After receiving the DNS query, the authoritative DNS server of BytePlus GTM returns an A record containing the appropriate address, based on the policies configured in BytePlus GTM.

5. The authoritative DNS server of BytePlus GTM returns the A record containing the address to the recursive DNS server.

6. The recursive DNS server returns the A record to the client. Assuming the returned address is `203.0.113.1`.

7. The client establishes a connection directly with the address `203.0.113.1`. The traffic does not pass through BytePlus GTM.


<span id="how-does-byteplus-gtm-achieve-traffic-management"></span>
## How does BytePlus GTM achieve traffic management?

BytePlus GTM deploys DNS records to the authoritative DNS server, thus achieving traffic management. BytePlus GTM combines the following methods to achieve traffic management:


* Address management

* Routing user requests based on the source of the request

* Routing user requests based on load balancing configuration

* Routing user requests based on health checks and failover


BytePlus GTM provides different routing policies and routing modes.


* **Basic routing**: Routing policy based on geolocation. You can enable or disable weight\-based load balancing for the basic routing policy.

* **Intelligent routing**: Routing policy based on latency and capacity. Intelligent routing policy does not support weight\-based load balancing. You can set the intelligent routing policy to any of the following routing modes. Intelligent routing is only supported in the ultimate edition.

   * **Performance**: When receiving a DNS query from a user, BytePlus GTM returns the address with the lowest access latency for the user.

   * **Capacity**: When receiving a DNS query from a user, BytePlus GTM returns the address with the lowest access latency for the user, subject to the capacity limits of the address.


Regardless of the routing policy and routing mode, you can configure health check parameters and failover parameters. However, for automatically generated routing rules under the intelligent routing policy, you cannot manually configure failover parameters.

Overall, request routing in BytePlus GTM can be categorized as:


* Routing user requests based on the source of the request.

* Routing user requests based on load balancing configuration.

* Routing user requests based on health check and failover configuration.


<span id="address-management"></span>
### Address management

BytePlus GTM provides addresses, pools, traffic targets, pool sets, and rules to manage addresses.

<span id="basic-routing"></span>
#### Basic routing

If your GTM instance uses a basic routing policy, you need to configure addresses, pools, pool sets, and rules.


* **Address**: An address can be an IPv4 address, IPv6 address, or domain name. In actual business scenarios, an address can represent an IP address of an IDC, a CNAME of a load balancing service, or a CNAME of a CDN service.

* **Pool**: One or more addresses can be added to the same pool. Generally, addresses in the same pool have the same business attributes (such as geolocation and ISP). An address can be added to multiple pools.

* **Pool set**: One or more pools can be added to the same pool set. A pool can be added to multiple pool sets.

* **Rule**: A rule can contain one or more pool sets. Among them, only one pool set can serve as the primary pool set, while other pool sets can only serve as backup pool sets. A GTM instance can contain one or more rules. User requests are routed only to addresses within the primary pool set.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d186f31b2372c1d780bc2e7ba39ad50b.jpeg) </span>

<span id="intelligent-routing"></span>
#### Intelligent routing

If your GTM instance uses the intelligent routing policy, you need to configure addresses, pools, and traffic targets. You don't need to configure pool sets and rules because BytePlus GTM will automatically generate rules based on the pools you set as traffic targets.


* **Address**: An address can be an IPv4 address, IPv6 address, or domain name. In actual business scenarios, an address can represent an IP address of an IDC, a CNAME of a load balancing service, or a CNAME of a CDN service.

* **Pool**: One or more addresses can be added to the same pool. Generally, addresses in the same pool have the same business attributes (such as geolocation and ISP). An address can be added to multiple pools.

* **Traffic target**: Under the intelligent routing policy, BytePlus GTM automatically generates one or more pools required for rules.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_64c785b6245841bebea4dae322687c19.jpeg) </span>

<span id="routing-user-requests-based-on-the-source-of-the-request"></span>
### Routing user requests based on the source of the request

In BytePlus GTM, the source of user requests is defined by lines. Lines can be ISPs or geolocations.

<span id="basic-routing"></span>
#### Basic routing

In basic routing mode, you can configure lines for rules. BytePlus GTM will match an appropriate rule for user requests based on the lines.

In the example diagram below:


* User requests from Singapore will match the rule for the Singapore geolocation line, and then the requests will be routed to the pool associated with the rule. This pool contains the IP addresses used by the data center in Singapore.

* User requests from Japan will match the rule for the Japan geolocation line, and then the requests will be routed to the pool associated with the rule. This pool contains the IP addresses used by the data center in Japan.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_29f6da36e4d76255f864ac0f4fd68b4b.jpeg) </span>

<span id="intelligent-routing"></span>
#### Intelligent routing

In intelligent routing mode, BytePlus GTM can automatically detect the access latency from users to IDCs based on attributes such as the ISP and geolocation of the user's IP address. It then automatically routes user requests to the IDC data center with the lowest access latency. Therefore, you don't need to manually configure lines for rules.

<span id="routing-user-requests-based-on-load-balancing-configuration"></span>
### Routing user requests based on load balancing configuration

Load balancing configuration includes weight, capacity, and load. Only intelligent policy supports capacity and load. You can use the address management feature in combination with load balancing configuration to flexibly route user requests. The following table shows the load balancing parameters supported by addresses, pools, pool sets, and rules.


| |Weight |Capacity |
|---|---|---|
|Address |✅ |✅ |
|Pool |✅ |✅ |
|Pool set |❌ |❌ |
|Rule |✅ |❌ |



* ✅: Supported

* ❌: Not supported


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In a rule, only one pool set can be effective. Therefore, pool sets are not related to load balancing configuration.</div>


* <div data-tips="true" data-tips-type="tip">For GTM instances of the ultimate edition, you can set weights for associated pools within a pool set. If a pool is associated with multiple pool sets, you can set weights for that pool separately in different pool sets.</div>



<span id="basic-routing"></span>
#### Basic routing

In the basic routing policy, you can set weights for addresses, pools, and rules separately. The weight is a positive integer.


* **Rule weight**: Used to achieve load balancing among all rules matching the same line. Assuming the sum of weights of all rules is the total weight, and the total number of user requests allocated to all rules is the total number of user requests. When BytePlus GTM routes user requests, the proportion of user requests allocated to each rule to the total number of user requests equals the proportion of this rule's weight to the total weight.

* **Pool weight**: Used to achieve load balancing among all pools under a rule. Assuming the sum of weights of all pools under a rule is the total weight, and the total number of user requests allocated to all pools is the total number of user requests. When BytePlus GTM routes user requests, the proportion of user requests allocated to each pool to the total number of user requests equals the proportion of this pool's weight to the total weight.

* **Address weight**: Used to achieve load balancing among all addresses under a pool. Assuming the sum of weights of all addresses under a pool is the total weight, and the total number of user requests allocated to all addresses is the total number of user requests. When BytePlus GTM routes user requests, the proportion of user requests allocated to each address to the total number of user requests equals the proportion of this address's weight to the total weight.


For example, in the image below:


* Rule 1 and rule 2 receive 75% and 25% of user requests respectively.

* Pool 1 and pool 2 receive 75% and 25% of user requests from rule 1 respectively.

* Addresses `203.0.113.1` and `203.0.113.2` can receive 50% and 50% of user requests from pool 1 respectively.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f62e6c68633c270abd71b2f796557f2f.png) </span>

After BytePlus GTM deploys DNS records to authoritative DNS server, the authoritative DNS server will implement load balancing based on the Weighted Round Robin (WRR) algorithm according to the **actual weight** of each DNS record. BytePlus GTM calculates the **actual weight** of an address as follows:


1. Calculate the result of `weight of the rule to which the address belongs * weight of the pool to which the address belongs * address weight`.

2. Normalize the result calculated in the previous step to the range of [1, 1000].


<span id="intelligent-routing"></span>
#### Intelligent routing

In the intelligent routing policy, you can set capacity for addresses or pools in the capacity routing mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you create custom rules under the intelligent policy, the weights you set for custom rules will not take effect.</div>


<span id="capacity-routing-mode"></span>
##### Capacity routing mode

In the capacity routing mode, you can set capacity for addresses or pools. BytePlus GTM will return the address with the lowest user access latency while meeting the capacity limits of the address.

Capacity is a relative value. If you choose to set capacity for addresses, then the capacity of a pool is the sum of the capacities of all available addresses it contains. If you choose to set capacity for pools, BytePlus GTM will evenly distribute the capacity of the pool to each address.

Based on the capacity ratio of each address, BytePlus GTM routes the corresponding proportion of user requests to each address.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a367ab6d9a250a234212090e8e40c6b3.jpeg) </span>

<span id="routing-user-requests-based-on-health-checks-and-failover-configuration"></span>
### Routing user requests based on health checks and failover configuration

BytePlus GTM can perform regular health checks on addresses. Based on the health check results and your failover configuration, BytePlus GTM can:


* Perform automatic failover based on health check results.

* Send alarm notifications to remind you to perform manual failover.


<span id="health-checks"></span>
#### Health checks

BytePlus GTM can periodically initiate health checks to addresses through one or more health probes. The request type for health checks can be ICMP Ping, HTTP, HTTPS, or TCP. Based on the health check results, addresses are determined to be available or unavailable. You can set the time interval for health checks. The shorter the health check interval, the more quickly BytePlus GTM can detect unavailable addresses.

Each pool set has a **Pool set availability threshold** parameter, which indicates the minimum number of available addresses required for the pool set to be considered available. If a pool set contains fewer available addresses than the **Pool set availability threshold**, the pool set is determined to be unavailable.

The following table shows whether BytePlus GTM determines the availability of addresses, pools, and pool sets.


| |Detects availability? |
|---|---|
|Address |✅ |
|Pool |❌ |
|Pool set |✅ |



* ✅: Yes

* ❌: No


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Health check parameters can be configured in policies or rules.</div>



* <div data-tips="true" data-tips-type="tip">If the policy type of the GTM instance is basic routing:</div>


   * <div data-tips="true" data-tips-type="tip">Health check parameters can be configured in policies or rules.</div>


* <div data-tips="true" data-tips-type="tip">If the policy type of the GTM instance is intelligent routing:</div>


   * <div data-tips="true" data-tips-type="tip">If you haven't created custom rules, health check parameters can only be configured in policies.</div>


   * <div data-tips="true" data-tips-type="tip">If you have created custom rules, health check parameters can be configured in policies or custom rules.</div>



<div data-tips="true" data-tips-type="tip">A rule can inherit health check parameters from its parent policy or use custom health check parameters:</div>



* <div data-tips="true" data-tips-type="tip">If a rule inherits health check parameters from its parent policy, the policy's health check parameters take effect in the rule.</div>


* <div data-tips="true" data-tips-type="tip">If a rule uses custom health check parameters, the custom health check parameters take effect in that rule.</div>



<span id="automatic-failover"></span>
#### Automatic failover

BytePlus GTM performs automatic failover based on address availability. The failover logic is as follows:

<span id="failover-across-addresses"></span>
##### Failover across addresses

The failover logic across addresses is as follows:


* When an address becomes unavailable, BytePlus GTM removes that address from the domain's DNS records. After the updated DNS records take effect on a recursive DNS server, user requests using that recursive DNS server to obtain domain resolution results will no longer be routed to that address. BytePlus GTM will redistribute user requests among available addresses according to your load balancing configuration.

* When the address becomes available again, BytePlus GTM will include that address in the domain's DNS records again. After the updated DNS records take effect on a recursive DNS server, user requests using that recursive DNS server to obtain domain resolution results will be routed to that address again. BytePlus GTM will redistribute user requests among available addresses according to your load balancing configuration.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f393046540fe4cf401fb849f90b4c7f5.jpeg) </span>

<span id="failover-across-pool-sets"></span>
##### Failover across pool sets

In a rule, only one pool set can be active. All user requests matching this rule will be routed to addresses in the currently active pool set.

By default, the **Pool set active mode** parameter of a pool set is set to **Automatic**. When the primary pool set becomes unavailable, BytePlus GTM will transfer all user requests to another available pool set in the same rule, in order of pool set priority from high to low. If all pool sets are unavailable, BytePlus GTM will transfer user requests to the pool set with the highest priority. If a higher priority pool set becomes available again, BytePlus GTM will transfer user requests back to the higher priority pool set.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1a93ca4c91f34762fa35c503be2bf0d3.jpeg) </span>

<span id="manual-failover"></span>
#### Manual Failover

If you need to manually select an available pool set when the primary pool set becomes unavailable, you can set the **Pool set active mode** parameter of the pool set to **Manual**. In this mode, failover between addresses will still occur automatically, but failover between pool sets will no longer be automatic. To ensure you are promptly informed of pool set failures, you can create alarm strategies in BytePlus GTM and associate them with GTM instances. If a pool set becomes unavailable, BytePlus Cloud Monitor will send alarm notifications through your configured communication channels. After receiving the alarm notification, you can manually select an available pool set according to your disaster recovery plan.

In addition to the status of pool sets, you can monitor the status of GTM instances, rules, pool sets, pools, and target addresses through alarm strategies.
