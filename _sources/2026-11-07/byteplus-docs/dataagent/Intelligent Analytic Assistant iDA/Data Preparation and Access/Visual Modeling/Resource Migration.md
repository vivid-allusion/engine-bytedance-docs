---
title: "Resource Migration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Resource_Migration_"
---

<span id="7b193ec4"></span>
# 1. Overview

This document describes the resource migration functionality for visual modeling, including both resource export and resource import. This feature enables flexible migration of resources such as visual modeling tasks and datasets. For example, visual modeling tasks and their associated datasets from Project A can be exported and imported into Project B, facilitating resource sharing and collaboration across projects.

<span id="24c75767"></span>
# 2. Quick start

**Note:** 

Users with "Visual Modeling Task Module Edit Permission" or "Project Edit" permission can access this page, including system administrators, group administrators, project administrators, and users with module\-level permissions.

**Steps:** 

Data preparation \- Visual modeling \- Resource migration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7881e8de5eb43d58e7a375f83bfc394~tplv-goo7wpa0wc-image.image) </span>

<span id="c154f7ad"></span>
# 3. Feature introduction

<span id="498e0deb"></span>
## 3.1 Resource export

<span id="7091f2e2"></span>
### 3.1.1 Select resources to export

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f00279212ab46369110fc5846b0c446~tplv-goo7wpa0wc-image.image) </span>

First, you can view all exportable visual modeling tasks in the resource list, including detailed information such as task name, task owner, save path, and creation time. The creation time field supports sorting. By default, the system sorts tasks in reverse chronological order, allowing you to quickly locate the most recent tasks.

Second, you can filter the resources to export in multiple ways:


* **Task name**: Supports fuzzy search for quickly locating specific tasks.

* **Save path:**  Provides a dropdown menu with multi\-select and fuzzy search, helping users quickly find tasks.

* **Task owner**: Also supports multi\-select and fuzzy search in the dropdown menu.


**Note:**  Only offline tasks that you have management permissions for and have created manually are displayed here. System\-created tasks, real\-time tasks, and tasks containing output label operators are not included.

<span id="a3f8993e"></span>
### 3.1.2 View associated datasets

After selecting one or more visual modeling tasks at the top, scroll down the page to view the datasets associated with these tasks in real time below.

Associated datasets are displayed in two categories: **input node datasets** and **output node datasets**. At the same time, the system will display the visual modeling tasks that reference these datasets. Output datasets will clearly indicate whether you have export permissions: If you currently lack export permissions, the system will restrict export operations. If permissions change, you can click the “**Refresh permission status**” button to update and view your latest permission settings for the dataset in real time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc41b378039242299e9f6e0cfa03d063~tplv-goo7wpa0wc-image.image) </span>

**Caution:** 


* If multiple tasks are associated with the same dataset, the system will automatically remove duplicates, and the list will display it only once.

* For datasets that are both outputs of Task A and inputs of Task B, they will be displayed in both input and output node datasets.


<span id="c982c6e6"></span>
### 3.1.3 View associated data connections

This page displays all data connections associated with the selected task, including the connection name and the tasks that reference the connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65174c499dfb43fd8344d7c5800a7c89~tplv-goo7wpa0wc-image.image) </span>

<span id="9f01ea5d"></span>
### 3.1.4 Export permission information settings

When you select “Synchronize export permission information,” the system will export the following permission\-related information:


* **Creators of tasks and datasets**. If the creator is the resource Owner, the system will search for the user in the target project. If the user does not exist, permissions will be associated with the importer.

* **Authorization information, including users with management, edit, and view permissions**. If the target user already exists, the corresponding permissions will be assigned. If not, permissions will not be assigned.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/476a3d7094ab4805afb9528468377aea~tplv-goo7wpa0wc-image.image) </span>

**Caution:**  Exported permissions do not include information related to user groups, roles, departments, or row and column permissions. You need to re\-authorize these in the new project.

<span id="c35c305e"></span>
### 3.1.5 Perform export operations

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9545839fb812499693bd2567f01ccea2~tplv-goo7wpa0wc-image.image) </span>

After completing the above operations, you can click the “Export” button. The system will generate the corresponding export file based on the resources you selected for export.

**Export restrictions**: The system limits each export to a maximum of 100 tasks.

**Export file naming**: The default naming rule for exported files is: "Visual Modeling_${export time}_random string", for example: "Visual Modeling_2023\-12\-08 12:00:09_random string".

<span id="19e1776b"></span>
## 3.2 Resource import

<span id="c951ec8b"></span>
### 3.2.1 Upload the file to be imported

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c398287d129443a95d07366b9dfceeb~tplv-goo7wpa0wc-image.image) </span>

Click the New button to upload the file to be imported. (Caution: Only .prep files are supported)

<span id="9b0f5d10"></span>
### 3.2.2 Select the import method

Please select the import method:


* **New**: Create a brand\-new visual modeling task in the target project.

* **Overwrite**: Replace the existing task in the current project with the task content from the imported package.


