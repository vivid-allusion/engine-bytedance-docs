---
title: "Resource Migration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Resource_Migration"
---

<span id="7b193ec4"></span>
# 1. Overview

This document describes the resource migration feature of visual modeling, which includes resource export and resource import. This feature supports flexible migration of resources such as visual modeling tasks and datasets. For example, visual modeling tasks and their associated datasets from Project A can be exported and then imported into Project B, facilitating resource sharing and collaboration between projects.

<span id="24c75767"></span>
# 2. Quick start

**Notes:** 

Users with the "Visual Modeling Task Module Edit Permission" or "Project Edit" permission can access this page, including system administrators, group administrators, project administrators, and users with module\-specific permissions.

**Steps:** 

Data preparation \- Visual modeling \- Resource migration

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d36165b86b24cf283e45beb0481e7e0~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="c154f7ad"></span>
# 3. Feature description

<span id="498e0deb"></span>
## 3.1 Resource export

<span id="7091f2e2"></span>
### 3.1.1 Select resources to export

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/710d129f10b4402897a59ba82e8e5973~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


First, you can view all exportable visual modeling tasks in the resource list, including detailed information such as task name, task owner, save path, and creation time. The creation time field supports sorting. By default, the system sorts tasks in descending order of creation time, allowing you to quickly find the most recent tasks.

Second, you can filter the resources to export in multiple ways:


* **Task name**: Supports fuzzy search for quickly locating specific tasks.

* **Save path:**  Provides a drop\-down menu with multi\-selection and fuzzy search support to help users quickly find tasks.

* **Task owner**: Also supports multi\-selection and fuzzy search in the drop\-down menu.


**Note:**  Only offline tasks that you have management permissions for and created manually are displayed here. System\-created tasks, real\-time tasks, and tasks containing output label operators are not included.

<span id="a3f8993e"></span>
### 3.1.2 View associated datasets

After selecting one or more visual modeling tasks at the top, scroll down the page to view the datasets associated with these tasks in real time below.

Related datasets are displayed in two categories: **input node datasets** and **output node datasets**. At the same time, the system will display the visual modeling tasks that reference these datasets. Output datasets will clearly indicate whether you have export permissions: if you currently do not have export permissions, the system will restrict export operations; if your permissions change, you can click the “**Refresh permission status**” button to update and view your latest permissions for the dataset in real time.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21813bf99a264e478ad28bfc103febb0~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


**Caution:** 


* If multiple tasks are associated with the same dataset, the system will automatically remove duplicates, and the list will display it only once.

* For datasets that are both the output of Task A and the input of Task B, they will be displayed in both the input and output node datasets.


<span id="c982c6e6"></span>
### 3.1.3 View related data connections

This page displays all data connections associated with the selected task, including the connection names and the tasks that reference these connections.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b729ea3a010543249c28b7befb588eca~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="9f01ea5d"></span>
### 3.1.4 Export permission information settings

When you select “Synchronize export permission information”, the system will export the following permission\-related information:


* **Creators of tasks and datasets**. If the creator is the resource Owner, the system will look for this user in the target project; if the user does not exist, the permission will be assigned to the importer.

* **Authorization information, including users with management, edit, and view permissions**. If the target user exists, the corresponding permissions will be assigned; if not, permissions will not be assigned.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e2ea29b4b6f4ad3a57053eef3ae2479~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


**Caution:**  Exported permissions do not include information related to user groups, roles, departments, or row and column permissions. You need to re\-authorize these in the new project.

<span id="c35c305e"></span>
### 3.1.5 Perform export operations

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d515f369d46244419fc63527289f632e~tplv-goo7wpa0wc-image.image" width="2822px" /></div>


After completing the above steps, you can click the “Export” button. The system will generate the corresponding export file based on the resources you selected for export.

**Export restrictions**: The system limits each export to a maximum of 100 tasks.

**Export file naming**: The default naming rule for exported files is: "可视化建模_${export time}_随机字符串", for example: "可视化建模_2023\-12\-08 12:00:09_随机字符串".

<span id="19e1776b"></span>
## 3.2 Resource import

<span id="c951ec8b"></span>
### 3.2.1 Upload the file to be imported

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b975618e4f6a4b48aa2cf686adba0b12~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


Click the New button to upload the file to be imported. Caution: Only .prep files are supported.

<span id="9b0f5d10"></span>
### 3.2.2 Select the import method

Please select the import method:


* **New**: Create a brand new visual modeling task in the target project.

* **Overwrite**: Replace the existing task in the current project with the task content from the imported package.


<span id="72c77033"></span>
### 3.2.3 New method

 **(1) Select the resource to import**

