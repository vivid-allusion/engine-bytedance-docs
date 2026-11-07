---
title: "Regions"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Regions"
---

<span id="2BCaD3yA"></span>
## Region term

<span id="XM9L4NQt"></span>
#### Introduction​

A region refers to a specific geographic area where a physical data center resides. Regions are typically divided based on the city where the data center resides.

<span id="o1TpUN8j"></span>
#### Related features


* Private networks between different regions are completely isolated, ensuring maximum stability and fault tolerance across regions.

* You can either use Elastic IP Addresses (EIP) for public interconnectivity across regions, or leverage Cloud Enterprise Network (CEN) for private interconnection.


<span id="Yg9G2uUw"></span>
#### How to select a region


|Considerations |Recommended solution |
|---|---|
|Geographic location |To reduce access latency and improve download speeds, it is recommended to select the region closest to your target service when purchasing resources. The region cannot be changed after the resources are purchased. |
|Private network connectivity |If isolating private networks is required, deploy them in different regions. If connecting private networks is required, deploy them in the same region. |
|Resource pricing |Resource prices vary by region. Please select the region based on your budget and the reference price on the purchase page. |


<span id="YocmnS6d"></span>
## Region list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="tip">The availability of regions varies by product. The regions available in the console shall prevail.</div>



|Region |RegionID |Stage |
|---|---|---|
|**China regions** |||
|China (Beijing) |cn\-beijing |GA |
|China (Shanghai) |cn\-shanghai |GA |
|China (Guangzhou) |cn\-guangzhou |GA |
|China (Hong Kong) |cn\-hongkong |GA |
|**Other countries and regions** |||
|Asia Pacific (Johor) |ap\-southeast\-1 |GA |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |GA |
