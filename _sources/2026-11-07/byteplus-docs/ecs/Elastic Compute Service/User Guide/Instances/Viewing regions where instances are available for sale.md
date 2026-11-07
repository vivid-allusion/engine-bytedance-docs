---
title: "Viewing regions where instances are available for sale"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing_regions_where_instances_are_available_for_sale"
---

Instance types available for sale may vary in different regions and availability zones. You can refer to the methods in this topic to view the inventory and other information of the target instance.

<span id="Qj4WCzRP"></span>
## Background

Before you purchase an instance, we recommend that you understand the sale regions, inventory, quotas, and other information of the target instance type. This helps you make an informed choice.


* Regional differences: Instance types available for sale may vary in different regions. Please select a region based on your business needs. [How to select a region?](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones)

* Inventory limit: The instance type you need may temporarily be unavailable for sale in some regions due to inventory shortage. We recommend that you refresh the inventory periodically or check the inventory in other regions. [How to view inventory?](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) 

* If your account does not have the required resource quota (e.g., the number of vCPUs exceeds the limit), this may also lead to failure to purchase the target instance. Please check and change your quota settings. [How to view and change quota?](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management)


<span id="Qj4WCzRP"></span>
## Method 1: View on the console

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This method is only applicable for viewing instances in GA status by default. To view instances in Beta, contact your account manager to apply to be added to the allowlist, or use method 2.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. Hover the cursor over the "Availability zone" column of a target instance type to view the availability zones.

   As shown in the following picture, the system automatically displays the inventory and availability of the instance type in each region.


<span id="GzHx0dIr"></span>
## Method 2: Query by calling API operation

If you want to access the regions and inventory information of an instance through programming, you can call the [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) operation . This API operation queries the inventory of computing resources in an availability zone, including region, availability zones, and inventory of computing resources.

<span id="qDOC2d0A"></span>
## Method 3: View on the price calculator

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The price calculator only displays instances in GA status. To view instances in Beta, use method 2.</div>



1. Go to the [price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2) page.

2. Select an instance type, and the system will show the prices and availability status of this type in each region.


<span id="rD7TBah3"></span>
## Related documents


* [Regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones)

* [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances)

* [Managing instance resource quota](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management)


<span id="rD7TBah3"></span>
## FAQs


* [How to select a region?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V6YCJ5oup5Zyw5Z-f77yf)

* [How to select an availability zone?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V6YCJ5oup5Y-v55So5Yy677yf)

* [Can I change the region and availability zone after purchasing an instance?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5a6e5L6L6LSt5Lmw5a6M5oiQ5ZCO5piv5ZCm5Y-v5Lul5pu05o2i5Zyw5Z-f5ZKM5Y-v55So5Yy677yf)

* [How do I choose an ECS instance suitable for my business?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V6YCJ5oup6YCC5ZCI5oiR5Lia5Yqh55qERUNT5a6e5L6L77yf)

* [What should I do when "Sold out" appears when I purchase an instance of a particular type?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.6LSt5Lmw5p-Q6KeE5qC855qE5a6e5L6L5pe277yM5pi-56S64oCc5bey5ZSu572E4oCd5oCO5LmI5Yqe77yf)


For more questions about purchasing instances, refer to [Instance FAQs](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs).
