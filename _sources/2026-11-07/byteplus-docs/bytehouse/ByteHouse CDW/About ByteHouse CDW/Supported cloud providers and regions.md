---
title: "Supported cloud providers and regions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-supported-regions-and-providers"
---

<span id="supported-cloud-providers"></span>
## Supported cloud service platforms

The current ByteHouse Cloud Warehouse edition runs on BytePlus, fully operating on a cloud infrastructure. This means that computing, storage, and service layers are fully deployed and managed on the cloud platform.

<span id="f79cb58e"></span>
## Supported regions and availability zones

Regions determine the geographical storage location of data and can also decide the location of computing resources. Selecting a region that is the same or close to your business services will reduce latency and lower the costs of data analysis and transmission.

The regions supported by ByteHouse are as follows, and you can choose the appropriate region and availability zone for deploying ByteHouse according to your business circumstances.

<span id="74d2115e"></span>
### Cluster connection address


|**Regions** |**RegionID** | **[Recommended] Cluster connection address SQL TCP (Host:Port)**  |**OpenAPI Address** |
|---|---|---|---|
|Hong Kong |cn\-hongkong |In the Console **Tenant Management\-Basic Information\-Network Information**, obtain the tenant\-specific cluster connection `{HOST}`address (private or public network).<br><br>`{PORT}`default is 19000. |In the Console **Tenant Management\-Connection Information\-Public API Domain**, obtain the tenant\-specific connection address (private or public network).<br><br>For details, refer to [API List](https://docs.byteplus.com/docs/bytehouse/api-list). |
|Johor |ap\-southeast\-1 |||
|Jakarta |ap\-southeast\-3 |||


<span id="18dc0302"></span>
### Cluster connection port

Refer to the table below for the ports used by common connection methods.


|Connection Method / way |Port Number |
|---|---|
|TCP |19000 |
|HTTP |8123 |
|MySQL Client |3306 |


<span id="7848e272"></span>
## Caution

If there are access restrictions in your network environment, please add the following IP addresses to the whitelist to ensure normal access to ByteHouse cloud data warehouse services.


|**Regions** |**Public Internet Exit IP** |
|---|---|
|Hong Kong |150.5.146.60, 150.5.168.25 |
|Southeast Asia (Johor) |101.47.140.89, 101.47.11.124 |
|Southeast Asia (Jakarta) |163.7.17.61, 163.7.18.196 |
