---
title: "Cross-account Transit Router sharing​​"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Cross-account-Transit-Router-sharing"
---

<span id="kZvcUT06"></span>
## Scenarios

To enable cross\-account connectivity, you must first share your Transit Router (TR) with another account that owns the target network instance. Once shared, the recipient account can manage and connect to the TR.

<span id="B4V1j8Hx"></span>
## Prerequisites


* You have created a TR instance. To create a new instance, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

* If you share the Transit Router (TR) within the same enterprise organization, you must [enable the enterprise organization](https://docs.byteplus.com/en/docs/organization/ActivatingOrganizationService).


<span id="ElzHMy5u"></span>
## Configuration procedures

<span id="kFuWwFWD"></span>
### Step 1: Initiate TR sharing (Resource owner)


1. Log in to [the Resource management console](https://console.byteplus.com/resourcemanager/).

2. In the left\-side navigation pane, select **Resource sharing \> Shared by me**.

3. In the top menu bar, select your target region.

4. On the **Shared unit** tab, click **Create shared unit** and configure the parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Unit name |Type in a name for the shared unit. |Shared TR |
   |Regions |Region defaults to the region selected in the top menu bar. To modify, reselect the region in the top menu bar. |China (Beijing) |
   |Product |Select the Transit Router \- TR instance. |Transit Router \- TR instance. |
   |ID |Type in the ID of the TR to be shared, then search and check it. |Check the target transit router |
   

5. Click **Next** to associate sharing permissions.

   TR sharing permissions are system\-defined and cannot be modified. For default supported actions, see [Instructions](https://docs.byteplus.com/en/docs/transitrouter/Cross-account-Sharing-overview#T39M302D).

6. Click **Next** to associate shared users.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Resource user |Choose a method for resource sharing.<br><br><br>* **Allow sharing with any account**: Share the TR with any BytePlus root account.<br><br>* **Only allow sharing with enterprises and organizations**: Share the TR only with BytePlus root accounts in the same enterprise organization. |Allow sharing with any account |
   |Add by business organization |Select main account for the user type, enter the user ID, and click **Add** to assign the resource user.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Enterprise organization administrators can enable organization\-based sharing by turning on <strong>Add by business organization</strong>. This allows them to quickly select the entire organization, specific organizational units, or individual member accounts from the organizational directory.</div><br> |\-\- |
   

7. Click **Next** to confirm that the resources, associated permissions, and shared users are correct.

8. Click **Confirm** to complete the action.


<span id="kFuWwFWD"></span>
### Step 2: Accept a sharing invitation (Shared user)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When sharing resources within an enterprise organization, member accounts automatically accept invitations. No manual acceptance is required. The sharing invitation is valid for 14 days and will be automatically denied if it expires.</div>



1. Log in to [the Resource management console](https://console.byteplus.com/resourcemanager/).

2. In the left\-side navigation pane, select **Resource sharing \> Share with me**.

3. In the top menu bar, select your target Region.

4. Click **Accept** to the right of the shared unit to complete the action.


<span id="kFuWwFWD"></span>
### Step 3: Create a cross\-account attachment (Shared user)

Create a cross\-account intra\-region attachment based on the type of the target network instance. For procedures, see [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc), [Creating a VPN attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpn), and [Creating a Direct Connect Gateway attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">When configuring parameters, the system defaults to disabling association forwarding and route learning. If these features are enabled, the default route table is automatically associated, which cannot be modified by the shared user. To modify it, contact the resource owner.</div>


<span id="qVJsm57G"></span>
## Related actions


|Related actions |Description |
|---|---|
|Modify TR sharing |After initiating sharing, you can modify shared resources and users as needed. For procedure, see [Edit a shared unit](https://docs.byteplus.com/en/docs/resourcemanagement/Shared_by_Me_Management#editing-shared-unit). |
|Cancel TR sharing |If cross\-account communication via this Transit Router (TR) is no longer needed, cancel the share. For procedure, see [Delete a shared unit](https://docs.byteplus.com/en/docs/resourcemanagement/Shared_by_Me_Management#deleting-shared-unit). |
|Decline a sharing invitation |shared resources you do not need can be denied. For procedure, see [Reject sharing invitation](https://docs.byteplus.com/en/docs/resourcemanagement/Shared_with_Me_Management#rejecting-share-invitation). |


<span id="yS3z3bfw"></span>
## Related documentation


* [CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment): Create a VPC attachment.

* [CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment): Create a VPN attachment.

* [CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment): Create a Direct Connect Gateway attachment.
