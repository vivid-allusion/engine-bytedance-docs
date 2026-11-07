---
title: "Detailed Explanation of User Permissions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Detailed_Explanation_of_User_Permissions"
---

This article provides a detailed introduction to the types of permissions, permission\-related pages, and how to obtain each type of permission for every functionality.

<span id="9d5715ba"></span>
# Function overview

DataAgent product permissions include the following functionalities:


|Permission types |Permission types |Permission features |Introduction |
|---|---|---|---|
|Asset permissions |Project resource permissions |[Project permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#942d5402) |Permissions for creating, searching, viewing, editing, global viewing, and managing projects. |
|||[Dataset permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#874a55c6) |Permissions for creating datasets, list display scope, read\-only, viewing, editing, and managing. |
|||[Visual modeling permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#44c9b764) |Permissions for viewing, editing, and managing visual modeling tasks. |
|||[Data connection permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#7ec0110a) |View, edit, and manage permissions for data connections. |
||Agent permissions |[Agent permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#4efb3f5c) |Usage and management permissions for agents (including create, configure, delete, and more).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">To use an agent configured with a specific dataset, the user must have at least view permission for that dataset.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">To configure a dataset for an agent, the user must also have at least view permission for that dataset.</div><br> |
|Data permissions |Row and column permissions for data |[Row and column permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#f3ed5cd6) |Permission for users to view specific rows or columns in a dataset. |


<span id="942d5402"></span>
# Project permissions

<span id="6cb7c01a"></span>
## Permission overview


|Project permission types |Explanation |
|---|---|
|Create |By default, all users can create projects.<br><br><br>* SaaS environment: Deleting projects is not supported. Please create new projects with caution. System administrators can go to the "System Management" \- "System Settings" page and enable "Only the primary account can create projects" under the project creation settings. In this case, only the primary account can create projects, and sub\-accounts do not have permission to create projects.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f19c7fcca8664ba39158480fabc80782~tplv-goo7wpa0wc-image.image) </span> |
|Search list |Permission to search for the xx project in the project options list in the top navigation bar.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a320b26f788470d9c880ab4cd1ac1ad~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Confidential projects cannot be found by users other than the project administrator.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Projects are sorted by app_id in ascending order. app_id refers to the project ID, which can be obtained by opening any address under the project. As shown in the figure, by opening any link under a project, the URL will display as follows, and the app_id value is 1000326.</div><br><br><br>   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d07ffb79b55e41599080b6260af3f7de~tplv-goo7wpa0wc-image.image" />   </div><br>    |
|No permission |Indicates that there is no permission to view the project. |
|View |Permission to access and enter the project, with the following permissions:<br><br><br>* Can view resources within the project for which they have permission<br><br>* Can create **personal** folders and perform other operations<br><br>* Can create public folders in public folders with **edit permission**<br><br>* **Cannot** create public folders in the **root directory** of public folders<br><br>* Can create folders/datasets in folders with **edit permission**<br><br>* **Cannot** create folders/datasets in the **root directory** of datasets<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Project view permission + edit permission for a public folder = ability to create a new public folder under that public folder</div><br><br><br>* <div data-tips="true" data-tips-type="warning">An error will occur after clicking Confirm to create in the root directory.</div><br> |
|Edit |Includes the above view permissions, and also:<br><br><br>* Can create public folders/datasets in the **root directory**<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Datasets can only be created in folders <strong>with edit permission</strong>.   </div><br>    |
|Global view |Includes the above edit permissions, and also:<br><br><br>* Can view all datasets within the project and **view all data**<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Datasets can only be created in folders <strong>with edit permission</strong>.   </div><br>    |
|Manage |* Can manage permissions for all resources within the project<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The privatized version supports deleting projects in "Management Center" \- "Project Management".   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f19c7fcca8664ba39158480fabc80782~tplv-goo7wpa0wc-image.image" width="566px" />   </div><br>    |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Project type</strong> and <strong>project control level</strong> will have different impacts on project\-related permissions. For details, see <a href="https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#473a0b83">Project information</a>.</div>


<span id="bbb2be4a"></span>
## How to obtain


|Methods for obtaining project permissions |Operation |Operators |Remarks |
|---|---|---|---|
|Project administrator proactively grants permissions |* Project center \- user management \- add user, assign project permissions<br><br>* Project center \- authorize by user, assign project permissions to the target user |Project administrator |\-\- |
|Obtain project permissions by acquiring other resources |Other users grant dataset/visual modeling task/data connection permissions to user A. When user A logs in, they automatically obtain permission to view the project. |Resource administrator |\-\- |
|Obtain permissions by joining a user group |Add the user to the xxx user group, and configure project permissions in user group details \- permission management |User group/project administrator |* If group authorization shielding is enabled, this does not apply. For details, refer to [User-Based Authorization](https://docs.byteplus.com/docs/dataagent/User-Based_Authorization)<br><br>* There will be a delay for both user group authorization and de\-authorization |


<span id="874a55c6"></span>
# Dataset permissions

<span id="1e476cb3"></span>
## Permission overview


|Dataset permission types |Explanation |
|---|---|
|Create |Creating a dataset requires project edit or higher permissions. If a user has edit permissions in a folder, creating a dataset in that folder only requires project view or higher permissions. |
|List display permissions |The left\-side list in the dataset module **displays content**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The display rules for datasets in Project Center \- Project Information will affect this permission. For details, see <a href="https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#c101df17">Dataset display rules</a>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">All datasets (all <strong>datasets</strong> within the project are displayed; clicking on those without permission will prompt a no\-permission message and allow you to apply).</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only datasets you have permission for are displayed.</div><br> |
|View only |* Can view data<br><br>* Can favorite datasets<br><br>* Can view dataset details (data preview, model information)<br><br>* No permissions to download or copy data |
|View |Includes the above view\-only permissions, and also:<br><br><br>* Query datasets on the visual query page<br><br>* Add temporary fields<br><br>* Download datasets<br><br>* Monitor configuration |
|Edit |Includes the above view permissions, and also:<br><br><br>* Can edit basic dataset information<br><br>* Can create usage instructions and set tags<br><br>* Can modify dataset models and perform routine configuration operations<br><br>* Can copy datasets, provided the user also has data connection permissions for the dataset |
|Manage |Includes the above edit permissions, and also:<br><br><br>* Can manage permissions and transfer ownership<br><br>* Can move or delete datasets and perform other operations<br><br>* Can configure row and column permissions |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For view\-only, preview, edit, and management permissions, <strong>project control level</strong> and <strong>row and column permissions</strong> will have different impacts on dataset\-related permissions:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Project control level</strong> will have different impacts on permissions for personal datasets (folders) and public datasets (folders). For details, see <a href="https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions#b0b118d4">Project control levels</a>.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Row and column permissions</strong>: In certain scenarios (as shown below), if row and column permissions are set for a dataset, users may not be able to preview the dataset even if they have dataset permissions.</div>



<span id="bd22a5ca"></span>
## Permission\-related pages


* No dataset permission illustration:

* Dataset details illustration: The user must have at least read\-only permission for the dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/030c93c1d4dd4cc6b7999c926129f31d~tplv-goo7wpa0wc-image.image) </span>

* Dataset editing functionality illustration: The user must have at least editing permission for the dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84cb0159ff3641a486afe7449fdbace0~tplv-goo7wpa0wc-image.image) </span>

* Dataset left\-side list functionality illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75abdeef358f4cf6bbca467a724d2005~tplv-goo7wpa0wc-image.image) </span>

   
   |Operation |Required permission |
   |---|---|
   |Basic information |Dataset management permission |
   |Permission assignment |Dataset management permission |
   |Edit |Dataset edit or management permission |
   |Transfer ownership |Dataset management permission |
   |Move |Dataset management permission |
   |Copy |Dataset edit or management permission + Data connection edit or management permission |
   |Delete |Dataset management permission |
   |Attribution analysis configuration |Dataset edit permission |
   |Data preview configuration |Dataset edit permission |
   |Set tags |Dataset edit or management permission |
   |Switch priority |Dataset edit permission |
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">An error will occur when copying a dataset if there is no data connection permission.</div>



<span id="1058e525"></span>
## How to obtain


|Methods for obtaining dataset permissions |Operation |Eligible users |Remarks |
|---|---|---|---|
|Resource/project administrator grants permission proactively |* Method 1: Use the single resource authorization pop\-up on the right side of the resource list or "Permission assignment" in the resource preview interface to grant permissions to any member, user group, or Feishu group within the project.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32d81964e7d04d1f8eb040f961b4605e~tplv-goo7wpa0wc-image.image) </span><br><br>* Method 2: Project center \- authorize by resource<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d1e5b74eaaa4925aff56814f96635b3~tplv-goo7wpa0wc-image.image) </span><br><br>* Method 3: Project center \- authorize by user<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df03b90419764ac39bde270652ed6f35~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the project administrator can perform this operation.   </div><br>    |* Resource administrator [Methods 1, 2]<br><br>* Project administrator [Methods 1, 2, 3] |\-\- |
|Obtain by joining a user group |Add the user to the xxx user group, then configure the user group's dataset permissions in User Group Management \- User Group Details \- Permission Management \- Dataset.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7ed2b823d064a7e97749ee2b512da84~tplv-goo7wpa0wc-image.image) </span> |User group/project administrator |* User group administrators can only configure datasets **for which they have management permission**<br><br>* If group authorization blocking is enabled, this does not apply. For details, refer to [User-Based Authorization](https://docs.byteplus.com/docs/dataagent/User-Based_Authorization)<br><br>* There will be a delay when granting or revoking user group permissions |


<span id="44c9b764"></span>
# Visual modeling permissions

<span id="55b6b8e7"></span>
## Permission overview


|Permission type |Description |
|---|---|
|Create |At least dataset view permission is required. To add or remove fields, apply filters, and perform other operations, dataset edit permission is required. |
|View |Can view the details page of the visual modeling task, but does not support any operations |
|Edit |In addition to having visual modeling task view permission, can modify the processing flow, run configuration, and perform other operations for the visual modeling task |
|Manage |In addition to having visual modeling task edit permission, can manage permissions, delete, and perform other operations |


<span id="ef5ab1b9"></span>
## Permission\-related pages


* Visual modeling details illustration: The user must have at least viewing permission for visual modeling.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0ea150ac7ae4cc9ae790e6e0c03dc1e~tplv-goo7wpa0wc-image.image) </span>

