---
title: "Creating aggregation query workspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating_an_aggregate_query_workspace"
---

If you need to view monitoring data of multiple workspaces, you can create an aggregation query workspace for a global view. This topic describes the procedure and considerations for creating an aggregation query workspace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · Apply for Trial]</strong>: This feature is currently in <strong>beta</strong>. If you want to use it, contact your account manager.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Limits

The aggregation query workspace must be associated with at least one common workspace.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A common workspace or a local workspace has been created. For more details, refer to [Creating common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces) and [Creating local workspaces](https://docs.byteplus.com/en/docs/vmp/Creating_a_local_workspace).

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation Procedures


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. On the left navigation bar, click **Workspace** to go to the workspace list page.

4. Click **Create**, and click the **Aggregated workspace** tab to configure the aggregation query workspace.

   
   |Parameter |Descriptions |
   |---|---|
   |Aggregation query workspace name |Specify a name for the aggregation workspace. The name is in the string format and must be 1 to 100 characters in length. |
   |Description |Specify the description of the aggregation query workspace. You can specify the detailed information about the workspace, including the purpose and scope of the workspace. |
   |Project |The project to which the workspace belongs. Project management is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, while streamlining expense allocation and auditing for diverse cloud resources.  |
   |Tags |Add labels to the workspace. A label is used to identify the workspace. You can combine labels with selectors to filter workspaces. A label is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use labels for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
   |Enable custom authentication (optional) |By default, the aggregation query workspace supports authentication through  **AK/SK** for data writing and query. You can also manually enable and configure custom authentication based on your business requirements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The common workspace provides dual\-mode <strong>AK/SK</strong> authentication capability by default:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Use the standard signature method of <strong>AK/SK</strong> to complete identity verification by carrying signature information in the request header.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Use the  <strong>AK</strong> as the username and the <strong>SK</strong> as the password to complete basic authentication. This meets the access requirements of third\-party tools.</div><br><br><br>* **Enable custom authentication**: After you enable this option, workspaces support **custom authentication** and **BytePlus AK/SK** authentication. Custom authentication is categorized into the following two types: **Basic Auth** and **Bearer Token**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Basic Auth</strong> and <strong>Bearer Token</strong> cannot be both enabled.   </div><br>   <br><br>   * **Basic Auth**: A basic authentication method that supports authentication through custom usernames and passwords, which achieves data writing and query.<br><br>   * **Bearer Token**: A token\-based authentication method that supports authentication through tokens, which achieves data writing and query.<br><br>* **Disable custom authentication** (default): After you disable custom authentication, you can use the default  **AK/SK** method to perform authentication. |
   |Basic Auth (optional) |You need to specify the following parameters only if **Enable custom authentication** is enabled and **Basic Auth** is used for authentication.<br><br><br>* **User name**: Specify a username used for Basic Auth authentication.<br><br>* **Password**: Specify a password used for Basic Auth authentication.<br><br>   * **Confirm password**: Enter the password used for basic authentication again and ensure the two passwords are identical. |
   |Bearer Token (optional) |You need to specify this parameter only if **Enable custom authentication** is enabled and **Bearer Token** is used for authentication.<br><br>You can click **auto generation** to obtain a **Token** or manually enter a **Token**. This token is used to validate requests and restrict the scope of operations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The bearer token will be stored by the system through reversible encryption to ensure token data security. To prevent risks caused by the manually configured token, such as weak passwords and repeated use, we recommend that you use the <strong>automatic generation</strong> feature of the   to obtain the token.</div><br> |
   |Should single workspace query errors be ignored |Specify whether to ignore the query errors of a single workspace during queries.<br><br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a23fe514b7cf317a3f7ce6fdc2d3a51b.png) </span>Ignores the query errors of a single workspace. If an error occurs in a workspace, only data queried from other workspaces will be returned. This is suitable for scenarios where high accuracy of monitoring data is not required.<br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b1e4b6b24897ecfec6af06c69491d3d.png) </span>Does not ignore the query errors of a single workspace. If an error occurs in a workspace, an error in the entire aggregation workspace is reported during queries. This is suitable for scenarios where high accuracy of monitoring data is required. |
   |Select the workspaces to aggregate. |Select workspaces for aggregation queries. At least 2 standard workspaces need to be selected.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only workspaces within the same region and the same account can be aggregated.</div><br> |
   

5. Click **Create now**, and wait for the system to create the workspace.


<span id=".57uT5p6c6aqM6K-B"></span>
## Verifying results

<span id=".6I635Y-W5p-l6K-i5Zyw5Z2A"></span>
### Obtain the query URL

After the aggregation query workspace is created, you can view the workspace in the workspace list.

Click the workspace name to go to the details page of the workspace, and allow viewing and obtaining the query URL of the workspace.

<span id=".5p-l6K-i6IGa5ZCI5oyH5qCH"></span>
### Query aggregation metrics

You can use the Explore feature or Grafana to view the metrics in the aggregation query workspace. The `__ws__` tag will be added to the metrics, which indicates the ID of the workspace where the metrics belong, such as `__ws__: f7a69888-***`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Use the custom Grafana to access the workspace and query metrics. Refer to <a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster">Deploying Grafana in a VKE cluster and accessing workspaces</a>.</div>
