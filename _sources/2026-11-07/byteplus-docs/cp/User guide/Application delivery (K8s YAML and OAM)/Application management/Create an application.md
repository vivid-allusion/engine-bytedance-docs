---
title: "Create an application"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_an_application"
---

An application is an independently deliverable unit that offers services to external users. This article explains how to create an application.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information


* **K8s YAML application**

   Define and orchestrate applications using native K8s YAML. This is intended for developers who are familiar with Kubernetes.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The workspace has been created. For detailed instructions, see [Creating a workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name to enter that workspace.

   4. From the left navigation bar, select **Application delivery \> Application management**.

2. On the application management page, click **create application**.

3. On the Create Application page, fill in the relevant application configuration information as instructed.

   * **K8s YAML application**

      
      |Configuration Item |Descriptions |
      |---|---|
      |Application ID |Enter the Application ID as prompted by the interface. The Application ID is the unique identifier for the application and cannot be changed after it is created. In the application orchestration YAML file, the value of the preset placeholder appName will be set to the Application ID you enter. |
      |Application name |Display name of the custom application.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This name is not the resource name in the YAML file.</div><br> |
      |Description |Enter remarks for the current application. This field can be left empty. |
      |Member management |Quickly configure the members of the current application and set different permissions for each member to meet the requirements of multi\-role collaboration in application delivery.<br><br><br>* **Add members**: Add multiple members to the current application. Only users who have visibility permissions for the current workspace are eligible for selection.<br><br>* **Permissions**: The system includes five predefined roles: administrator, developer, tester, operations, and read\-only. For details about role permissions, see [Role permissions](https://docs.byteplus.com/en/docs/cp/Role_permissions). Each member can be configured with permissions for one or more roles.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The BytePlus account is set as the administrator of the application by default and cannot be removed as the administrator.</div><br> |
      |Deployment methods |Currently, only **predefined K8s YAML deployment** is supported, that is, deploying applications via K8s YAML description files. |
      

4. Uncheck "Continue initializing the application process", click **OK**, and the application will be created. After the application is created, it is displayed as shown in the figure.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Create a deployable environment for the application to facilitate subsequent application orchestration and configuration management. For detailed instructions, see [Create an environment](https://docs.byteplus.com/en/docs/cp/Create_environments).