* Visual modeling editing functionality illustration: The user must have at least editing permission for visual modeling.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb4d991eb3d54840b4d4e0c2addc42d3~tplv-goo7wpa0wc-image.image) </span>

* Visual modeling left\-side list functionality illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/978b142f88474e73ad3657f686b43da4~tplv-goo7wpa0wc-image.image) </span>

   
   |Operation |Required permission |
   |---|---|
   |Rename |Visual modeling edit permission |
   |Move |Visual modeling manage permission |
   |Copy |Visual modeling edit or manage permission |
   |Grant permission |Visual modeling manage permission |
   |Transfer owner |Visual modeling manage permission |
   |Delete |Visual modeling manage permission |
   


<span id="a27de457"></span>
## How to obtain


|Methods for obtaining visual modeling task permissions |Operation |Eligible personnel |
|---|---|---|
|Resource or project administrator actively grants permission |* Method 1: Use the single resource permission dialog on the right side of the resource list or "Permission assignment" in the resource preview interface to grant permissions to any member, user group, or Feishu group within the project.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f79f7cabc8094ee38e165602970396d4~tplv-goo7wpa0wc-image.image) </span><br><br>* Method 2: Project Center – Grant by resource<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6829ec0317904ff5894f38a81e78571d~tplv-goo7wpa0wc-image.image) </span><br><br>* Method 3: Project Center – Grant by user<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ede599a8239473f855a62cc29750bc1~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the project administrator can perform this operation.   </div><br>    |* Resource administrator [Methods 1, 2]<br><br>* Project administrator [Methods 1, 2, 3] |