When you select the import method as New, you can view and select the task to be imported from the resource list. Based on the task you select, the system will display the corresponding dataset list, data connection list, and cluster queue list.

 **(2) Import datasets**

For datasets associated with the visual modeling task, they will be newly created or associated with existing datasets according to your selection.

**Input node datasets** are not imported and can only be associated with existing datasets. This is a mapping relationship. After import, the input node datasets of the task will be replaced with the associated datasets, and the metadata of the associated datasets will not be overwritten.

**Output node datasets** will be imported, with two import modes:


* New: Create the dataset in the current project. If a dataset with the same name exists, the import will fail.

* Associate with existing dataset: During import, the dataset will be replaced with the associated dataset. The system will compare the metadata differences between the original dataset and the associated dataset, and the user can choose whether to overwrite.


 **(3) Configure data connections**

In the **Data Connections** list, the data connections referenced by the currently selected visual modeling task are displayed, and data connections available for association in this project are provided for the user to select. When importing a visual modeling task, the system will automatically replace the data connection in the task with the data connection you select.

 **(4) Configure cluster queue**

In the **resource queue** list, the resource queues used by the selected visual modeling tasks are displayed. Please select a resource queue suitable for "scheduled tasks" from the drop\-down list. When importing a visual modeling task, the system will automatically replace the resource queue in the task with the queue you select.

 **(5) Import permission information**

In the target project, the system will search for the creator of the original resource and the task Owner. If found, the permissions will be associated with the corresponding user; if not found, the permissions will be associated with the importer.

<span id="1c9e4b89"></span>
### 3.2.4 Overwrite method

 **(1) Select resources to import**

When you select the overwrite import method, you can view the task names of the resources to be imported in the resource list and select which resource in this project to overwrite. At the same time, you can also choose whether to overwrite the task name, description, and storage directory.

**Overwrite logic**: The datasets, data connections, and queues in the visual modeling task will be processed according to the configured mapping relationships, and the remaining content will be overwritten.

 **(2) Import datasets**

For datasets associated with the visual modeling task, you can choose to create new datasets or associate them with existing datasets based on your actual selection.

 **(3) Configure data connections**

In the **data connection** list, the data connections referenced by the currently selected visual modeling tasks are displayed, and the available data connections in this project are provided for you to select. When importing a visual modeling task, the system will automatically replace the data connection in the task with the data connection you select.

 **(4) Configure cluster queue**

In the **resource queue** list, the resource queues used by the selected visual modeling tasks are displayed. Please select a resource queue suitable for "scheduled tasks" from the drop\-down list. When importing a visual modeling task, the system will automatically replace the resource queue in the task with the queue you selected.

 **(5) Import permission information**

After importing permissions, the resource owner will be consistent with the source resource, and the resource permissions will be added on top of the existing ones. If not imported, the Owner and permission information of the current resource in this project will remain unchanged.

<span id="5690398b"></span>
### 3.2.5 Perform the import operation

After completing the above operations, you can click the "Import" button. The system will import resources according to your selection.

During the import process, the import progress will be displayed, as shown below:

After the import is complete, an overview of the successful and failed cases will be displayed, and you can also download the detailed import data.

<span id="8ab40bef"></span>
# 4. Permission description

<span id="e093f41e"></span>
## 4.1 Resource export

(1) Users with the "**visual modeling task module edit permission**" or "**project edit**" permission can access this page, including system administrators, group administrators, project administrators, and users with module permission points.

(2) Users who access this page can export tasks and output datasets for which they have **management permission**. Data connections and input datasets are not subject to permission checks.

<span id="736de713"></span>
## 4.2 Resource import

(1) Users with the "**visual modeling task module edit permission**" or "**project edit**" permission can access this page.

(2) Method for creating a new task:


* Task resource permission: No permission check; any importer can create a new one.

* Input dataset permission: To associate with an existing dataset, **management permission** for that dataset is required.

* Output dataset permission: No check for new datasets; to associate with an existing dataset, **management permission** for that dataset is required.

* Data connection: To associate with an existing data connection, **management permission** for the data connection is required;

* Permission information:

   * If permission information is imported: The task Owner is user A from the source project. A must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.

   * If permission information is not imported: The task Owner is the importer B. B must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.


(3) Task overwrite method:


* Task resource permissions: **management permission** is required;

* Input dataset permissions: When associating with an existing dataset, **management permission** for that dataset is required;

* Output dataset permissions: No check is performed for newly created datasets. When associating with an existing dataset, **management permission** for that dataset is required;

* Data connection: When associating with an existing data connection, **management permission** for the data connection is required.

* Permission information

   * Importing permission information: The task Owner will be replaced. The task Owner is A from the source project. A must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.

   * Not importing permission information: The task Owner is C from the current project. C must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.
