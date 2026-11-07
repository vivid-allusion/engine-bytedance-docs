---
title: "Detailed Explanation of Permission Features"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Detailed_Explanation_of_Permission_Features"
---

<span id="_1-新建项目"></span>
# 1. Create a project

Only system administrators can create projects. If other users attempt to create a project, a no\-permission warning will be displayed.

<span id="_2-项目信息"></span>
# 2. Project information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0829d6cd4aeb4ea0b18136f578e37744~tplv-goo7wpa0wc-image.image) </span>

See [Project Information](https://docs.byteplus.com/docs/DataWind/Project_Information) for details. The following section provides a detailed explanation of project types and project control levels.

<span id="项目类型"></span>
## Project types


| |**Usage scenarios** |**What does this affect?**  |
|---|---|---|
|**Confidential project** |For projects with higher permission requirements, it is not desirable for users from other departments to view the project space. |* Only the project administrator can add members.<br><br>* Except for the project administrator, the project cannot be found in the project search box.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0c29ad0816f4bfda4e695893b23c884~tplv-goo7wpa0wc-image.image) </span><br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5fb61b23a4345e59fe2696fec43b1b7~tplv-goo7wpa0wc-image.image) </span> |
|**Non\-confidential project** |The project can be made public within the group. |Users can search for the project and proactively find the project administrator to apply to join the project. |


<span id="_2-1-项目管控程度"></span>
## 2.1 Project control levels


| |**Personal dashboard** |**Personal dashboard** |**Personal dashboard** |**Public dashboard** |**Public dashboard** |**Public dashboard** |
|---|---|---|---|---|---|---|
|**Control mode** |**Is it possible to create new items** |**Who holds the management permissions** |**Can the administrator grant permissions to others** |**Is it possible to create new items** |**Who holds the management permissions** |**Can the administrator grant permissions to others** |
|Standard mode |✅ |The creator is set as the administrator by default. |✅ |✅ |The creator is set as the administrator by default. |✅ |
|Moderate mode |✅ |The creator is set as the administrator by default. |❌ |✅ |The project administrator is set as the administrator by default, and the creator has edit permissions. |✅ |
|Strict mode |❌ |\-\- |❌ |✅ |The project administrator is set as the administrator by default, and the creator has edit permissions. |✅ |


(1) After switching the project control level, the management permissions for newly created resources will be handled according to the new mode. The management permissions for historical resources created before the switch will remain unchanged and will not be updated retroactively. It is recommended not to switch the project control status frequently.

(2) In medium and strict modes, the authorization button for personal dashboards is not disabled, but after operations from the administrator or regular user perspective, users will be reminded that authorization is not allowed.

<span id="_3-项目权限"></span>
# 3. Project permissions

<span id="_3-1-权限概览"></span>
## 3.1 Permission overview


|**Project permission types** |**Explanation and notes** |
|---|---|
|**Search list** |Permission to determine whether the xx project can be found in the top navigation project options list<br><br><br>* Only the top search bar is available in private deployment environments<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9177b00b39ec441db05131fee00f4866~tplv-goo7wpa0wc-image.image) </span><br><br>* In the SaaS environment, in addition to searching via the top navigation bar mentioned above, you can also search from the homepage. Items without permission can be grayed out.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a658964e6724249a533b9a2b7f10d36~tplv-goo7wpa0wc-image.image) </span><br><br>   Caution:<br><br>* It is necessary to distinguish between confidential and non\-confidential projects.<br><br>* Sort by app_id. |
|<span id="无权限"></span><br>### **No permission** |Indicates that project view permission is not available |
|<span id="查看"></span><br>### **View** |Has permission to access the project, with the following permissions:<br><br><br>* Can view resources within the project for which permission is granted<br><br>* Can create **personal** dashboards or folders and perform related operations<br><br>* Can create public dashboards or folders in public folders **with edit permissions**<br><br>* **Cannot** create public folders or public dashboards in the **root directory** of public folders<br><br>* Can create folders or datasets in folders **with edit permissions**<br><br>* **Cannot** create folders or datasets in the **root directory** of datasets<br><br>   Note:<br><br>* Project view permission + edit permission for a public folder = ability to create public folders or dashboards in that public folder<br><br>* An error will occur after clicking Confirm when creating in the root directory |
|<span id="编辑"></span><br>### **Edit** |Includes the above viewing permissions, and also includes:<br><br><br>* Can create public dashboards, public folders, and datasets in the **root directory**<br><br>* Create user attributes<br><br>   Note:<br><br>* Dashboards can only be created in public folders **with edit permissions**<br><br>* Datasets can only be created in folders **with edit permissions** |
|<span id="全局查看"></span><br>### **Global view** |Includes the above editing permissions, and also includes:<br><br><br>* Can view all public dashboards, public dashboard folders, and datasets within the project, and **view all data**<br><br>* **Can view all personal dashboards via personal dashboard links, but the dashboard list will not display all personal dashboards**<br><br>   Note:<br><br>* Dashboards can only be created in public folders **with edit permissions**<br><br>* Datasets can only be created in folders **with edit permissions** |
|<span id="管理"></span><br>### **Manage** |* You can manage permissions for all resources within the project (the private deployment version also supports project deletion)<br><br>   Note:<br><br>* Dashboards can be created in all public folders |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>1. Affects the permission configuration of the search list</strong></div>