<span id="7ec0110a"></span>
# Data connection permissions

<span id="24938b1b"></span>
## Permission overview


|Permission type |Description |
|---|---|
|Create |Except for regular users and users whose project permission is view only, all other users can create data connections |
|View |* Can view the data connection<br><br>* When creating a dataset, you can select this data connection |
|Edit |In addition to the above view permission, can edit the information of the data connection |
|Manage |In addition to the above edit permission, can modify the permissions of the data connection and perform other operations |


<span id="ef6a5e11"></span>
## Permission\-related pages


* Data connection details illustration: The user must have at least viewing permission for the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9526bbda4194df59a0e01c1bfda3189~tplv-goo7wpa0wc-image.image) </span>

* Data connection editing functionality illustration: The user must have at least editing permission for the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce39aa39051c4b59b6e146613cc165e9~tplv-goo7wpa0wc-image.image) </span>

* Data connection left\-side list functionality illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b7ad5aa8d2f45c3b37a4989b9a1be75~tplv-goo7wpa0wc-image.image) </span>

   
   |Operation |Required permission |
   |---|---|
   |Permission assignment |Data connection manage permission |
   |Create dataset |Creating a new dataset requires project edit permission or higher. If a user has edit permission for a specific folder, then creating a new dataset in that folder only requires project view permission or higher. |
   |Create a visual model |To create a new visual model, at least dataset view permission is required. To add or remove fields, filter data, or perform other operations, dataset edit permission is needed. |
   |Transfer ownership |Data connection management permission |
   |Delete |Data connection management permission |
   


