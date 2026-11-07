---
title: "Modifying instance counts of scaling groups"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

After you create a scaling group, you can modify the scaling group's instance count or capacity limits at any time.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* After you modify the instance count or capacity limits of a scaling group, the scaling group will immediately trigger an instance count check, and the number of instances in the group will change accordingly. For example, if there are currently 5 instances in the scaling group and the maximum number of instances is modified to 3, the scaling group will immediately delete 2 instances.

* Instances with instance protection enabled cannot be automatically deleted or removed from a scaling group. Therefore, if the new maximum number of instances (or expected number of instances) is not greater than the number of protected instances in the scaling group, unprotected instances (if any) will be deleted or removed first, and then the scaling group's automatic scaling activities will be stopped.

* The default upper limit for the maximum number of instances is 100. You can raise the upper limit in the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), with a maximum allowable value of 1000.


<span id=".5L-u5pS55a6e5L6L5pWwL-WuuemHjw=="></span>
## Modify the instance count or capacity


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of your target resource.

3. Click the name of the scaling group and select the "Overview" tab.

4. Click the "Modify Instances/Capacity" button and adjust the instance count or capacity based on your needs.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can enable or disable the expected instance count or capacity feature. When you enable the feature, the expected instance count or capacity must be between the maximum and minimum instance count or capacity.   </div>
   

   5. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup)