<div data-tips="true" data-tips-type="warning">Project information \-\-\> Project type</div>



* <div data-tips="true" data-tips-type="warning">Non\-confidential project (searchable by all users)</div>


* <div data-tips="true" data-tips-type="warning">Confidential project (searchable only by authorized users)</div>


   <div data-tips="true" data-tips-type="warning">2. Different control modes will result in different permissions; see Project Information \-\-\> Project Control Level as described above for details   </div>
   


<span id="_3-2-如何获取？"></span>
## 3.2 How to obtain?


|Methods for obtaining project permissions |Operation |Operators |Remarks |
|---|---|---|---|
|**Project administrator proactively grants permissions** |1. Project Center \- User Management \- Add user, assign project permissions<br><br>2. Project Center \- Permission Management, assign project permissions to the target user |Project administrator | |
|**Project permissions are obtained by acquiring other resources** |Other users grant Xiaoming permissions for dashboard/dataset/visual modeling tasks; when Xiaoming logs in, project read permission is automatically obtained |Resource administrator | |
|**Obtained by being added to a user group** |Add the user to the xxx user group, and configure project permissions in the User Group Details \- Permission Management tab |User group/project administrator |1. **Not applicable if group\-based permission blocking is enabled**<br><br>2. There will be a delay for both granting and revoking user group permissions |
|**Obtained by being added as a role member** |Add the user to the xxx role, and configure project permissions in the Role Details \- Permission Management tab |Role/project administrator |1. **Not applicable if group\-based permission blocking is enabled** |


<span id="_4-仪表盘权限"></span>
# 4. Dashboard permissions

<span id="_4-1-权限概览"></span>
## 4.1 Permission overview


|**Dashboard permission types** |**Explanation** |
|---|---|
|**List display permission** |Items displayed in the **left\-side list** of the dashboard module |
|<span id="仅阅览"></span><br>### View only |1. View data<br><br>2. Chart function buttons: Create monitor<br><br>3. Dashboard function buttons: Create new subscription [personal only], add bookmark, embed dashboard, and so on<br><br>4. **Not allowed** to download or copy data **on charts** |
|<span id="查看"></span><br>### View |In addition to the above view\-only permissions, also includes:<br><br><br>1. Chart function buttons: Copy, download data<br><br>2. Dashboard function buttons: Favorite, export image |
|<span id="编辑"></span><br>### Edit |Includes the above viewing permissions, as well as:<br><br><br>1. Edit basic information and view dashboard access statistics<br><br>2. Editable dashboard: add components within the canvas, delete charts, adjust layout, set linkage, configure jumps, and more<br><br>3. Editable charts [requires dataset viewing permissions as well]<br><br>4. Charts can be copied on the dashboard editing page [dataset view permission is also required] |
|<span id="管理"></span><br>### Management |Includes the above editing permissions, as well as:<br><br><br>1. Permission management and owner transfer<br><br>2. Advanced subscription [individual/group]<br><br>3. Move, copy, or delete dashboard and other operations |


<span id="_4-2-影响权限的设置有哪些？"></span>
## 4.2 What settings affect permissions?

**1. Permissions for list display**

**Project Center \- Project Information \- Dashboard display rules**


* All dashboards (all **public dashboards** within the project are displayed. Clicking on dashboards without permission will prompt a no\-permission message, and users can apply for access.)

* Only dashboards you have access to


**2. Permissions for view\-only, view, edit, and manage**


* **Dashboard types**

   * Personal dashboards can only be granted view\-only or view permissions; edit or manage permissions cannot be granted.

   * Public dashboards can be granted view\-only, view, edit, or manage permissions.