<span id="df8d96c4"></span>
## How to obtain


|How to obtain data connection permission |Operation |Authorized personnel |
|---|---|---|
|Resource/project administrator grants permission proactively |* Method 1: Use the single resource authorization pop\-up on the right side of the resource list or the "Permission allocation" option in the resource preview interface to grant permission to any member, user group, or Lark Group within the project.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b72702b367f4c21899f0d01ff227f2d~tplv-goo7wpa0wc-image.image) </span><br><br>* Method 2: Project center \- authorize by resource<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/388f29f7939a45d0acedd14bc5a670bd~tplv-goo7wpa0wc-image.image) </span><br><br>* Method 3: Project center \- authorize by user<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09781b4ea1524aed8d7d902273041db5~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the project administrator can perform this operation.   </div><br>    |* Resource administrator [Methods 1, 2]<br><br>* Project administrator [Methods 1, 2, 3] |


<span id="4efb3f5c"></span>
# Agent permissions

<span id="06ebba27"></span>
## Permission overview


|Agent permission types |Explanation |
|---|---|
|Use |* Can view the agent list<br><br>* Can use the agent<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To use an agent for Q&A, the user must also have at least view permission for the dataset configured for the agent.   </div><br>    |
|Manage |In addition to the above usage permissions, agent creation, configuration, publishing, deactivation, deletion, and member addition can also be performed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To configure a dataset for an agent, the user must also have at least view permission for that dataset.</div><br> |


<span id="e5175e07"></span>
## Permission\-related pages


* Agent usage illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/931d7744a8d344618150d43166fe8a74~tplv-goo7wpa0wc-image.image) </span>

* Agent list illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1644884ef0a447c8bc2c74f5f3441aae~tplv-goo7wpa0wc-image.image) </span>

* Agent configuration illustration: With agent management permission, the user can access the agent configuration page to perform related configuration operations. However, to add a dataset to the agent, the user must also have at least viewing permission for the relevant dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6852dc536a274a3e980320953b71a576~tplv-goo7wpa0wc-image.image) </span>


<span id="7ae84c01"></span>
## How to obtain


|How to obtain agent permission |Operation |Authorized personnel |
|---|---|---|
|Agent administrator grants permission proactively |* Agent configuration \- Basic information \- Add member: The agent administrator adds regular agent members.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3737ed4a2b5b4f4db9b67a9f53d82bb8~tplv-goo7wpa0wc-image.image) </span> |Agent administrator |


<span id="f3ed5cd6"></span>
# Row and column permissions

<span id="2de9db60"></span>
## Permission overview


|Row and column permission types |Explanation |
|---|---|
|Row permission |Control whether xxx user can or cannot view certain rows of a field. For details, see [Data Row and Column Permissions](https://docs.byteplus.com/docs/dataagent/Data_Row_and_Column_Permissions) |
|Column permission |Restrict visibility of a specific column in the dataset to only xxx user. For details, see [Data Row and Column Permissions](https://docs.byteplus.com/docs/dataagent/Data_Row_and_Column_Permissions) |


<span id="801946c2"></span>
## Permission\-related pages


* Row and column permission configuration entry illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97a7be923ce34d4bb3a20411b5a033bb~tplv-goo7wpa0wc-image.image) </span>

* Row and column permission illustration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57a1af3b398749e18e819bf6bd022869~tplv-goo7wpa0wc-image.image) </span>

* How to determine whether row and column permissions are restricted

   * No row permission illustration

   * No column permission or only partial row permission


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Dataset permission vs row and column permission</div>


   * <div data-tips="true" data-tips-type="warning">Q: Does having dataset permission mean having row and column permission? A: No. When row and column permission restrictions are enabled for a dataset, having dataset permission does not mean data can be viewed. Row and column permission must also be applied for.</div>


   * <div data-tips="true" data-tips-type="warning">Q: Does having row and column permission mean having dataset permission? A: No. Even with row and column permissions, to access the visual modeling page for ad hoc analysis, dataset permissions must also be requested.</div>


