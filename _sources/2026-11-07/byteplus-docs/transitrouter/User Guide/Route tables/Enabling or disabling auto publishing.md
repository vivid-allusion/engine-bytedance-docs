---
title: "Enabling or disabling auto publishing"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attachments-04"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The auto publishing feature automatically publishes routes in the Transit Router (TR) route table to the route table of the network instance. The default status of the auto publishing feature depends on the TR attachment type, as shown in the table below.


|Attachment type |Routing propagation mode |Auto publishing status |
|---|---|---|
|VPC attachment |\-\- |This feature is related to the settings during creation and can be enabled/disabled as needed. |
|VPN attachment |Static routes |This feature is disabled by default and cannot be enabled. |
||Dynamic |This feature is enabled by default and cannot be disabled. |
|DC Gateway attachment |\-\- |This feature is enabled by default and cannot be disabled. |
|Inter\-region attachment |\-\- |This feature is enabled by default and cannot be disabled. |


<span id=".5pON5L2c6K-05piO"></span>
## Enable auto publishing

<span id=".5pON5L2c6K-05piO"></span>
### Limits


* When a single Virtual Private Cloud (VPC) is attached to multiple TR instances, each TR can have auto publishing enabled for up to 5 VPC attachments.

* Auto publishing for a cross\-account VPC attachment can only be enabled by the VPC owner. The TR owner cannot perform this action.


<span id=".5pON5L2c6K-05piO"></span>
### Instructions


* When you enable auto publishing, the system automatically retrieves routes from the TR associated forwarding route table for the target attachment. It then publishes these routes into the route table of that network instance. For details, see [Route synchronization](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx5L2_55So6ZmQ5Yi2).

* If you have manually configured a route pointing to the TR on the VPC side and want to use the auto publishing feature, first enable auto publishing, then delete the manually configured route on the VPC side.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This action may cause about 1 second of service interruption. Assess its impact carefully and perform it during off\-peak hours.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click the switch in the **Auto Publish Route** column of the target network instance attachment.

5. Click **Enable** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Disable auto publishing

<span id="H1fzM3bF"></span>
### Instructions


* If you disable auto publishing, the system automatically deletes the route entries published from TR to VPC. This may affect communication between the VPC and other networks. Proceed with caution.

* Auto publishing for a cross\-account VPC attachment can only be disabled by the VPC owner. The TR owner cannot perform this action.


<span id="H1fzM3bF"></span>
### Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the area under **Basic information**, select the ** Intra\-region attachments** tab.

4. Click the switch in the **Auto Publish Route** column of the target network instance attachment.

5. Click **Disable** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyTransitRouterVpcAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes): Modify the name, description, and attachment point of a specified VPC attachment, and enable or disable route publishing for the specified VPC attachment.
