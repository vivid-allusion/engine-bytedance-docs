---
title: "Quota management"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Quota_management"
---

The **permissions and quotas** page allows viewing and managing each user's sandbox creation quotas under the current branch, including setting the default daily sandbox quota per user, and viewing each user's sandboxes created today, total sandboxes created, and current daily quota.

<span id="YGrBETka"></span>
## Background


* The daily sandbox quota counts by "user × calendar day" and resets the sandboxes created today at 0:00 every day.

* The platform provides a unified "default daily sandbox quota" for all users and supports setting quotas individually for specific users (including "unlimited").

* When a user reaches their daily quota for sandbox creation, they cannot create more sandboxes until the next day when the quota resets or until an administrator adjusts their quota.


<span id="Nti98tf7"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target current branch is in **running** status.

* The current account has sandbox service management permissions (view and modify default quotas).


<span id="uz1u2SJK"></span>
## Procedure

<span id="GB2y65FW"></span>
### Check sandbox quota


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, select **Sandbox service** \> **Permissions and quotas** tab.

   The top of the page shows the **Default daily sandbox quota per user**. The list below displays each user's sandbox usage in the current branch, including sandboxes created today, total sandboxes created, daily quota, and join time.


<span id="FJj2phZC"></span>
### Search user

Enter user name, user ID, or email in the search box above the list to automatically filter matching users.

<span id="mjGDb4Td"></span>
### Modify default daily sandbox quota


1. Click the edit icon to the right of the **Default daily sandbox quota per user**.

2. Select the quota type in the pop\-up edit dialog box:

   * **Specific amount**: Enter the number of sandboxes each user can create daily in the input box (unit: sandboxes/day), with a default value of 100.

   * **Unlimited**: No limit on the number of sandboxes each user can create daily.

3. Click **OK** to save. The new default quota takes effect immediately for users without individually set quotas.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The default quota serves as a fallback setting for all users. Users with individually set quotas (such as set to "Unlimited") follow their individual settings and are not affected by default quota adjustments.   </div>
   

<span id="MzZeKZXF"></span>
## Field description


|**Field** |**Decscription** |
|---|---|
|User |User name, for example, System Admin. |
|Sandboxes created today |The number of sandboxes this user has created today (calendar day). |
|Total sandboxes created |The total number of sandboxes this user has created. |
|Daily quota |The user's current effective daily sandbox creation quota. The value is a specific amount (such as 100) or "Unlimited". |
|Join time |The time the user joined the current workspace or branch. It displays "\-" if not recorded. |


<span id="o2waKsGj"></span>
## Precautions


* **Sandboxes created today** is calculated by calendar day and resets automatically at 0:00 daily. **Total sandboxes created** is cumulative and does not reset.

* After adjusting the default quota to **Unlimited**, all users without individually set quotas will no longer be restricted by daily creation limits. Proceed with caution.

* When a user reaches the daily creation quota and tries to create another sandbox, the attempt will fail. They must wait for the quota to reset the next day or have their quota adjusted by an administrator.
