---
title: "Region and Availability Zone"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Regions-and-Availability-Zones"
---

<span id=".5Zyw5Z-f77yIUmVnaW9u77yJ"></span>
## Region

<span id=".566A5LuL"></span>
### Instructions​

A region is a geographical zone where a data center is located. The intranet is completely isolated among different regions, maximizing stability and fault tolerance of different regions. Regions are usually divided based on the city where the data center is located.

<span id=".5aaC5p6c6YCJ5oup5Zyw5Z-f77yf"></span>
### How to select a region?

Select the same region as the Elastic Compute Service (ECS) that will use the NAT Gateway. Once created, the NAT Gateway's region cannot be changed.

<span id=".5Y-v55So5Yy677yIQVrvvIk="></span>
## Availability Zone

<span id=".566A5LuL"></span>
### Instructions​

An Availability Zone (AZ) refers to a physically isolated location within the same region, featuring independent power and network infrastructure.

<span id=".55u45YWz54m55oCn"></span>
### Related features

The NAT Gateway supports cross\-Availability Zone disaster recovery. If the primary availability zone fails, the NAT Gateway automatically switches to the secondary availability zone to ensure normal business operations.

<span id=".5aaC5L2V6YCJ5oup5Y-v55So5Yy677yf"></span>
### How to select an availability zone

Select the availability zone where the NAT Gateway resource is deployed.

<span id=".5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo"></span>
## Regions and Availability Zones

The currently available regions and AZs are listed in the table below. We will gradually add more regions and AZs for your selection and use.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Product features may vary by regions. The features available in the console shall prevail.</div>



|Regions |RegionID |AZ quantity |ZoneID |Status |
|---|---|---|---|---|
|**China regions** |||||
|China (Beijing) |cn\-beijing |4 |* AZ A: cn\-beijing\-a<br><br>* AZ B: cn\-beijing\-b<br><br>* AZ C: cn\-beijing\-c<br><br>* AZ D: cn\-beijing\-d |GA |
|China (Shanghai) |cn\-shanghai |4 |* AZ A: cn\-shanghai\-a<br><br>* AZ B: cn\-shanghai\-b<br><br>* AZ C: cn\-shanghai\-c<br><br>* AZ E: cn\-shanghai\-e |GA |
|China (Guangzhou) |cn\-guangzhou |3 |* AZ A: cn\-guangzhou\-a<br><br>* AZ B: cn\-guangzhou\-b<br><br>* AZ C: cn\-guangzhou\-c |GA |
|China (Hong Kong) |cn\-hongkong |2 |* AZ A: cn\-hongkong\-a<br><br>* AZ B: cn\-hongkong\-b |GA |
|**Other countries and regions** |||||
|Asia Pacific (Johor) |ap\-southeast\-1 |3 |* AZ A: ap\-southeast\-1a<br><br>* AZ B: ap\-southeast\-1b<br><br>* AZ C: ap\-southeast\-1c |GA |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |3 |* AZ A: ap\-southeast\-3a<br><br>* AZ B: ap\-southeast\-3b<br><br>* AZ C: ap\-southeast\-3c |GA |