<span id="72c77033"></span>
### 3.2.3 New method

 **(1) Select the resource to import**

When you select the import method as New, you can view and select the task to be imported from the resource list. Based on the task you select, the system will display the corresponding dataset list, data connection list, and cluster queue list.

 **(2) Import datasets**

For datasets associated with the visual modeling task, you can choose to create new datasets or associate them with existing datasets based on your actual selection.

**Input node datasets** are not imported and can only be associated with existing datasets. This is a mapping relationship. After import, the input node datasets of the task will be replaced with the associated datasets, and the metadata of the associated datasets will not be overwritten.

**Output node datasets** will be imported, with two import modes:


* New: Create the dataset in the current project. If a dataset with the same name exists, the import will fail.

* Associate with existing dataset: During import, the dataset will be replaced with the associated dataset. The system will compare the metadata differences between the original dataset and the associated dataset, and the user can choose whether to overwrite.


 **(3) Configure data connections**

In the **Data Connection** list, the data connections referenced by the currently selected visual modeling task are displayed, and data connections available for association in this project are provided for user selection. When importing a visual modeling task, the system will automatically replace the data connection in the task with the data connection you select.

 **(4) Configure cluster queue**

In the **resource queue** list, the resource queues used by the selected visual modeling tasks are displayed. Please select a resource queue suitable for "scheduled tasks" from the dropdown list. When importing a visual modeling task, the system will automatically replace the resource queue in the task with the queue you select.

 **(5) Import permission information**

In the target project, the system will search for the creator of the original resource and the task owner. If found, the permissions will be associated with the corresponding user; if not found, the permissions will be associated with the importer.

<span id="1c9e4b89"></span>
### 3.2.4 Overwrite method

 **(1) Select resources to import**

When you choose overwrite as the import method, you can view the task names of resources to be imported in the resource list and select which resource in this project to overwrite. You can also choose whether to overwrite the task name, description, and storage directory.

**Overwrite logic**: The datasets, data connections, and queues in the visual modeling task will be processed according to the configured mapping relationships, and the remaining content will be overwritten.

 **(2) Import datasets**

For datasets associated with the visual modeling task, you can create new datasets or associate them with existing datasets based on your selection.

 **(3) Configure data connection**

In the **data connection** list, the data connections referenced by the currently selected visual modeling tasks are displayed, and the data connections available for selection in this project are available for users to select. When importing a visual modeling task, the system will automatically replace the data connection in the task with the data connection you select.

 **(4) Configure cluster queue**

In the **resource queue** list, the resource queues used by the selected visual modeling tasks are displayed. Please select a resource queue suitable for "scheduled tasks" from the dropdown list. When importing visual modeling tasks, the system will automatically replace the resource queue in the task with the queue you selected.

 **(5) Import permission information**

After importing permissions, the resource Owner will be consistent with the source resource, and resource permissions will be added on top of the original ones. If permissions are not imported, the Owner and permission information of the current project's resources will remain unchanged.

<span id="5690398b"></span>
### 3.2.5 Perform the import operation

After completing the above operations, you can click the "Import" button. The system will import the resources you selected for import.

During the import process, the import process will be displayed.

After the import is complete, an overview of successful and failed cases will be displayed, and you can download the import details.

<span id="8ab40bef"></span>
# 4. Permission description

<span id="e093f41e"></span>
## 4.1 Resource export

(1) Users with "**visual modeling task module edit permission**" or "**project edit**" permission can access this page, including system administrators, group administrators, project administrators, and users with module permission points.

(2) Users who access this page can export tasks and output datasets for which they have **management permission**. Data connections and input datasets are not subject to permission checks.

<span id="736de713"></span>
## 4.2 Resource import

(1) Users with "**visual modeling task module edit permission**" or "**project edit**" permission can access this page.

(2) Method for creating new tasks:


* Task resource permissions: No permission check, any importer can create new tasks.

* Input dataset permissions: To associate an existing dataset, **management permission** for that dataset is required.

* Output dataset permissions: No check for new datasets; to associate an existing dataset, **management permission** for that dataset is required.

* Data connection: To associate an existing data connection, **management permission** for the data connection is required.

* Permission information:

   * If permission information is imported: The task owner is user A from the source project. A must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.

   * If permission information is not imported: The task owner is B, the importer. B must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.


(3) Task overwrite approach:


* Task resource permissions: **Management permission** is required.

* Input dataset permissions: When associating an existing dataset, **management permission** for that dataset is required.

* Output dataset permissions: No check is performed for newly created datasets. When associating an existing dataset, **management permission** for that dataset is required.

* Data connection: When associating an existing data connection, **management permission** for the data connection is required.

* Permission information

   * Importing permission information: The task owner will be replaced. The task owner is A from the source project. A must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.

   * Not importing permission information: The task owner is C from the current project. C must be automatically granted **read permission** for the input node dataset and **write permission** for the output node dataset; otherwise, the task may fail to run.