* <div data-tips="true" data-tips-type="warning">When configuring row and column permissions, the <strong>simulation verification feature</strong> can be used to quickly verify whether user permissions are configured correctly.</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03a7009a4c014b4e9a51843d7eb65c4a~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   


<span id="aee79c0a"></span>
## How to obtain

Data row and column permissions must be set at the dataset level; therefore, the following instructions are all operations performed at the dataset level:


* Data row and column permissions are proactively granted by the project administrator or resource administrator.

* How to configure: On the row and column permission rule configuration page, authorize any member or user group within the project. For details, refer to [Data Row and Column Permissions](https://docs.byteplus.com/docs/dataagent/Data_Row_and_Column_Permissions).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cb8f2813fcf49f682805007992202fd~tplv-goo7wpa0wc-image.image) </span>


<span id="02c69336"></span>
# Other features

<span id="58957799"></span>
## Bulk authorization


* "A resource" (using dataset as an example) \- "More" \- "Permission allocation": You can first write the usernames elsewhere (such as in a text file), separating usernames with commas, then add users in bulk. You can also choose to authorize user groups.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d58130b510cc4c10bc80afeb434c1079~tplv-goo7wpa0wc-image.image) </span>

* "Project center" \- "User group management": First create and associate a user group, then authorize all users within the user group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/316629b3f626412b9d12644ce8bd0a50~tplv-goo7wpa0wc-image.image) </span>

* "Project center" \- "Authorize by resource": First filter the resources to be authorized, then click "Bulk authorization" to authorize users or user groups.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e64bf53847544c69b060c04b3831a78d~tplv-goo7wpa0wc-image.image) </span>


<span id="c4c82c2d"></span>
## Reference permissions

This is equivalent to copying the user list and corresponding permission settings. For example, if users A and B both have edit permissions for a dataset, when referencing this dataset's permissions in the project, you can set users A and B to have edit permissions for the project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ea76542faa14c66891ef45f8b066506~tplv-goo7wpa0wc-image.image) </span>

<span id="fada04ef"></span>
# Related references

<span id="473a0b83"></span>
## Project information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f23ffb336b0b422db50301e8296b0ca0~tplv-goo7wpa0wc-image.image) </span>

All instructions can be found at [Project Information](https://docs.byteplus.com/docs/dataagent/Project_Information). The following provides a detailed explanation of project types, project control levels, and dataset display rules.

<span id="43329b98"></span>
### Project types


| |Usage scenarios |Impact on permissions |
|---|---|---|
|Confidential projects |For projects with high permission requirements, users from other departments are not allowed to view the project space. |* Members can only be added by the project administrator.<br><br>* The project cannot be found in the project search box except for the project administrator. |
|Non\-confidential projects |The project can be made public within the organization. |Users can search for the project and proactively find the project administrator to apply to join the project. |


<span id="b0b118d4"></span>
### Project control levels


|Control modes |Personal resources (personal datasets) ||||Public resources (public datasets and others) |||
|---|---|---|---|---|---|---|---|
||Create |Request |Manage permissions |Grant permissions to others |Create/request |Manage permissions (approver) |Grant permissions to others |
|Standard |✅ |✅ |Creator |✅ |✅ |Creator |✅ |
|Moderate |✅ |❌ |Creator |❌ |✅ |Default configuration<br><br>Project administrator + administrator of the folder containing the resource<br><br>(Creator has edit permissions) |✅ |
|Strict |❌ |❌ |\-\- |❌ |✅ |Default configuration<br><br>Project administrator + administrator of the folder containing the resource<br><br>(Creator has edit permissions) |✅ |



* After switching the project control level, the management permission ownership of newly created resources will be handled according to the new mode. The management permission ownership of historical resources created before the switch will remain unchanged and will not be updated retroactively.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended not to frequently switch the project control status.   </div>
   

<span id="c101df17"></span>
### Dataset display rules


| |Usage scenarios |Impact on permissions |
|---|---|---|
|All datasets |* Need to be aware of all datasets within the project (including those without permissions)<br><br>* Facilitates users in requesting permissions for datasets they do not have access to |All datasets within the project are displayed; clicking on a dataset without permission will prompt that permission is lacking, and permission requests are supported. |
|Only datasets with permissions |* Only need to view datasets for which the user has permissions<br><br>* Datasets without permissions have high permission requirements and are not suitable for display to users without permissions in the list<br><br>* Prefer to simplify the list and avoid interference from datasets without permissions |Affects the content displayed in the left\-side list of the dataset module; the list only shows datasets for which the user has permissions. |
