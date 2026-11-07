---
title: "Limits"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Limits"
---

Before using an elastic IP address (EIP), understand the quota and related limits of the EIP.

<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limits


|Quota parameter |Description |Maximum |Description |Adjustable limit |
|---|---|---|---|---|
|eip |Number of EIPs that can be applied for per account per region |20 |If the default quota does not meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=EIP) to request an increase. |30 |
|\- |Daily number of EIP applications per account per region |Twice the number of EIPs that can be applied for |Application/association count = console action count + API call count.<br><br><br>* Console action count: Number of times to apply for/associate an EIP via the EIP console.<br><br>* API call count: Number of times to apply for/associate an EIP by API calls. |\-\- |
|\- |Daily number of times that an account associates an EIP to a cloud resource per region |Three times the number of EIPs that can be applied for ||\-\- |


<span id=".5Yqf6IO96ZmQ5Yi2"></span>
## Feature limits


|Limit item |Description |
|---|---|
|EIP |An EIP can only associate with one cloud resource in the same region at a given period.<br><br>The applied public IP address cannot be modified. |
|Associate with Elastic Compute Service |EIPs can only be associated with running or stopped ECS instances. |
|Associate with Internet NAT Gateway |An Internet NAT Gateway can associate up to 10 EIPs.<br><br>An Internet NAT Gateway requires at least one EIP for access to the Internet. |
|Associate with Classic Load Balancer |A Classic Load Balancer (CLB) can only be associated with one EIP at a given time. |
|Associate secondary network interface |An ECS instance can mount multiple secondary network interfaces. By associating EIPs with these secondary network interfaces, a single ECS instance can have multiple EIPs. |


<span id=".5oCn6IO96ZmQ5Yi2"></span>
## Performance limits


|Metering method |Bandwidth cap at application (Mbps) |Bandwidth cap at modification (Mbps) |How to increase the maximum bandwidth |
|---|---|---|---|
|Pay\-by\-data\-transfer |1 \- 200 |1 \- 200 |Add an EIP to a Bandwidth Package to share high bandwidth. For more details, see [How to increase the bandwidth cap of an EIP](https://docs.byteplus.com/en/docs/eip/Bandwidth-FAQs). Contact customer service support if you have questions. |
|Pay\-by\-bandwidth |1 \- 500 |1 \- 1000 ||
|Subscription |1 \- 500 |1 \- 1000 ||


<span id=".5Zyw5Z-f57qn5bim5a696ZmQ5Yi2"></span>
## Regional bandwidth limits

When purchasing an EIP, you must specify the outbound bandwidth cap. The platform charges based on the outbound bandwidth.


* Inbound bandwidth:

   * If you set the bandwidth cap to less than 10 Mbps (inclusive), the platform defaults to allocate 10 Mbps for inbound bandwidth.

   * If you set the bandwidth cap to more than 10 Mbps, the platform allocates the same value for inbound bandwidth.

* Outbound bandwidth: The allocated outbound bandwidth equals the set value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After being added to a Bandwidth Package, the EIP shares the package’s bandwidth. Regional outbound/inbound bandwidth caps become invalid, but the regional bandwidth purchase limit remains effective.   </div>
   

   
   |Limits |Description |Bandwidth cap (Gbps) |Effective target |
   |---|---|---|---|
   |Regional outbound bandwidth cap |Maximum outbound peak bandwidth for all EIPs under a single account in a single region. |5 |Pay\-by\-data\-transfer EIP |
   |Regional inbound bandwidth cap |Maximum inbound peak bandwidth for all EIPs under a single account in a single region. |5 |Pay\-by\-data\-transfer EIP |
   |Regional bandwidth purchase limit |The maximum total of EIPs and IPv6 Internet bandwidth can be purchased under a single account in a single region. |50 |Pay\-as\-you\-go and Subscription EIPs and Pay\-as\-you\-go IPv6 Internet bandwidth. |
