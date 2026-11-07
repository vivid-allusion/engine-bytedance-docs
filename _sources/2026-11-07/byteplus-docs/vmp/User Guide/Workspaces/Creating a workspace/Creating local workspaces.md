---
title: "Creating local workspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating_a_local_workspace"
---

The local workspace allows you to associate your self\-built or external Prometheus instances in the Vital Managed Service for Prometheus (VMP) console. This topic describes the procedure and considerations for creating a local workspace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · Apply for Trial]</strong>: This feature is currently in <strong>beta</strong>. If you want to use it, contact your account manager.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An external Prometheus instance has been created or obtained.


* If the self\-built Prometheus instance is located inside the VPC, the Query address must be configured for the instance.

* If the external Prometheus instance is deployed in an Internet data center (IDC) or another cloud provider:

   * No additional configuration is required when the external Prometheus instance has a public network address.

   * You need to first use Cloud Enterprise Network (CEN) to establish network connectivity and allow inbound traffic from the selected VPC CIDR block when the external Prometheus instance does not have a public network address.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you associate a local workspace with a self\-built Prometheus instance in an Elastic Compute Service (ECS) instance, you need to configure a security group for the ECS instance to allow traffic from the security groups and ports of the local workspace. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Associating_a_local_workspace_with_a_local_Prometheus_instance">Using a local workspace to associate a local Prometheus instance</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. Click **Workspace** in the left navigation bar to go to the workspace list page.

4. Click **Create**, and click the **Local workspace** tab to configure the local workspace.

   * **Basic information**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Name |Specify the name of the workspace. The name can contain Chinese characters, uppercase letters and lowercase letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`). The name must be 1 to 100 characters in length. |
      |Project |The project to which the workspace belongs. Project management is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
      |Tag |Add labels to the workspace. A label is used to identify the workspace. You can combine labels with selectors to filter workspaces. A label is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use labels for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
      |Address |Specify a query URL for the self\-built Prometheus instance. The address must start with HTTPS or HTTP. The address must be up to 1,000 characters in length. |
      |Description |Specify the description of the workspace. The description can contain Chinese characters, letters, digits, and special characters. The description must be 1 to 200 characters in length. |
      

   * **Permissions and network**

      
      |**Parameter** |**Descriptions** |
      |---|---|
      |Authentication method |Specify an authentication method for the custom Prometheus instance. Valid values:<br><br><br>* **Basic auth**: The username and password are used for authentication. When you select this method, you need to configure the username and password for your custom Prometheus instance.<br><br>* **Bearer token**: A token is used for authentication. When you select this method, you need to configure an authentication token for your custom Prometheus instance. |
      |Custom HTTP Header |Configure custom HTTP headers. The HTTP header is in the format of header and value. The header can contain Chinese characters, letters, and special characters and must be 1 to 200 characters in length.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can configure up to 10 groups of HTTP headers for the local workspace.</div><br> |
      |Network Configuration |You can configure one of the following methods of accessing the self\-built Prometheus instance:<br><br><br>* **Public network**: You can choose this method when your self\-built Prometheus instance is located in an IDC or another cloud provider, and can be accessed over the public network.<br><br>* **Private network**: You can choose this method when your self\-built Prometheus instance is located in a BytePlus VPC, or is located at another cloud provider but is connected to the BytePlus VPC via a dedicated line. When you select Private VPC access, you need to specify a VPC and its subnet. |
      

5. Click **Submit** to complete the configuration.


<span id="dzFrnoj1"></span>
## Connectivity test

After the configuration is complete, click the workspace name to go to the Overview page of the workspace. Click **Connectivity Test** to ensure that the configured local workspace can access the self\-built Prometheus instance.

<span id="PYaclDeU"></span>
## What to do next

The local workspace does not provide an access address and does not support metric queries through the Explore feature in the console. To query the metrics stored in the local workspace, you need to add the local workspace to the aggregation workspace and query metrics through the aggregation workspace. For details, see [Creating aggregation query workspaces](https://docs.byteplus.com/en/docs/vmp/Creating_an_aggregate_query_workspace).
