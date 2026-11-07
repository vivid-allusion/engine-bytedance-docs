---
title: "Quota management"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Quota_management"
---

Workspaces using the Supabase engine support quota management for each user's AI models access token usage. This topic describes how to view users' token usage, set global default quotas, and customize quotas for individual users.

<span id="1iioN8oF"></span>
## Precautions


* In a newly created workspace, the default user quota (token and image generation) is 0, the customized user quota is "default," and user usage is 0.

* When creating a child branch, 

   * If "Target time for data synchronization" is set to "Present time," the child branch inherits the parent branch's user quota configuration at the present time, and the child branch's user usage is 0.

   * If "Target time for data synchronization" is set to "Specific time," the child branch inherits the parent branch's user quota configuration at the specific time, and the child branch's user usage is 0.

* When restoring a branch to a "Specific time, the branch's user quota will restore to the configuration at that specific time while the user usage remains unchanged.

* User token usage statistics are processed afterward, so actual usage may slightly exceed the quota value.


<span id="oVDFs7Qz"></span>
## Function entry


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, select **AI models access** \> **Quota management** tab.


<span id="tyZBo9Wl"></span>
## Global default quota

At the top of the **Quota management** page, the current global default quota configuration is displayed:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default daily token quota per user is 0, and the default daily image generation quota per user is 0, meaning AI models access is not supported.</div>


Click the edit icon on the right to modify the global default quota method and limit. The restriction method can be either specific amount (requires setting quota) or unlimited (no quota setting required). After modification, all users without individually set quotas will automatically apply the new default values.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Setting a reasonable global quota helps control overall token usage costs and is recommended to adjust according to team size and business needs.</div>


<span id="iUNW6fy8"></span>
## Set quota for individual users

if certain users require a higher or lower token quota for their business scenarios, you can configure it individually:


1. Find the target user in the user list.

2. Click the edit icon in the **Daily quota** column.

3. Enter the customized quota value and save.

   * **Token quota**: supports selecting **Specific amount** or **Unlimited**. When selecting specific amount, you need to enter a specific value, unit is **10,000/Day**.

   * **Image generation quota**: supports selecting **Specific amount** or **Unlimited**. When selecting specific amount, you need to enter a specific value, unit is **images/day**.


After configuration, the user's quota will no longer be affected by the global default quota.

<span id="4ZsWaL3F"></span>
## User list

The page body displays the list of all users accessing AI models, including the following fields:


|**Field** |**Decscription** |
|---|---|
|User ID / Email |The user's unique identifier UUID and associated email address. |
|Token usage today |The token count consumed by the user on the current day. |
|Historical token consumption |Cumulative consumed token count of a user. |
|Images generated today |The number of images generated by the user using AI models on the current day. |
|Total images generated |The total number of images generated by this user using the AI model. |
|Daily quota |This user's daily token limit. Displaying "Default" means using the global default quota; click the edit icon to set a specific quota for this user. |
|Join time |The time when this user first joined and used the AI model. |


<span id="woeSjBhb"></span>
## Search and filter

The page provides search and filter functions. You can enter the user name, email, or phone number in the search box to quickly locate the target user.

<span id="W4ToWIrq"></span>
## View the branch's total token usage

You can view the branch's total token usage information on the branch's **Usage statistics and monitoring** page. For more details, refer to [Viewing branch details](https://docs.byteplus.com/en/docs/aidap/Supabase-Viewing_branch_details?_vtm_=a106466.b106468.0_0.0_0.0.1542_7610626577593304630).