* **Row and column permissions**

   * In certain scenarios, if row and column permissions are set for a dataset, users may not be able to see some chart data even if they have dashboard permissions.


<span id="_4-3-涉及页面说明"></span>
## 4.3 Description of related pages


* No dashboard permission illustration:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6deea8b789db4882a6eba5d32e775666~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Chart function button illustration:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c66f679eb3c4691b174bf85eff58a0d~tplv-goo7wpa0wc-image.image) </span>


* Dashboard function button illustration:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfb4a206fa7e4223bb36d9fb5255efb3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7fb928495214cf2b179b77246f07cf5~tplv-goo7wpa0wc-image.image) </span>


* Dashboard edit page illustration:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65468690a2474fdca19be9a01ce48cad~tplv-goo7wpa0wc-image.image) </span>


* Dashboard left\-side list function illustration:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fea6bb1f6b3415fb8cacbc68f9ef712~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Single chart resources cannot be authorized</div>


2. <div data-tips="true" data-tips-type="warning"><strong>Cannot grant others editing or management permissions for personal dashboards</strong></div>


3. <div data-tips="true" data-tips-type="warning">In medium/strict mode, personal dashboards cannot be authorized</div>



<span id="_4-4-如何获取？"></span>
## 4.4 How to obtain?


|Methods for obtaining dashboard permissions |Operation |Authorized personnel |Remarks |
|---|---|---|---|
|<span id="资源-项目管理员主动授权"></span><br>### Resource/project administrator proactively grants permissions |1. Single resource authorization dialog in the upper right corner of the resource [applies to both personal and public dashboards]<br><br>> The single resource authorization dialog can grant permissions to any member, user group, role, or 飞书 group within the project<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6000b45d20344b869b5ed89b1dfeb246~tplv-goo7wpa0wc-image.image) </span><br><br><br>2. Project Center \- Resource Permissions [applies to both personal and public dashboards]<br><br>> In Resource Permissions, click Authorize/Permissions Management to grant permissions to others<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f2607db558940579649f942dca19951~tplv-goo7wpa0wc-image.image) </span><br><br><br>3. Project Center \- Permissions Management [applies to public dashboards only, only project administrators can operate]<br><br>> In Permissions Management, select the target user and grant dashboard permissions<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4527d42c0243ec96b490196f15f572~tplv-goo7wpa0wc-image.image) </span> |Resource administrator [Methods 1.2]<br><br>Project administrator [Methods 1.2.3] | |
|<span id="通过加入用户组获取"></span><br>### Obtained by joining a user group |Add the user to the xxx user group, and configure the target dashboard in the user group details \- Permissions Management tab [applies to public dashboards only] |User group/project administrator |1. User group administrators can only configure public dashboards **for which they have management permissions**<br><br>2. The member list of department user groups cannot be configured and is automatically adapted based on the organizational structure<br><br>3. **Not applicable if group authorization blocking is enabled**<br><br>4. There will be a delay for both user group authorization and deauthorization |
|<span id="通过加入角色成员获取"></span><br>### Obtained by adding role members |Add the user to the xxx role, and configure the target dashboard in the role details \- permission management tab [only applicable to public dashboards]<br><br>Configure resource permissions for the role and set role members<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65eeb255f33e45d5a01429f18cc67e15~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e310708bddfe4b67b61c458c556706fa~tplv-goo7wpa0wc-image.image) </span><br><br>Caution: The prerequisite is that a resource administrator or higher role has already authorized the role for the dashboard; only then will the resource permission category appear in role management. |Role/project administrator |1. Role administrators can only configure public dashboards **for which they have management permissions**<br><br>2. **Not applicable if group authorization blocking is enabled**<br><br>3. Special case: Folders without permissions will also be displayed, but when selected for authorization, a no\-permission prompt will appear<br><br>   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2466dc891dc36ce03fe067786a380e29) </span> |
|<span id="通过文件夹权限继承而来"></span><br>### Inherited through folder permissions |Dashboard permissions are inherited by obtaining permissions for the dashboard folder<br><br><br>* Folders on resources are directly authorized, and dashboards within the folder are authorized by default<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d3e2582ba3c420c8d3d33e269d46b4e~tplv-goo7wpa0wc-image.image) </span><br><br>* Project Center \- Permission Management<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/097f49c151e944f190a7333446a24e61~tplv-goo7wpa0wc-image.image) </span><br><br>* Project Center \- Resource Management<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58db31b60ba94c83b7f730bb589c1983~tplv-goo7wpa0wc-image.image) </span> |Folder/project administrator |Inheritance logic, see the folder section below |


