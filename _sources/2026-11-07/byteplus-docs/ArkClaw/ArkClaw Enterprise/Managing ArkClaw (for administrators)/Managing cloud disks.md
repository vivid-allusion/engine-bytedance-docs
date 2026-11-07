---
title: "Managing cloud disks"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Cloud_Drive_Management"
---

Cloud disk management allows you to see how much storage your ArkClaw cloud disk is using, as well as allocate disk space to your entire organization, its teams, and individual employees. The administrator can filter employees by department and see who can use the enterprise cloud disk. The administrator can also assign or adjust capacity based on the remaining quota.

<span id="9kiFRlBN"></span>
## Notes


* Only accounts with cloud disk management permissions can adjust the capacity settings.

* Adjusting employee capacity settings will use the remaining quota, so first check if there is enough capacity available.

* An empty state occurs when the organizational structure has not been synchronized or when there is no manageable data.

* This feature is only available for ArkClaw instances that are created after a cloud disk is set up.


<span id="n65rxXMB"></span>
## Set up an ArkClaw cloud disk


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Cloud disk management".

3. On the "Network disk management" page, click "Enable now" to set up an ArkClaw cloud disk. Once enabled, you will have access to features such as cloud storage and intelligent document management.


<span id="52tuwQvF"></span>
## View cloud disk information


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Cloud disk management".

3. On the "Network disk management" page, view the following information: "Total space capacity", "Allocated space", "Used", number of assigned employees, and "Remaining allocatable total space".



