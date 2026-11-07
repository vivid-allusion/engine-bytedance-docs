---
title: "Configuring workspace public network access"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_workspace_public_network_access"
---

You can bind an [Elastic IP Address ](https://docs.byteplus.com/en/docs/eip/What-is-EIP)(EIP) to workspaces using the Supabase engine to enable access to the workspace over the public network. This topic describes the steps to configure public network access for the workspace.

<span id="4tSauYyH"></span>
## Background

Workspaces using the Supabase engine automatically provide services using the AI Native Database Platform’s shared public network after creation. Workspaces can also use a dedicated public network for services, but the shared public network and the dedicated public network cannot be used simultaneously. You can switch the workspace between a shared public network and a dedicated public network or change the EIP for the workspace. Switching requires disabling the current public network access first and then enabling it again to apply the change.

<span id="lJnnZFHF"></span>
## Billing

If a workspace using the Supabase engine requires service via a dedicated public network, an EIP is necessary. [Elastic IP Address](https://docs.byteplus.com/en/docs/eip/What-is-EIP) (EIP) is a standard service provided by BytePlus. Using EIP on the AI Native Database Platform is billed according to the EIP pricing standards. For more billing information about EIPs, refer to [Elastic IP Address.](https://docs.byteplus.com/en/docs/eip/Billing-overview).

<span id="uiVz2qzY"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**.

* To disable public network access for the workspace, you must first enable private network access for the workspace. To enable private network access, refer to [Configuring workspace private network access](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_workspace_private_network_access).


<span id="SPgHZow2"></span>
## Precautions


* After disabling public network access, the workspace cannot be accessed or connected through the public network or the Supabase console.

* A pay\-as\-you\-go EIP enters the **Closed** status after it falls into arrears for two hours and is automatically disassociated from resources. If you use a pay\-as\-you\-go EIP, monitor your account balance closely and top up promptly when the balance is insufficient to avoid the instance public network access address becoming unavailable due to account arrears. For more information about public IP address billing, refer to [Elastic IP Address](https://docs.byteplus.com/en/docs/eip/Arrears).

* Two hours after the account falls into arrears, the workspace enters a closed status for up to 7 days. During this period, after you top up your account, settle the overdue bills, and have an available balance greater than 0, the workspace status will automatically restore to **Running**. However, released EIPs will not be re\-associated with the workspace. You need to manually enable public network access and bind a new EIP to the workspace.

* The EIP console supports unbinding EIPs from their associated cloud resources. Exercise caution when performing unbinding operations in the EIP console.

* AI Native Database Platform provides a customized pg_net extension for the PostgreSQL database used by workspaces using the Supabase engine. Some public network addresses deemed unsafe cannot connect to the workspace. If this happens, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact us at any time.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your workspace was created before March 17, 2026, when pg_net is detected as not installed, you can follow these steps to resolve it.   </div>
   

   1. <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/aidap/Supabase-Suspending_a_workspace">Suspend</a>, <a href="https://docs.byteplus.com/en/docs/aidap/Supabase-Pausing_a_workspace">stop</a>, and <a href="https://docs.byteplus.com/en/docs/aidap/Supabase-Starting_a_workspace">start</a> the workspace sequentially.   </div>
   

   2. <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Execute <code>CREATE EXTENSION IF NOT EXISTS pg_net WITH SCHEMA extensions;</code>.   </div>
   

   3. <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Refer to this topic to disable and then enable the public network access.   </div>
   


<span id="aqMOperf"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, complete the following steps to enable or disable public network access.



<Tabs>
<Tab zoneid="ypi3FOipnI" title="Enable public network access">
<TabTitle>Enable public network access</TabTitle>

6. Click **Connect** on the **Supabase public network connection string** card at the top of the page. In the pop\-up ** Supabase public network connection string info** page, complete the following steps to enable shared public network or dedicated public network access.

   * **Enable shared address**

      1. On the **Supabase public network connection string** page, click **Enable shared address** in the **Actions** column.

      2. In the **Confirm enable shared address?**  dialog box, click **OK**.

   * **Enable dedicated address**

      3. On the **Supabase public network connection string** page, click **Enable dedicated address** in the **Actions** column.

      4. On the **Enable public network access** page, select the required EIP, then click **OK**.


</Tab>
<Tab zoneid="PfMHqZw7r9" title="Disable public network access">
<TabTitle>Disable public network access</TabTitle>

6. Click **Connect** on the **Supabase public network connection string** card at the top of the page. In the pop\-up ** Supabase public network connection string info** page, click **Disable** in the **Actions** column to enter the **Enable public network access** page.

7. In the pop\-up **Are you sure to disable the public network access?**  dialog box, click **OK**.


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After enabling or disabling public network access for the workspace, the workspace will switch to <code>Network changing</code> status and return to <code>Running</code> status once the change is complete.</div>