<span id="_5-数据集权限"></span>
# 5. Dataset permissions

<span id="_5-1-权限概览"></span>
## 5.1 Permission overview


|**Dataset permission types** |**Explanation** |
|---|---|
|**List display permission** |Items displayed in the left\-side list of the dataset module \*\*\*\* |
|<span id="仅阅览"></span><br>### View only |1. Data can be viewed<br><br>2. Datasets can be added to favorites<br><br>3. You can view dataset details (data preview, model information, lineage view)<br><br>4. You can perform queries and add temporary fields on the visual query page<br><br>5. Chart function button: Copy to dashboard action [dashboard view\-only permission is also required]<br><br>6. **Not allowed** to perform download or copy data operations **on the chart** |
|<span id="查看"></span><br>### View |In addition to the above view\-only permissions, also includes:<br><br><br>1. Data can be copied on the **visual query page**<br><br>2. On the **visual query page**, you can download, configure monitoring, and perform other operations<br><br>3. On the dashboard editing page: Copy chart [dashboard editing permission is also required] |
|<span id="编辑"></span><br>### Edit |In addition to the above view permissions, also includes:<br><br><br>1. Ability to edit basic dataset information<br><br>2. Ability to create usage instructions, visual query configurations, and set tags<br><br>3. Ability to modify dataset models, routine configurations, and other operations<br><br>4. Ability to copy datasets [requires data connection permission for the dataset] |
|<span id="管理"></span><br>### Manage |In addition to the above edit permissions, also includes:<br><br><br>1. Ability to manage permissions and transfer ownership<br><br>2. Ability to move or delete datasets, and other operations<br><br>3. Ability to configure row and column permissions |


<span id="_5-2-影响权限的设置有哪些？"></span>
## 5.2 What settings affect permissions?

 **(1) Permissions for list display**

**Project Center \- Project Information \- Dataset display rules**


* All datasets (All **datasets** within the project are displayed. If you do not have permission, clicking will display a no\-permission message, and you can request permission.)

* Only datasets you have permission to access


 **(2) For view, browse, edit, and manage permissions only**


* There is no distinction between public and personal datasets. Authorization can be performed under any control mode.

* Row and column permissions

   * In certain scenarios (as below), if row and column permissions are set for a dataset, users may not be able to preview or perform visual queries even if they have dataset permissions.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6deea8b789db4882a6eba5d32e775666~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_5-3-权限涉及页面"></span>
## 5.3 Pages involving permissions


* No dataset permission illustration

* No permission illustration for accessing the visualization page:

* Visualization query page feature illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3892756cde6f40fbb8c289fa2bc40153~tplv-goo7wpa0wc-image.image) </span>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2099b12e25064d24b16e67a9e413b597~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/959a715d651e47c9a6d6bc021df1790e~tplv-goo7wpa0wc-image.image) </span>


* Dataset details illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/069d9b72a52d4418ab6764824bf2d9e0~tplv-goo7wpa0wc-image.image) </span>

* Dataset editing feature illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe751c3ce42414e8bf7b4ec145c1a08~tplv-goo7wpa0wc-image.image) </span>

* Dataset left\-side list feature illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/380f20ce8b4b4bd78bef4904a670db00~tplv-goo7wpa0wc-image.image) </span>

* Copy to dashboard feature button illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48e71f64e6074e88bede9542cfcbe040~tplv-goo7wpa0wc-image.image) </span>

* Copy chart to dashboard editing page illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c27000d7b262433fa937951f2d542ca8~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">The download feature on the visual query page requires view permission for the dataset</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/959a715d651e47c9a6d6bc021df1790e~tplv-goo7wpa0wc-image.image" width="1562px" />   </div>
   


<div data-tips="true" data-tips-type="warning">The download feature on the dashboard page also requires view permission for the dashboard</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f04453e17e945849057b0d6cded3ade~tplv-goo7wpa0wc-image.image" width="1596px" /></div>



2. <div data-tips="true" data-tips-type="warning">An error will occur when copying a dataset if there is no data connection permission</div>


3. <div data-tips="true" data-tips-type="warning">Copying a dashboard requires dashboard management permission; copying a dataset only requires dataset edit permission</div>



<span id="_5-4-如何获取？"></span>
## 5.4 How to obtain permission?