|Parameter |Description |
|---|---|
|Total space capacity |Total space capacity = Sum of cloud disk quotas for all purchased seats. Total space capacity can be reallocated. The default [capacity quota per seat for the different editions](https://docs.byteplus.com/en/docs/ArkClaw/Billing_instructions?lang=en#Q8ldd5U3) is as follows:<br><br>**Starter edition**: 10 GB.<br><br>**Standard edition**: 20 GB.<br><br>**Premium edition**: 40 GB.<br><br>**Ultimate edition**: 80 GB.<br><br>Expanding storage capacity is not currently supported. |
|Space allocation |The amount of capacity that has been allocated from the total space capacity. |
|Used |The total amount of space capacity used. |
|Remaining allocatable total space |The amount of capacity still available for allocation from the total capacity. |


<span id="31GaYxUa"></span>
## View space information

<span id="KSx8vJ9U"></span>
### Team cloud disks

A team cloud disk is a shared space with permission controls that enable collaboration among multiple users. There are two types: enterprise and team.


* Enterprise cloud disk: A space that stores files for the entire organization and is visible to all employees. Through permission management, the administrator can configure user and user group access to the space and specific directories. An organization can only have one enterprise cloud disk.

* Team cloud disk: A space created for a specific user group or project for file storage and collaboration. The administrator can create multiple team spaces in the admin console.

1. On the "Network disk management" page, click "Team drive".

2. On the "Team drive" tab, view the following information: space name, space allocation, used space, remaining space, and usage ratio.


<span id="Zm5C8Mj3"></span>
### Personal cloud disks

A personal cloud disk is an independent space that is only visible to the employee themselves.


1. On the "Network disk management" page, click "Employee Personal Cloud Drive".

2. In the upper\-right corner of the "Employee Personal Cloud Drive" tab, you can click different tabs to change the view.

   * "User group staff configured": Select a department on the left to view its members' quota configuration on the right.

   * "Full list": Displays the quota configuration of all employees. You can search for specific employees by name using the search box.


<span id="LWwt2pWR"></span>
## Configure capacity

<span id="UyOaQ7Bc"></span>
### Configure team capacity

You can assign cloud disk capacity to a specific team, or adjust an existing allocation.


1. On the "Network disk management" page, click "Team drive".

2. On the "Team drive" tab, find the team cloud disk you want to edit and click "Capacity configuration" in the "Operation" column.

3. In the "Team Cloud Drive Capacity configuration" dialog box, specify the capacity you want to assign. The key information in the dialog is explained below.

   
   |**Parameter/Section** |**Description** |
   |---|---|
   |Space name |Displays the name of the space to which you are allocating capacity. |
   |Please adjust Total Capacity |Specify how much cloud disk capacity you want to allocate to the space. The unit is GB. The default value is 10 GB, and the range extends from 1 GB to the remaining quota. |
   |Change preview |Dynamically displays the impact of this adjustment based on the value you entered.<br><br>"Total space": Displays the total capacity for the space after the adjustment, as well as the amount of the change.<br><br>"Used": Displays the amount of capacity used and its percentage.<br><br>"Remaining available space": Displays the available capacity after the adjustment, as well as the amount of the change.<br><br>"Remaining allocatable total space": Displays the amount of capacity still available for allocation from the total capacity after the adjustment, as well as the amount of the change. |
   

4. The page will refresh automatically once the capacity configuration is complete. You can confirm this by doing one of the following:

   * A message will appear at the top of the "Network disk management" page that says, "Team Cloud Drive Capacity configuration updated successfully".

   * "Remaining allocatable total space" at the top of the "Network disk management" page will reflect the new value.

   * "Allocate space" for the corresponding team on the "Team drive" tab will also show the new capacity value.


<span id="zCLxDKGN"></span>
### Configure employee capacity

You can assign cloud disk capacity to a specific employee, or adjust an existing allocation.


1. On the "Network disk management" page, select "Employee Personal Cloud Drive \> User group staff configured/Full list".

2. Under "Employee quotas", find the employee you want to edit and click "Capacity configuration" in the "Operation" column.

3. In the "Capacity configuration" dialog box, specify the capacity you want to assign. The key information in the dialog is explained below.

   
   |**Parameter/Section** |**Description** |
   |---|---|
   |Employee name |Displays the name of the employee to whom you are allocating capacity. |
   |Please adjust Total Capacity |Specify how much cloud disk capacity you want to allocate to the employee. The unit is GB. The default value is 10 GB, and the range extends from 1 GB to the remaining quota.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The amount of capacity allocated to the employee must not exceed the remaining quota. If it does, the configuration cannot be submitted.</div><br> |
   |Change preview |Dynamically displays the impact of this adjustment based on the value you entered.<br><br>"Total staff space": Displays the total capacity for the employee after the adjustment, as well as the amount of the change.<br><br>"Employees have used": Displays the capacity used by the employee and its percentage.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">"Employee surplus available": Displays the available capacity for the employee after the adjustment, as well as the amount of the change.</div><br><br><br>"Remaining allocatable total space": Displays the change in the remaining quota of the enterprise cloud disk after this adjustment. |
   

4. The page will refresh automatically once the capacity configuration is complete. You can confirm this by doing one of the following:

   * A message will appear at the top of the "Network disk management" page that says, "Capacity configuration updated successfully".

   * "Remaining allocatable total space" at the top of the "Network disk management" page will reflect the new value.

   * "Total space" for the corresponding employee on the "Employee space" tab will also show the new capacity value.


<span id="s90DNHsT"></span>
## Configure the ArkClaw cloud disk


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Cloud disk management".

3. On the "Network disk management" page, click "Cloud Drive Configuration" in the upper\-right corner.

4. On the "Cloud Drive Configuration" page, you can enable or disable the "Semantic Search" feature. With it turned on, you can find images, documents, and audio/video files using just one sentence to get accurate results.


<span id="OnyI9lFT"></span>
## Configure team cloud disk permissions


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Cloud disk management".

3. On the "Network disk management" page, click "Team drive".

4. On the "Team drive" tab, find the team cloud disk you want to edit and click "Permission configuration" in the "Operation" column.

5. The permission management page for the team cloud disk opens. Click "Edit General Permissions" in the upper\-right corner to make the necessary changes.

   
   |Parameter |Description |
   |---|---|
   |Current configuration object |The cloud disk space that you are configuring is displayed by default. |
   |Authorization Type |Select the permission configuration method:<br><br><br>* All Types: Set the permission scope uniformly for all operation types on this resource.<br><br>* Split Type: Set permission scopes separately for operations such as reading, listing, uploading, and deleting files. |
   |Permission scope |Select the desired permission scope: "Allow All", "Controlled Access", or "Deny All".<br><br>If you select "Controlled Access", specify the authorized users.<br><br><br>* Switch between the "Department", "User group", or "User" tab and select the desired users.<br><br>* The selected users will appear in the right panel. Click the  **×**  icon to remove an individual user or the trash can icon to clear them all.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the effective scope is set to all users, a department, or a user group, the permissions are dynamic and newly added members automatically inherit them.</div><br> |
   

6. After confirming everything is correct, click **OK** to save the changes. To discard the changes, click **Cancel**.


<span id="xHeXA6Ya"></span>
## Add a team cloud disk


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Cloud disk management".

3. On the "Cloud disk management" page, select "Team Drive \> Add Team Cloud Drive".

4. On the "Add Team Cloud Drive" page, configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Select team |The team cloud disk that you create will be named in the following format: Team Name + Team Cloud Disk.<br><br>Each team can create one dedicated team cloud disk.<br><br>If a team has not yet been created, click "Create team" on the right to do so. For more information, see [Managing department information](https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments). |
   |Space default permissions |Select the permissions you need: "Read File", "List File", "Upload File", and "Delete File".<br><br>They apply to all users in the team and cannot be set separately for individual users within a user group.<br><br>To assign different permissions to different team members, go to Permission management \> Cloud Drive Space. Alternatively, access this quickly from the team cloud disk permission configuration. You can also grant external members access to the dedicated space with different permission levels. |
   |Space Default Capacity |Specify how much cloud disk capacity you want to allocate to the team cloud disk. The range extends from 1 GB to the remaining quota. |
