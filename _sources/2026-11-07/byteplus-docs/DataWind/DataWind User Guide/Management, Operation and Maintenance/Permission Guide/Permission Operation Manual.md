---
title: "Permission Operation Manual"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Permission_Operation_Manual"
---

<span id="_1-可视化查询模块"></span>
# 1. Visualization query module

<span id="_1-1-功能清单"></span>
## 1.1 Feature list


|**Function** |**Function overview and usage** |**Required permissions** |
|---|---|---|
|Add personal expression |[Add or Modify Fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields) |Dataset view or higher permission required |
|Create group |[Configure Field Grouping](https://docs.byteplus.com/docs/DataWind/Configure_Field_Grouping) |Dataset view or higher permission required |
|Attribution analysis |[Intelligent Attribution](https://docs.byteplus.com/docs/DataWind/Intelligent_Attribution) |Dataset view or higher permission required |
|Create monitoring<br><br><br>> * Who can view the monitoring? Chart creator, monitoring configurator, monitoring recipient, project administrator<br><br>> * Who can modify the monitoring? Chart creator, monitoring configurator, monitoring recipient<br><br>> * Who receives the test message? Monitoring recipient |[（暂不发布）Monitoring and Alerting](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62874) |Dataset view or higher permission required |
|Download chart |[Data Download](https://docs.byteplus.com/docs/DataWind/Data_Download), download pivot table |Dataset view or higher permission required |
|Copy value or header | |Dataset view or higher permission required |
|Field value alias |[Set Field Value Aliases](https://docs.byteplus.com/docs/DataWind/Set_Field_Value_Aliases) |Dataset edit or higher permission required |
|Add dataset field |[Add or Modify Fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields) |Dataset edit or higher permission required |
|Create hierarchy |[Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down) |Dataset edit or higher permission required |
|Attribution analysis configuration |[Intelligent Attribution](https://docs.byteplus.com/docs/DataWind/Intelligent_Attribution) |Dataset edit or higher permission required |
|Batch modify fields |[Add or Modify Fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields) |Dataset edit or higher permission required |
|Geographical role |[Map](https://docs.byteplus.com/docs/DataWind/Map)Supported types: filled map, marker map |Dataset edit or higher permission required |


<span id="_1-2-授权操作方法"></span>
## 1.2 Authorization operation method

(1) On the dataset page, select the corresponding dataset details page.

(2) Click Permission assignment.

(3) Select the name of the authorizer.

(4) Grant permissions according to the required authorization requirements.

> **Permission scope: View only < View < Edit < Manage**

> If the minimum required permission is View only, you can select View only, View, Edit, or Manage; if the minimum required permission is View, you can select View, Edit, or Manage.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5da9a4960d7246fb882b25f9eda5edb2~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-仪表盘模块"></span>
# 2. Dashboard module

<span id="_2-1-功能清单"></span>
## 2.1 Feature list


|**Function** |**Function overview and usage** |**Required permissions** |
|---|---|---|
|Add to favorites |[2.2 Add a dashboard to favorites](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations#_2-2-%E6%94%B6%E8%97%8F%E4%BB%AA%E8%A1%A8%E7%9B%98) |Dashboard view or higher permission required |
|Standard subscription (sent to self only) |[(暂不发布)Data Subscription](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628c5)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bebb1cb53084509a9843d8618d38a67~tplv-goo7wpa0wc-image.image) </span> |Dashboard view or higher permission required |
|Share dashboard |[Share](https://docs.byteplus.com/docs/DataWind/Dashboard_Viewing_Operations#_2-1-4-%E5%88%86%E4%BA%AB) |Dashboard view or higher permission required |
|Download chart/data from dashboard |[Download/copy data](https://docs.byteplus.com/docs/DataWind/Dashboard_Viewing_Operations#_3-3-2-%E4%B8%8B%E8%BD%BD-%E5%A4%8D%E5%88%B6%E6%95%B0%E6%8D%AE)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2be1afed42f48928e6cb94935c751df~tplv-goo7wpa0wc-image.image) </span> |Dashboard view or higher permission required |
|Copy value or value and header from dashboard chart | |Dashboard view or higher permission required |
|Edit dashboard |[Dashboard Editing Overview](https://docs.byteplus.com/docs/DataWind/Dashboard_Editing_Overview) |Dashboard edit or higher permission required |
|Edit basic information of the dashboard |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/762ad712838c4769b6a01de4d2a0363e~tplv-goo7wpa0wc-image.image) </span> |Edit or higher permissions for the dashboard |
|View dashboard access statistics |[Access Statistics](https://docs.byteplus.com/docs/DataWind/Access_Statistics) |Edit or higher permissions for the dashboard |
|Advanced subscription (can subscribe for oneself, others, or groups)<br><br><br>> * Who can view the subscription? Dashboard administrators, subscription managers, project administrators, subscription recipients<br><br>> * Who can modify the subscription? Dashboard administrators, subscription creators, project administrators<br><br>> * Who receives the test message? Current editor |[(暂不发布)Data Subscription](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628c5)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bebb1cb53084509a9843d8618d38a67~tplv-goo7wpa0wc-image.image) </span> |Dashboard management permissions |
|Grant permissions to others |[Authorization and Sharing](https://docs.byteplus.com/docs/DataWind/Authorization_and_Sharing) |Dashboard management permissions<br><br>(Special case: Has management permissions but cannot grant❓)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1639cfd9daba419b87d54f00dbd8f226~tplv-goo7wpa0wc-image.image) </span> |
|Copy dashboard |[2.7 Copy dashboards](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations#_2-5-%E5%A4%8D%E5%88%B6%E4%BB%AA%E8%A1%A8%E7%9B%98) |Dashboard management permissions |
|Move dashboard |[2.6 Move dashboards](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations#_2-4-%E7%A7%BB%E5%8A%A8%E4%BB%AA%E8%A1%A8%E7%9B%98)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5a1dd70ad42458385d45ed1fa3ac98d~tplv-goo7wpa0wc-image.image) </span> |Dashboard management permissions |
|Delete dashboard<br><br>(Creator but cannot find the delete button❓👇)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1639cfd9daba419b87d54f00dbd8f226~tplv-goo7wpa0wc-image.image) </span> |[2.12 Delete dashboard](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations#_2-9-%E5%88%A0%E9%99%A4%E4%BB%AA%E8%A1%A8%E7%9B%98)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8340e8809ab4cf5a7971c23330d6276~tplv-goo7wpa0wc-image.image) </span> |Dashboard management permissions |
|Transfer dashboard ownership |[Resource Authorization](https://docs.byteplus.com/docs/DataWind/Resource_Authorization) |Dashboard management permissions or project administrators |
|Create a personal folder<br><br>(Cannot create a personal folder❓👇<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1639cfd9daba419b87d54f00dbd8f226~tplv-goo7wpa0wc-image.image) </span> |[Dashboard List Operations](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations) |Project view permissions or higher |
|Create a personal dashboard<br><br>(Cannot create a personal dashboard❓👇<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1639cfd9daba419b87d54f00dbd8f226~tplv-goo7wpa0wc-image.image) </span> |[3.1 Personal dashboards](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations#_3-1-%E4%B8%AA%E4%BA%BA%E4%BB%AA%E8%A1%A8%E7%9B%98) |Project view permissions or higher |
|Create a public dashboard |[3.2 Shared with me (shared dashboards)](https://docs.byteplus.com/docs/DataWind/Dashboard_List_Operations#_3-2-%E4%B8%8E%E6%88%91%E5%85%B1%E4%BA%AB%EF%BC%88%E5%85%B1%E4%BA%AB%E4%BB%AA%E8%A1%A8%E7%9B%98%EF%BC%89) |Project edit permissions or higher |


<span id="_2-2-授权操作方法"></span>
## 2.2 Authorization operation method

(1) Option 1: Click to enter the dashboard view page, and then click the Authorize button in the upper right corner; Option 2: Click the three dots on the right side of the dashboard to open the operation list, then click the Authorize button.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08788da38ff247d384dcc18a2bba1d1d~tplv-goo7wpa0wc-image.image) </span>

(2) Click Authorize.

(3) Select the name of the authorizer.

(4) Grant permissions according to the required authorization requirements.

> **Permission scope: View only < View < Edit < Manage**

> If the minimum required permission is View only, you can select View only, View, Edit, or Manage; if the minimum required permission is View, you can select View, Edit, or Manage.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5da9a4960d7246fb882b25f9eda5edb2~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-数据集模块"></span>
# 3. Dataset module

<span id="_3-1-功能清单"></span>
## 3.1 Feature list


|**Functionality** |**Overview and usage instructions** |**Required permissions** |
|---|---|---|
|Create a dataset |[2.1 Create a new dataset](https://docs.byteplus.com/docs/DataWind/109998#_2-1-%E6%96%B0%E5%BB%BA%E6%95%B0%E6%8D%AE%E9%9B%86) |Project edit permissions or higher<br><br>(If the user has edit permissions for a folder, only project view permissions or higher are required to create a dataset in that folder) |
|Folder for the new dataset |[2.3 Create a folder](https://docs.byteplus.com/docs/DataWind/109998#_2-3-%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9) |Project edit permissions or higher |
|Edit lifecycle |Retention period for synchronized data in the dataset. If the lifecycle is 3 days, partition data generated on January 25 will be deleted on January 28. If the data is synchronized daily, only data synchronized within the last 3 days can be queried. |Dataset edit permissions or higher |
|Edit runtime parameters |Set dataset synchronization runtime parameters as needed to ensure successful synchronization, optimize synchronization performance, and so on |Dataset edit permissions or higher |
|Edit dataset model configuration |Replace base table |Dataset edit permissions or higher |
|Copy |[Dataset List Management](https://docs.byteplus.com/docs/DataWind/110015) |Dataset edit or higher permissions |
|Create usage instructions | |Dataset edit or higher permissions |
|Set tags |[Tag Management](https://docs.byteplus.com/docs/DataWind/110017) |Dataset edit or higher permissions |
|Move |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5a1dd70ad42458385d45ed1fa3ac98d~tplv-goo7wpa0wc-image.image) </span> |Dataset management permissions |
|Cross\-project configuration (mirrored dataset) |[Mirror Dataset](https://docs.byteplus.com/docs/DataWind/110002) |Dataset management permissions |
|Grant permissions to others |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff40e590d11c47338f9e90ba06849e63~tplv-goo7wpa0wc-image.image) </span> |Dataset management permissions |
|Tag management |[Tag Management](https://docs.byteplus.com/docs/DataWind/110017) |Project management permissions |
|Transfer dataset ownership |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9befcc1147c341bf9123ae5e4c1ff88a~tplv-goo7wpa0wc-image.image) </span> |Dataset management permissions/Project administrator |


<span id="_3-2-授权操作方法"></span>
## 3.2 Authorization operation method

<span id="_3-2-1-单数据集权限授权操作方法"></span>
### 3.2.1 Single dataset permission authorization method

(1) On the dataset page, select the corresponding dataset details page.

(2) Click Permission assignment.

(3) Select the name of the authorizer.

(4) Grant permissions according to the required authorization requirements.

> **Permission scope: View only < View < Edit < Manage**

> If the minimum required permission is View only, you can select View only, View, Edit, or Manage; if the minimum required permission is View, you can select View, Edit, or Manage.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5da9a4960d7246fb882b25f9eda5edb2~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-项目权限授权操作方法"></span>
### 3.2.2 Project permission authorization method

 **(1) Applicant:**  Click Project Center, find the project information, and contact the project administrator for the next step.

 **(2) Project administrator**: Click Project Center \-\-\> select Permission management \-\-\> enter username and so on \-\-\> click Project \-\-\> select permission scope.

> **Permission scope: View < Edit < Global view < Manage**

> If the minimum required permission is Edit, you can select Edit, Global view, or Manage.

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd31eee7b474b8a886310131fc9267f~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-项目中心模块"></span>
# 4. Project center module

<span id="_4-1-功能清单"></span>
## 4.1 Feature list


|**Function** |**Function overview and usage** |**Required permissions** |
|---|---|---|
|Add or batch update user/user group attributes |[User Properties](https://docs.byteplus.com/docs/DataWind/User_Properties) |Project edit permissions |
|Third\-party integration |[Overview of Embedded Analytics](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f6288b) |Project management permissions |
|User management |[User Management](https://docs.byteplus.com/docs/DataWind/User_Management) |Project management permissions |
|Delete user/user group attributes configured by others |[User Properties](https://docs.byteplus.com/docs/DataWind/User_Properties) |Project management permissions |
|Permission management |[Permission Management](https://docs.byteplus.com/docs/DataWind/Permission_Management) |Project management permissions |
|Modify project settings |[Project Information](https://docs.byteplus.com/docs/DataWind/Project_Information) |Project management permissions |


<span id="_4-2-授权操作方法"></span>
## 4.2 Authorization operation method

 **(1) Applicant:**  Click Project Center, locate the project information, and contact the project administrator for the next steps

 **(2) Project administrator**: Click Project Center \-\-\> select Permission Management \-\-\> enter the username and other details \-\-\> click Project \-\-\> select the authorization scope

> **Permission scope: View < Edit < Global view < Manage**

> For example, if editing or higher is required, you can select Edit, Global view, or Manage

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd31eee7b474b8a886310131fc9267f~tplv-goo7wpa0wc-image.image) </span>
