---
title: "Configure a GTM Instance"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/0_OA55"
---

This document describes how to configure a GTM instance you create in BytePlus GTM.

<span id="prerequisites"></span>
## Prerequisites

Before configuring the GTM instance, you must [create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/k_FIn3).

<span id="steps"></span>
## Steps

You need to follow these steps to configure the GTM instance:


* [Step 1: Configure the basic information](https://docs.byteplus.com/en/docs/36/20654#base_config): Set the policy type of the GTM instance, TTL for DNS records, remarks, and other information.

* Step 2: [Add pools or traffic targets to the GTM instance](https://docs.byteplus.com/en/docs/36/20654#address-pools):

   *  **(Basic routing only)**  [Add pool](https://docs.byteplus.com/en/docs/36/20654#pool): Add one or more pools to the GTM instance.

   *  **(Intelligent routing only)**  [Add traffic target](https://docs.byteplus.com/en/docs/36/20654#target): Add one or more traffic targets to the GTM instance. Intelligent routing is only supported by the ultimate edition.

* [Step 3: Enable health checks](https://docs.byteplus.com/en/docs/36/20654#health_config): Configure health check parameters. If health checks are enabled, BytePlus GTM performs periodical health checks on all addresses based on the health check parameters you set. If an address is considered unavailable, BytePlus GTM does not direct user requests to the address. BytePlus GTM automatically redirects user requests back to the address if the address becomes available again in subsequent health checks.

* [Step 4: Configure policy](https://docs.byteplus.com/en/docs/36/20654#route_config):  **(Basic routing only)**  Configure the policy you select in Step 1.

* [Step 5: Verify traffic and start routing](https://docs.byteplus.com/en/docs/36/20654#start): After the GTM instance configuration is complete, choose whether to automatically start routing.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9bf1c0b5d0628367c7a4f191ffc42bcd.jpeg) </span>

&nbsp;

<span id="step-1-configure-the-basic-information"></span>
### Step 1: Configure the basic information

Find the GTM instance you created on the BytePlus GTM [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances). In the **Actions** column, click **Configure**. On the **Instance configuration** page, find the **Basic information** section and configure the basic information of the GTM instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you have selected intelligent routing, the console hides the rule, pool, and weight settings for addresses. For BytePlus GTM to distribute user requests based on the addresses' traffic capacity, you can choose capacity routing mode.</div>



|Parameter |Description |
|---|---|
|**Policy type** |The policy type of the GTM instance.<br><br><br>* **Basic routing**: Traffic routing policy based on geolocation and weight. BytePlus GTM resolves the routing domain to an IP address that match the ISP and geographical information of the user's IP address.<br><br>* **Intelligent routing**: Traffic routing policy based on latency or capacity. BytePlus GTM resolves the routing domain to an IP address that meets the latency or capacity requirements.<br><br>&nbsp;<br><br>   Only GTM instances with the ultimate edition support intelligent routing. |
|**Routing mode** | **(Intelligent routing only)**  The routing mode for the intelligent policy.<br><br><br>* **Performance**: Routing mode based on latency. BytePlus GTM will return the IP address with the lowest access latency.<br><br>* **Capacity**: Routing mode based on capacity. BytePlus GTM will return the IP address with the lowest access latency, on the premise of meeting the capacity limits of the IP addresses. |
|**Load balancing** | **(Basic routing only)**  Whether to enable load balancing for basic policy.<br><br><br>* **Enable**: First, BytePlus GTM routes user requests to the nearest access point IP address under the same ISP. Then, BytePlus GTM distributes user traffic proportionally to multiple data centers based on weights. Suitable for scenarios where multiple data centers provide services at the same time, each has multiple access point IP addresses that belong to different ISPs, the distances between data centers are significant, and the capacity of each data center varies considerably.<br><br>* **Disable**: BytePlus GTM routes user requests to the nearest data center under the same ISP. Suitable for scenarios where multiple data centers provide services at the same time, each has multiple access point IP addresses that belong to different ISPs, the distances between data centers are significant, and the capacities of each data center are not significantly different. |
|**TTL** |This is the time you want DNS records to expire in the cache of recursive DNS servers. BytePlus GTM deploys DNS records to authoritative DNS servers. Recursive DNS servers obtain DNS records from the authoritative DNS server. The lower the TTL, the more frequently recursive DNS servers obtain DNS records from the authoritative DNS server, allowing changes to DNS records to take effect in a shorter time. For example, if you want DNS\-based failover to take effect in a shorter time, you can set the TTL to a lower value. |
|**Remark** |Remark for the GTM instance. |


After configuring, click **Next**.

&nbsp;

<span id="step-2-add-pool-or-traffic-targets"></span>
### Step 2: Add pool or traffic targets

&nbsp;

<span id="adding-an-pool-basic-routing-only"></span>
#### Adding an pool (Basic routing only)

On the **Add pool** page, click **Add pool** to add one or multiple pools. You need to set the following parameters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also skip this step. After configuring your GTM instance, you can add pools to your GTM instance. See <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ">Create a Pool</a>.</div>


**Basic information**


|Parameter |Description |
|---|---|
|**Name** |The name of the pool. UTF\-8 encoded. Maximum length is 64 UTF\-8 characters. |
|**Remark** |Remark for the pool. Defaults to an empty string. UTF\-8 encoded. Maximum length is 128 UTF\-8 characters. |
|**Address type** |The type of address in the pool.<br><br><br>* **IPv4**: Use IPv4 addresses as addresses.<br><br>* **IPv6**: Use IPv6 addresses as addresses.<br><br>* **Domain name**: Use domain names as addresses. |


Click **Add address** to add one or multiple addresses.

**Address**


|Parameter |Description |
|---|---|
|**Address** |The address within the pool. Depending on the type of address you choose, this can be set to an IPv4 address, IPv6 address, or a domain name. |
|**Weight** |The weight of the address. Weight is a positive integer, with the range of values referred to in [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/8cqTK1). BytePlus GTM routes user requests in proportion to the weights of the addresses. If **Load Balancing** was not enabled when configuring the GTM instance or in the **Common configuration** of the policy, this parameter does not appear. |
|**Address geolocation** |The geolocation of the address. If your GTM instance uses intelligent routing, BytePlus GTM routes user requests to the address with the lowest latency based on the user's geolocation and the address's geolocation.<br><br><br>* If the address type is IPv4 or IPv6, BytePlus GTM automatically determines the geolocation based on the address. If you need to customize the geolocation, you can modify it on your own.<br><br>* If the address type is a domain name, BytePlus GTM does not automatically determine the geolocation. You can set the IP address's geolocation on your own. |
|**Address availability mode** |The rule for determining whether the address is available.<br><br><br>* **Automatic**: BytePlus GTM determines whether the address is online based on health check results. An address is unavailable if the health check fails. If health checks are turned off, then the address is always available.<br><br>* **Always available**: The address is always available. BytePlus GTM does not perform health checks on this address.<br><br>* **Always unavailable**: The address is always unavailable. BytePlus GTM does not perform health checks on this address. |


After setting up, click **Next**.

&nbsp;

<span id="add-traffic-targets-intelligent-routing-only"></span>
#### Add traffic targets (Intelligent routing only)

On the **Add traffic targets** page, add one or multiple traffic targets. See [Set Traffic Targets for Intelligent Policy](https://docs.byteplus.com/docs/byteplus-dns-suite/c7KpPz). You need to set the following parameters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also skip this step. After configuring your GTM instance, you can add pools to your GTM instance. See <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ">Create a Pool</a>. Then you set your added pools as traffic targets. See <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/c7KpPz">Set Traffic Targets for Intelligent Policy</a>.</div>


**Basic information**


|Parameter |Description |
|---|---|
|**Name** |The name of the pool. UTF\-8 encoded. Maximum length is 64 UTF\-8 characters. |
|**Remark** |Remark for the pool. Defaults to an empty string. UTF\-8 encoded. Maximum length is 128 UTF\-8 characters. |
|**Address type** |The type of address in the pool.<br><br><br>* **IPv4**: Use IPv4 addresses as addresses.<br><br>* **IPv6**: Use IPv6 addresses as addresses.<br><br>* **Domain name**: Use domain names as addresses. |
|**Capacity** |The capacity of the pool. This parameter is read\-only and equals the sum of the capacity of all addresses within the pool. If you have not selected capacity routing mode, this parameter does not appear.<br><br>Capacity is a positive integer that indicates the traffic capacity of the pool or address. You can set a reasonable capacity value for your data center based on parameters such as bandwidth and concurrent connections. Capacity is a relative value, therefore you don't need to enter actual data like bandwidth or concurrent connections of the data center, but you need to ensure that different addresses or pools use a consistent unit of capacity. |
|**Set as traffic target** |Whether to set this pool as a traffic target. After configuring your GTM instance, you can refer to [Set Traffic Targets for Intelligent Policy](https://docs.byteplus.com/docs/byteplus-dns-suite/c7KpPz) to learn how to update your traffic targets.<br><br><br>* **Yes**: (Default) Set this pool as a traffic target.<br><br>* **No**: Do not set this pool as a traffic target. |


**Address**


|Parameter |Description |
|---|---|
|**Address** |Target address in the pool. Depending on the type of address you select, you can set it to an IPv4 address, IPv6 address, or a domain name. |
|**Address geolocation** |The geolocation of the address. If your GTM instance uses intelligent routing, BytePlus GTM routes user requests to the address with the lowest latency based on the user's geolocation and the address's geolocation.<br><br><br>* If the address type is IPv4 or IPv6, BytePlus GTM automatically determines the geolocation based on the address. If you need to customize the geolocation, you can modify it on your own.<br><br>* If the address type is a domain name, BytePlus GTM does not automatically determine the geolocation. You can set the IP address's geolocation on your own. |
|**Address availability mode** |The rule for determining whether the address is available.<br><br><br>* **Automatic**: BytePlus GTM determines whether the address is online based on health check results. An address is unavailable if the health check fails. If health checks are turned off, then the address is always available.<br><br>* **Always available**: The address is always available. BytePlus GTM does not perform health checks on this address.<br><br>* **Always unavailable**: The address is always unavailable. BytePlus GTM does not perform health checks on this address. |
|**Address capacity** |The capacity of the address. Capacity is a positive integer that indicates the traffic capacity of the address, with a range of [1, 100000]. BytePlus GTM will judge the traffic capacity of different addresses based on the proportion of their capacities. For example, if address A has a capacity of 1000 and address B has a capacity of 2000, then address B has twice the traffic capacity of address A. BytePlus GTM will return the address with the lowest latency from the user's geolocation, while meeting the load requirements of the addresses.<br><br>You can set a reasonable capacity value for your data center based on parameters such as bandwidth and concurrent connections. Capacity is a relative value, therefore you don't need to enter actual data like bandwidth or concurrent connections of the data center, but you need to ensure that different addresses or pools use a consistent unit of capacity. The pool's capacity needs to equal the sum of the capacities of all addresses within the pool.<br><br>If you have not chosen capacity routing mode, this parameter does not appear. |


After setting up, click **Next**.

&nbsp;

<span id="step-3-configure-health-checks"></span>
### Step 3: Configure health checks

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Billing for GTM health check tasks is based on the number of health check tasks. For billing details, refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/R4Anoj">Billing</a>.</div>


In the **Configure health checks** section of the **Instance configuration** page, configure health check parameters. BytePlus GTM will periodically perform health checks on the addresses through one or more health check probes. According to the results of the health checks, the addresses will be considered available or unavailable. See [How It Works](https://docs.byteplus.com/docs/byteplus-dns-suite/dWyQcY).

**Health check parameters**


|Parameter |Description |
|---|---|
|**Interval** |The time interval for health checks. The shorter the interval, the quicker the BytePlus GTM detects an unavailable address and triggers a failover, but the higher the billing. See [Billing](https://docs.byteplus.com/docs/byteplus-dns-suite/R4Anoj).<br><br><br>* 1 minute: (Default) Health check interval is 1 minute.<br><br>* 15 seconds: (Ultimate Edition only) Health check interval is 15 seconds. |
|**Protocol** |The communication protocol used for health checking.<br><br><br>* **Ping**: Based on ICMP protocol, uses Ping requests for health checking the address.<br><br>* **TCP**: Uses TCP connection for health checking the address.<br><br>* **HTTP**: Uses HTTP requests for health checking the address.<br><br>* **HTTPS**: Uses HTTPS requests for health checking the address. |


**Advanced configuration**

If you select **Ping** as your **Protocol**, you can also set the following parameters:


|Parameter |Description |
|---|---|
|**Timeout** |The timeout for a single packet. For example, if you set this parameter to 5 seconds, and the address does not respond within 5 seconds after the probe sends a packet, then the packet is considered to have timed out and lost. The default value is 5 seconds. |
|**Packet count** |The number of packets sent by a single probe in a health check cycle. The default value is 20. |
|**Probe failure threshold** |The threshold for the packet loss rate at which a health check by a single probe is considered failed within a health check cycle. For example, if you set this parameter to 10, and the packet loss rate exceeds 10%, then the result of this health check is considered failed. The default value is 10. |
|**Health check failure threshold** |Within a health check cycle, the threshold for determining whether the health check result for a single address is a failure. This threshold is the percentage of health check probe points that return failed health check results. BytePlus GTM sets this parameter to 50 and you cannot change it. If more than 50% of the health probes perform failed health checks, then the health check is considered failed. |
|**Address unavailability threshold** |The threshold for the number of consecutive health check failures that determines if a single address is unavailable. For example, if you set this parameter to 3, and a single address has 3 consecutive health check failures, then the address is considered unavailable. The default value is 3. |
|**Address recovery threshold** |The threshold for the number of health check successes to determine if an unavailable address is available. For example, if you set this parameter to 3, an unavailable address will be determined as an available address after 3 consecutive health check successes The default value is 0.<br><br>&nbsp;<br><br>If you set this parameter to 0, BytePlus GTM ignores this parameter and uses its internal logic to determine whether an unavailable address will be determined as available again. |


If you select **TCP** as your **Protocol**, you can also set the following parameters:


|Parameter |Description |
|---|---|
|**Port** |The TCP port of the address. The default value is 80. |
|**Single connection failure threshold** |The timeout for establishing a single TCP connection. For example, if you set this parameter to 2 seconds, and the TCP connection has not succeeded within 2 seconds from the start of the establishment during a health check, it is considered a connection failure. The default value is 2 seconds.<br><br>&nbsp;<br><br>If a TCP connection meets the timeout condition of the **All connections failure threshold** parameter before meeting the timeout condition of the **Single connection failure threshold** parameter, then the TCP connection is considered a failure. |
|**All connections failure threshold** |Over a health check cycle, a single probe establishes multiple TCP connections with the address. For example, if you set this parameter to 5 seconds, and no TCP connections are successfully established within 5 seconds from the start of the first connection attempt by a single probe, then all TCP connections during these 5 seconds are considered as timed out and failed. The default value is 5 seconds.<br><br>&nbsp;<br><br>If a TCP connection meets the timeout condition of the **Single connection failure threshold** before the **All connections failure threshold** is up, then the TCP connection is considered timed out and failed. |
|**Connection count** |The total number of TCP connections established by a single probe within a health check cycle. The default value is 20. |
|**Probe failure threshold** |The threshold for the failure rate of connections established by a single probe within a health check cycle, which determines whether the result of the health check for the probe fails. For example, if you set this parameter to 10, and the connection failure rate of a health check exceeds 10%, then the results of that probe for that health check are considered failed. The default value is 10. |
|**Health check failure threshold** |Within a health check cycle, the threshold for determining whether the health check result for a single address is a failure. This threshold is the percentage of health check probe points that return failed health check results. BytePlus GTM sets this parameter to 50 and you cannot change it. If more than 50% of the probes perform failed health checks, then the health check for the address is considered failed. |
|**Address unavailability threshold** |The threshold for the number of consecutive health check failures that determines if a single address is considered unavailable. For example, if you set this parameter to 3, and a single address shows 3 consecutive health check failures, then the address is considered unavailable. The default value is 3. |


If you select **HTTP** or **HTTPS** as your **Protocol**, you can also set the following parameters:


|Parameter |Description |
|---|---|
|**Port** |The HTTP port of the address. The default value is 80. |
|**Host** |The domain part of the address URL. For example, if the URL of the address is `https://www.byteplus.com/en/product/dns`, then the **Host** is `www.byteplus.com`. The default value is empty. If you select **HTTPS** as your **Protocol**, you must set this parameter. |
|**Path** |The path part of the address URL, starting with `/`. For example, if the URL of the address is `https://www.byteplus.com/en/product/dns`, then the **Path** is `/product/dns`. The default value is empty. |
|**Probe failure threshold** |The timeout for a health check from a probe. For example, if you set this parameter to 5 seconds, and the address does not respond within 5 seconds after starting a health check from a probe, then the health check from that probe is timed out and considered a failure. The default value is 5 seconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After a probe starts a health check, if the address returns an HTTP status code within the following ranges, the health check of that probe will also be considered a failure:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Custom HTTP status code</strong> is set to <strong>Disabled</strong>, the address returns an HTTP status code outside the 200 \- 399 range.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Custom HTTP status code</strong> is set to <strong>Enabled</strong>, the address returns an HTTP status code outside the custom range.</div><br> |
|**HTTP request method** |* GET: Uses the GET method.<br><br>* POST: Uses the POST method.<br><br>* HEAD: Uses the HEAD method.<br><br>* PUT: Uses the PUT method.<br><br><br>The default value is GET. |
|**HTTP request headers** |The HTTP request headers, including **Field name** and **Field value**. For example, **Field name** is `Accept-Encoding`, and **Field value** is `gzip`. The default value is empty. |
|**Custom HTTP status code** |Whether to customize a range of HTTP status codes. If the address returns an HTTP status code outside of this range, the health check is considered failed.<br><br><br>* **Disabled**: Use the default range of HTTP status codes. If the HTTP status code is outside the range of 200 \- 399, the result is considered failed.<br><br>* **Enabled**: You customize a range of HTTP status codes. You can click **Add** to add multiple criteria. If you add different types of criteria, the criteria are combined as follows:<br><br>   * If **Range** and **Include** criteria both exist, a status code satisfying either condition lies within the customized range. For example, if the **Range** criterion is 100 to 120, and the **Include** status code is 121, then the custom range includes status codes from 100 to 121.<br><br>   * If **Exclude** and other types of criteria exist, the status codes within the custom range must satisfy the **Exclude** criteria. For example, if the **Range** is 100 to 120, the **Include** status code is 121, and the **Exclude** status code is 100, then the custom range includes status codes from 101 to 121. If other criteria conflict with the **Exclude** criteria, the **Exclude** criteria take precedence. |
|**Health check failure threshold** |Within a health check cycle, the threshold for determining whether the health check result for a single address is a failure. This threshold is the percentage of health check probe points that return failed health check results. BytePlus GTM sets this parameter to 50 and you cannot change it. In a health check, if more than 50% of the probes perform failed health checks, then the health check of the address is considered failed. |
|**Address unavailability threshold** |The threshold for the number of consecutive health check failures that determines if an address is unavailable. For example, if you set this parameter to 3, and an address shows 3 consecutive failed checks, then the address is considered unavailable. The default value is 3. |


 **（Basic routing only) Health check probes**


|Parameter |Description |
|---|---|
|**Type** |The type of health check probes used by the GTM instance.<br><br><br>* **Recommended**: Use the health check probes recommended by BytePlus GTM. BytePlus GTM recommends health check probes based on the line you configure for the rule.<br><br>* **Custom**: Choose the health probes on your own. |


After you complete configuration, click **Next**.

<span id="Steps 4: Configure policy (Only for Basic Routing)"></span>
### Step 4: Configure policy (Basic routing only)

On the **Instance configuration** page, find the **Configure policy** section, configure your policy according to your actual business scenario.

<span id="rules"></span>
#### Rules

Refer to [Create a Rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP) to learn how to add a rule. You can also add rules after configuring the GTM instance.

After configuration, click **Next**.

<span id="Step Five: Enable and Verify"></span>
### Step 5: Verify expected traffic and start routing

In the **Start routing** section of the **Instance configuration** page, decide whether to start routing automatically after GTM instance configuration is completed.

<span id="Enable Instance"></span>
#### Start routing

If you wish to start routing after configuring the GTM instance, select **Start routing**. After you start a GTM instance, BytePlus GTM will deploy the rules under this GTM instance as DNS records to the authoritative DNS servers of BytePlus GTM. The rules start to take effect once the deployment is complete. Also, BytePlus GTM starts health checking for the GTM instance. You can view the DNS records actually deployed by BytePlus GTM in the operation logs. See [View Operation Logs](https://docs.byteplus.com/docs/byteplus-dns-suite/View_Operation_Logs).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you did not add traffic targets or pools while configuring policies, then <strong>Start routing</strong> is not available. You can start routing after adding traffic targets for intelligent routing policy or adding rules for basic routing policy. See <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy">Start or Stop Routing</a>.</div>


<span id="Expected Routing Diagram"></span>
#### Expected traffic view

Displays how BytePlus GTM routes user requests to the addresses based on your configuration.

If BytePlus GTM uses intelligent routing and has not added any traffic targets, or if BytePlus GTM uses basic routing and has not added any rules, then the expected routing diagram is not displayed.

After configuration, click **Submit**. Then, you can see the configured GTM instance on the **Instance management** page.


* If **Start routing** is enabled, the GTM instance is in **Running** status.

* If **Start routing** is not enabled, the GTM instance is in **Stopped** status.


<span id="Subsequent Steps"></span>
## Follow\-up steps

<span id="(Only for CNAME Access) Add a CNAME Record with Your Domain Registrar"></span>
### (CNAME connection method only) Create a CNAME record in your DNS provider

If you choose **CNAME** when creating the GTM instance, you need to create a CNAME record at your DNS provider that points your domain to the GTM instance’s routing domain. Refer to [Connect Your Domain to BytePlus GTM](https://docs.byteplus.com/docs/byteplus-dns-suite/pHJ6zL).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you chose <strong>Domain</strong> when creating the GTM instance, you do not need to create a CNAME record.</div>


<span id="Traffic Routing Verification"></span>
### Verify traffic

If you have started routing, refer to the [Getting Started](https://docs.byteplus.com/docs/byteplus-dns-suite/S1LBKo) to learn how to verify that the traffic to your domain is routed according to the GTM instance configuration.
