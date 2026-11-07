---
title: "Create Helm application"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_Helm_application"
---

An application is a unit that provides services externally and can be delivered independently. This article introduces how to create a Helm application.

<span id="UtRFfUVs"></span>
## Background information

**Helm application: ** A Helm application is an instance that is deployed and managed using the Helm tool, packaged and configured based on a Helm Chart, and runs in a K8s cluster. Helm applications simplify K8s application operations and maintenance (no need to manually operate YAML files) and support full lifecycle management of applications.

<span id="l4uMUFK0"></span>
## Prerequisites


* The workspace has been created. For specific operations, refer to [Create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

* Helm applications require the creation of a custom resource pool. For details, refer to [Custom resource pool](https://docs.byteplus.com/en/docs/cp/Integrate_custom_clusters).


<span id="e93aBhdG"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to the [Code Pipeline Console ](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **Application delivery \> Application management**.

2. On the application management page, click **Create application \> Helm application**.

3. On the create application page, fill in the relevant configuration information for the application as required.

   * Basic Information

      
      |Parameter |Description |
      |---|---|
      |Application ID |Fill in the Application ID according to the interface instructions. The Application ID is the unique identifier for the application and cannot be changed after creation. The value of the built\-in placeholder appName in the application orchestration YAML file will use the Application ID you provided. |
      |Application display name |Customize the application's display name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This name is not the resource name in the YAML file.</div><br> |
      |Member management |Quickly configure the members of the current application and assign different permissions to each member to meet the needs of multi\-role collaboration in application delivery.<br><br><br>* **Add member**: Add multiple members to the current application; only users with visible permissions in the current workspace can be selected.<br><br>* **Permission**: The system provides five built\-in roles: administrator, development, test, operations, and read\-only. For details about role permissions, refer to [Role permissions](https://docs.byteplus.com/en/docs/cp/Role_permissions). Each member can be assigned one or more role permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The BytePlus account is the default administrator of the application and cannot be removed.</div><br> |
      

   * Environment configuration

      
      |**Parameter** |**Description** |
      |---|---|
      |Environment |Select the environment type and customize the environment display name. |
      |Environment ID |Fill in the Environment ID as prompted by the interface. The Environment ID is the unique identifier for the environment and cannot be changed after creation. The value of the built\-in placeholder envName in the application orchestration YAML file will be set to the Environment ID you provide. |
      |Deploy resources |Select a created custom resource pool. |
      |Namespace |When deploying the current environment, the Namespace name specified here will override the Namespace defined in the application's orchestration YAML file. If the Namespace does not exist in the cluster to be deployed, it will be created during deployment. |
      

   * Application orchestration

      
      |**Parameter** |**Description** |
      |---|---|
      |Chart source |Currently, HTTP and OCI sources are supported.<br><br><br>* HTTP: Pull Chart resources via HTTP/HTTPS protocol, relying on the repository index file to locate the Chart package.<br><br>* OCI: Based on the container image standard storage method, stores the Chart as an OCI image in the container registry (such as Docker Hub), supports image authentication, and adapts to the container ecosystem. The Chart address must conform to the OCI format. |
      |Chart address |The path to obtain the Chart package for the Helm application. |
      |Skip certificate verification |Skip verification of SSL/TLS certificates related to the Helm repository or Chart during deployment. This is suitable for test environments where certificates are not properly configured, but it reduces security and is not recommended for production environments. |
      |Chart authentication method |Verify the method for accessing the Chart repository or pulling Chart permissions. Currently, either no authentication or authentication via username and password is supported. |
      |Enable reuse |After enabling, Helm is allowed to reuse existing resources (for example, ConfigMap and Secret). Existing resources with the same name will not be re\-created during deployment, reducing resource redundancy. This is suitable for scenarios where historical configurations need to be retained. |
      |Enable reset |After enabling, existing resources related to this Helm application will be reset before deployment (for example, deleting old version Pods and Services), clearing historical remnants to ensure the application is deployed in a fresh state and preventing interference from old resources. |
      

   * Advanced configuration

      
      |**Parameter** |**Description** |
      |---|---|
      |Add Value<br><br> |Add a key\-value pair. The configuration here takes precedence over the configuration in `values.yaml`. For example, if the image tag is set to `imagetag = v1.0.1` here, while the image tag in `values.yaml` is `imagetag = v1.0`, the final deployment will use the image tag `imagetag = v1.0.1`. |
      |YAML file |By configuring the `overwrite-value.yaml` file, override the configuration in the `values.yaml` file. |
      

4. Click **Confirm** to complete the operation.