|Methods for obtaining dataset permissions |Operation |Eligible operators |Remarks |
|---|---|---|---|
|<span id="资源-项目管理员主动授权"></span><br>### Resource/project administrator actively grants authorization |1. Single resource authorization pop\-up in the upper right corner of the resource<br><br>> The single resource authorization pop\-up allows authorization for any member, user group, role, or Feishu group within the project<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5906cce25f3c48e9a498a1bd1037a91b~tplv-goo7wpa0wc-image.image) </span><br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c28cb7eef56842b593d6e3687af64cbf~tplv-goo7wpa0wc-image.image) </span><br><br><br>2. Project center \- Resource permissions<br><br>> In Resource Permissions, click Authorize or Permission Management to authorize others<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58db31b60ba94c83b7f730bb589c1983~tplv-goo7wpa0wc-image.image) </span><br><br><br>3. Project center \- Permission management [Project administrators only]<br><br>> In Permission Management, select the target user and grant dataset permissions<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/097f49c151e944f190a7333446a24e61~tplv-goo7wpa0wc-image.image) </span> |Resource administrator [Path 1.2]<br><br>Project administrator [Path 1.2.3] | |
|<span id="通过加入用户组获取"></span><br>### Obtained by joining a user group |Add the user to the xxx user group, and configure the target dataset in the Permission Management tab of the user group details |User group administrator/project administrator |1. User group administrators can only configure datasets **for which they have management permissions**<br><br>2. The member list of department user groups cannot be configured and is automatically adapted according to the organizational structure<br><br>3. **Not applicable if group authorization blocking is enabled**<br><br>4. There will be a delay when granting or revoking user group authorizations |
|<span id="通过加入角色成员获取"></span><br>### Obtain by adding role members |Add users to the xxx role, then configure the target dataset in the role details—Permission Management tab<br><br>Configure resource permissions for the role and set role members<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65eeb255f33e45d5a01429f18cc67e15~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d5421ca0d8043d5ae8cd4d54305245c~tplv-goo7wpa0wc-image.image) </span><br><br>Caution: The prerequisite is that a resource administrator or higher must first authorize the resource; only then will the resource permission category appear in role management. |Role/project administrator |1. Role administrators can only configure **datasets they have management permissions for**<br><br>2. **Not applicable if block group authorization is enabled**<br><br>3. Special case: Folders without permissions will still be displayed, but when selected for authorization, a no\-permission prompt will appear<br><br>   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e89ead171ed68fae5d64deaf0150ff95) </span> |
|<span id="通过文件夹权限继承而来"></span><br>### Inherited through folder permissions |Obtain dashboard permissions by inheriting folder permissions<br><br><br>* Directly grant permissions to a folder on a resource; datasets within the folder are authorized by default<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5906cce25f3c48e9a498a1bd1037a91b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Project Center—Permission Management<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c28cb7eef56842b593d6e3687af64cbf~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Project Center—Resource Management<br><br>> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58db31b60ba94c83b7f730bb589c1983~tplv-goo7wpa0wc-image.image) </span> |Folder/project administrator |Inheritance logic |


<span id="_6-数据行列权限"></span>
# 6. Dataset row and column permissions

<span id="_6-1-权限概览"></span>
## 6.1 Permission overview


|**Row and column permission types** |**Explanation** |**Settings/configuration that affect permissions** |
|---|---|---|
|<span id="行权限"></span><br>### Row permissions |Control which rows of a field xxx users can or cannot view |1. **Configuration methods are divided into fixed values and dynamic values.** <br><br>   1. Fixed value<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b2adbccad744ed0910a90549e105b1b~tplv-goo7wpa0wc-image.image) </span><br><br>   2. Dynamic value (used with user attributes)<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65f09cf6f1c04815b910c61b0be29274~tplv-goo7wpa0wc-image.image) </span><br><br>2. **Allowlist/blocklist configuration—only affects row permissions; does not apply to column permissions**<br><br>   1. Applies only to row permissions, not to column permissions.<br><br>   2. **Off**: Only users on the allowlist/blocklist can view the data, and the visible range is determined by the configured rules. Users not on any list cannot view any data.<br><br>   3. **On**: Users on the list are **restricted** and can only view data within the configured rules. Users not on the list can view all row data.<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd7f28374b14499ab0a7fbf08c76337d~tplv-goo7wpa0wc-image.image) </span><br><br>3. **AND/OR rule configuration**<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bd53fe54af240b994749742ff17aa80~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3323d43006c44b879dd5996181005eb3~tplv-goo7wpa0wc-image.image) </span> |
|<span id="列权限"></span><br>### Column permissions |Control so that only specific users can view a particular column of the dataset. |1. **Can be configured on model (base table) fields or dataset fields.** <br><br>   1. If a sensitive column is configured on a model field, all dataset fields derived from that model field will be affected.<br><br>   2. If a sensitive column is configured on a dataset field, it affects controlled users' access to that dataset field, but does not affect their access to the corresponding model field.<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29a4888ff97f45dc9800e982c2dff168~tplv-goo7wpa0wc-image.image) </span> |


