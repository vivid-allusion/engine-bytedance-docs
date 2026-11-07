---
title: "Limits"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Limits"
---

<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limits


|Quota parameter |Description |Maximum |Increasable |Adjustable quota limit |
|---|---|---|---|---|
|bandwidth_package |Maximum number of IPv4 Bandwidth Packages that can be created per account per region |5 |If the default quota is insufficient for your needs, please contact your account manager. |\-\- |
|bandwidth_package_ipv6 |Maximum number of dual\-stack Bandwidth Packages that can be created per account per region |5 ||\-\- |
|bandwidth_package/eip |Maximum number of EIPs or IPv6 Internet bandwidths can be added per Bandwidth Package instance |100 |If the default quota is insufficient for your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=bandwidthpackage) to apply for a quota increase. |500 |


<span id=".5bim5a696ZmQ5Yi2"></span>
## Bandwidth limits


|Metering method |Maximum bandwidth range (Mbps) |
|---|---|
|Pay\-by\-main\-traffic |(2\-2000) Mbps |
|Pay\-by\-bandwidth |(2\-5000) Mbps |
|Pay\-by\-95th\-peak |(2\-5000) Mbps |
|Subscription |(5\-5000) Mbps |


Bandwidth Package adopts a distributed high\-availability cluster architecture, distributing all traffic evenly across multiple traffic forwarding servers in the cluster. Therefore, the maximum bandwidth you set for the Bandwidth Package will be evenly allocated to these servers.

> Maximum traffic for a single connection = Maximum bandwidth of Bandwidth Package ÷ Server count in the cluster.

> For example, if you set the maximum bandwidth of Bandwidth Package to 5000 Mbps and the Bandwidth Package cluster contains 4 traffic forwarding servers, then the maximum traffic for a single connection is 5000 Mbps ÷ 4 = 1250 Mbps.


Rate limiting rules for Bandwidth Package:


* Inbound bandwidth: The inbound bandwidth rate is limited to the purchased maximum bandwidth.

* Outbound bandwidth: The outbound bandwidth rate is limited to the purchased maximum bandwidth.


For example, if the maximum bandwidth of your purchased Bandwidth Package is 5000 Mbps, then the maximum inbound and outbound bandwidths are both 5000 Mbps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Bandwidth Packages can only reach the set maximum bandwidth when multiple connections are used. You cannot reach the set maximum with less connections.</div>


* <div data-tips="true" data-tips-type="tip">When the total bandwidth of a Bandwidth Package instance exceeds 5000 Mbps, the platform automatically activates distributed rate limiting.</div>


* <div data-tips="true" data-tips-type="tip">During use, the maximum bandwidth of a Bandwidth Package instance may exceed your set value. With technology upgrades, the limit becomes more precise. Therefore, we recommend setting a maximum bandwidth slightly higher than your business requirements.</div>



<span id=".5YW25LuW6ZmQ5Yi2"></span>
## Limits on adding cloud resources to Bandwidth Package


|Protocol type for Bandwidth Package |Supported cloud resource |Prerequisites for adding resources |
|---|---|---|
|IPv4 |Pay\-as\-you\-go EIP |* Both are in the same region.<br><br>* Both have the same ISP.<br><br>* Both have the same protection type. |
|Dual\-stack |* Pay\-as\-you\-go EIP<br><br>* pay\-as\-you\-go IPv6 Internet bandwidth ||


&nbsp;

<span id=".5Yqg5YWl5YWx5Lqr5bim5a695YyF6ZmQ5Yi2"></span>
### 

<span id=".5Yqg5YWl5YWx5Lqr5bim5a695YyF6ZmQ5Yi2"></span>
###
