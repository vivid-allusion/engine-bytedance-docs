---
title: "Regions and Availability Zones"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones"
---

<span id=".5Zyw5Z-f"></span>
## Regions

<span id=".566A5LuL"></span>
#### Introduction​

A region refers to a distinct geographic area where physical data centers are located, typically divided based on the city in which the data center resides.

<span id=".55u45YWz54m55oCn"></span>
#### Related features


* Private networks between different regions are completely isolated, ensuring maximum stability and fault tolerance across regions.

* You can either use Elastic IP Addresses (EIP) for public interconnectivity across regions, or leverage Cloud Enterprise Network (CEN) for private interconnection.


<span id=".5aaC5L2V6YCJ5oup5Zyw5Z-f77yf"></span>
#### How to select a region?


|Considerations |Recommended solution |
|---|---|
|Geographic location |To minimize access latency and maximize download speeds, we recommend creating your VPC in the region geographically closest to your target services. Note that the region cannot be modified after resource creation. |
|Private network connectivity |If isolating private networks is required, deploy them in different regions. If connecting private networks is required, deploy them in the same region. |


<span id=".5Y-v55So5Yy6"></span>
## Availability zone

<span id=".566A5LuL"></span>
#### Introduction​

An Availability Zone (AZ) refers to a physically isolated location within the same region, featuring independent power and network infrastructure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f10d7e47d58eae704eb219b7f37832f.png) </span>

<span id=".55u45YWz54m55oCn"></span>
#### Related features


* Within the same region and VPC, different AZs interconnect over the private network.

* Availability Zones are fault\-isolated, meaning a failure in one AZ does not impact the normal operation of others, ensuring your business remains continuously online.


<span id=".5aaC5L2V6YCJ5oup5Y-v55So5Yy677yf"></span>
#### How to select an availability zone


* To ensure disaster recovery capabilities for your services, we recommend deploying them across different Availability Zones within the same region.

* If your services require lower latency, we recommend deploying them within the same Availability Zone.

* Availability Zone cannot be changed after resource creation.


<span id="Wlloay4G"></span>
## Regions and Availability Zones

The currently available Regions and Availability Zones are listed in the table below. We will gradually add more Regions and Availability Zones for your selection and use.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="tip">Product features may vary by Region. The features available in the console shall prevail.</div>



|Regions |RegionID |AZ Quantity |ZoneID |Status |
|---|---|---|---|---|
|**China regions** |||||
|China (Beijing) |cn\-beijing |5 |* AZ A: cn\-beijing\-a<br><br>* AZ B: cn\-beijing\-b<br><br>* AZ C: cn\-beijing\-c<br><br>* AZ D: cn\-beijing\-d<br><br>* AZ\-E: cn\-beijing\-e |GA |
|China (Shanghai) |cn\-shanghai |4 |* AZ A: cn\-shanghai\-a<br><br>* AZ B: cn\-shanghai\-b<br><br>* AZ C: cn\-shanghai\-c<br><br>* AZ E: cn\-shanghai\-e |GA |
|China (Guangzhou) |cn\-guangzhou |3 |* AZ A: cn\-guangzhou\-a<br><br>* AZ B: cn\-guangzhou\-b<br><br>* AZ C: cn\-guangzhou\-c |GA |
|China (Hong Kong) |cn\-hongkong |3 |* AZ A: cn\-hongkong\-a<br><br>* AZ B: cn\-hongkong\-b<br><br>* AZ C: cn\-hongkong\-c |GA |
|**Other countries and regions** |||||
|Asia Pacific (Johor) |ap\-southeast\-1 |3 |* AZ A: ap\-southeast\-1a<br><br>* AZ B: ap\-southeast\-1b<br><br>* AZ C: ap\-southeast\-1c |GA |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |3 |* AZ A: ap\-southeast\-3a<br><br>* AZ B: ap\-southeast\-3b<br><br>* AZ C: ap\-southeast\-3c |GA |


&nbsp;

&nbsp;