<span id="_6-2-权限涉及页面"></span>
## 6.2 Pages involving permissions


* Row and column permission configuration entry illustration [visible only to administrators]


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0e2894fce6a42a1b04f5d048a9b4cbf~tplv-goo7wpa0wc-image.image) </span>


* Row and column permission illustration


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b69b236d82334cafbee3fcf155311a1d~tplv-goo7wpa0wc-image.image) </span>


* How to determine whether row and column permissions are restricting access?

   * No row permission illustration

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6deea8b789db4882a6eba5d32e775666~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

   * No column permission / only partial row permission


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning"><strong>Dataset permissions vs. row and column permissions</strong></div>


2. <div data-tips="true" data-tips-type="warning">Does having dataset permissions mean having row and column permissions? No！ When row and column permission restrictions are enabled for a dataset, having dataset permissions does not mean you can view the data; you also need to apply for row and column permissions.</div>


3. <div data-tips="true" data-tips-type="warning">Does having row and column permissions mean having dataset permissions? No！ Even if you have row and column permissions, to access the visual query page for ad hoc analysis, you still need to apply for dataset permissions.</div>


4. <div data-tips="true" data-tips-type="warning">When configuring row and column permissions, use the <strong>simulation verification feature</strong> to quickly verify whether user permissions are configured correctly!</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0389f358d334f65a34f2632fc52244c~tplv-goo7wpa0wc-image.image" width="2938px" />   </div>
   

5. <div data-tips="true" data-tips-type="warning">Do column permissions affect visualization?</div>



<div data-tips="true" data-tips-type="warning">For example, in a table visualization, if a sensitive column is included in the select clause, it does not affect the visualization. However, if it is included in the group by or where clause, it will affect the visualization, causing the chart to not display. Other visualization types may have stricter logic than tables.</div>


<span id="_6-3-如何获取？"></span>
## 6.3 How to obtain permission?

See [Permission settings](https://docs.byteplus.com/docs/DataWind/Getting_Started_Guide_for_Administrator#d3d9053b)\-\-Enable dataset row and column permissions

<span id="_6-4-权限模拟验证"></span>
## 6.4 Permission simulation verification

When configuring row and column permissions, use the **simulation verification feature** to quickly verify whether user permissions are configured correctly, see [3.7 Permission simulation and verification](https://docs.byteplus.com/docs/DataWind/109982#_3-7-%E6%9D%83%E9%99%90%E6%A8%A1%E6%8B%9F%E9%AA%8C%E8%AF%81).

<span id="_7-数据连接权限"></span>
# 7. Data connection permissions

**Create**: Except for regular users and users with project view\-only permissions, all other users can create data connections.

**Authorization acquisition method**: Resource/project administrators can click 'Authorize' in the upper right corner of the data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f266b8e1e394ff3901a8fa441a1d6f1~tplv-goo7wpa0wc-image.image) </span>

**Authorization scope:**  Authorization can be granted to users or user groups.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99b6027036954bc8a937d6c3e2943ffa~tplv-goo7wpa0wc-image.image) </span>


|**Permission types** |**Explanation** |
|---|---|
|**View** |* You can view the data connection.<br><br>* You can select the data connection when creating a new dataset. |
|**Edit** |In addition to the above view permissions, you can edit the information of the data connection. |
|**Manage** |In addition to the above edit permissions, you can modify the authorization for the data connection. |


<span id="_8-如何批量授权？"></span>
# 8. How to perform batch authorization?

You can first write the usernames in a text field, separated by commas, and then add users in bulk.

<span id="_9-引用权限是什么作用？"></span>
# 9. What is the purpose of reference permissions?

This is equivalent to copying the user list and corresponding permission settings. For example, if both user A and user B have edit permissions for a dashboard, when assigning the dashboard's permissions to a dataset, you can set user A and user B to have edit permissions for that dataset as well.
