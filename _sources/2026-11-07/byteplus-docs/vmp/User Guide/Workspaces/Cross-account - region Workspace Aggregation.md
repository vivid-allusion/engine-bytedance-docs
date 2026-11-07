---
title: "Cross-account/region Workspace Aggregation"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Global_aggregation_across_accounts_and_regions"
---

Large enterprises often create multiple accounts in the cloud and assign different accounts to different departments or organizations. As an enterprise administrator, it is necessary to aggregate and query data across workspaces under different accounts to have an overview of the enterprise's resources and business information. The Vital Managed Service for Prometheus aggregation query workspace supports cross\-account and cross\-region aggregation, allowing the aggregation of workspaces from different accounts within the same enterprise.

<span id="XzIDYRSu"></span>
## Background Information

<span id="Dyv9Jfeo"></span>
### Enterprise organization

The enterprise organization service is a multi\-account management service provided by BytePlus. The enterprise organization maintains the relationships between multiple accounts in the cloud and provides the underlying support capabilities for other services in enterprise cloud adoption. You can create an enterprise organization and unify the management of your BytePlus root user accounts of your company and its subsidiaries by inviting or creating accounts to join the enterprise organization. At the same time, accounts and organizational units can be tagged, classified, and managed through Resource tags, and permissions of accounts within the organization can be controlled through organizational policies.

In the BytePlus enterprise organization, the following roles are mainly involved:


* **Enterprise administrator**: administrator of the enterprise organization, with the highest data read and write permission within the account group, able to access, manage, and assign other member accounts.

* **Organizational unit**: a node that carries the organizational structure in the enterprise organization, supporting the binding of accounts or other level organizational units to this node. Using organizational units, it is easy to manage a category of accounts, for example, all accounts related to subsidiary A are bound under the A organizational unit node, while the control policy **prohibit access to Cloud Enterprise Network** is bound to the A organizational unit node, uniformly controlling the permission scope of all member accounts of subsidiary A.

* **Member account**: a member within the enterprise organization, subject to access, management, and assignment by the administrator. Resource and billing between member accounts are naturally completely isolated, and member accounts can be separately established to segment IT projects or company organizations with no resource interconnection or strict confidentiality requirements.


<span id="4CbPV2Va"></span>
### Trusted service

To help enterprise organizations integrate with cloud services, enterprise organizations support designating cloud services (for example: Vital Managed Service for Prometheus) as enterprise organization's **trusted services**, that is, configuring mutual trust relationships between the enterprise organization and the cloud service. Once the cloud service becomes a trusted service, it can access the account structure within the enterprise organization. The enterprise organization's administrator can also perform organization\-based business operations within the trusted service, facilitating the achievement of enterprise cloud business goals.

<span id="mBsgiTb5"></span>
## Usage Limits


* When aggregating cross\-region workspaces, only aggregation of Common workspaces is supported, Local workspaces aggregation is not currently supported.

* When aggregating cross\-region workspaces, the **Johor** region is not currently supported. For more details, refer to [Regions and Availability Zones](https://docs.byteplus.com/en/docs/vmp/Regions-and-availability-zones).


<span id="mBsgiTb5"></span>
## Prerequisites


* The enterprise organization has been created, and organizational units and control policies have been configured.

* Member accounts have been invited or created in the enterprise organization.

* The member account has created a Vital Managed Service for Prometheus common workspace. For details, please refer to [Create a common workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* The member account has integrated cloud product monitoring data into the Vital Managed Service for Prometheus common workspace. For details, please refer to [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring) and [Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services).


<span id="BGoRHOKb"></span>
## Operation Procedure

<span id="nyZJiPEQ"></span>
### Scenario 1: Cross\-Region workspace aggregation

The cross\-region workspace aggregation scenario allows you to aggregate workspaces in different regions under the same account. This is applicable for scenarios where monitoring data exists in multiple regions under one account. You can perform the following steps to configure the IAM user:


1. Log in to the [VMP Console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Workspace** to go to the workspace list page.

4. Click **Create**, and click the **Aggregation workspace** tab to configure the aggregation query workspace.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46a1bbd3bf54fdd407b17e340db36ab1.png) </span>

   
   |Parameter |DescriptionS |
   |---|---|
   |Aggregate query workspace name |Specify a name for the aggregation workspace. The name is in the string format and must be 1 to 100 characters in length. |
   |Description |Specify the description of the aggregation query workspace. You can specify the detailed information about the workspace, including the purpose and scope of the workspace. |
   |BasicAuth |Configure the Basic Auth authentication feature.<br><br><br>* When the Basic Auth feature is disabled, the workspace only supports authentication via **BytePlus AK/SK** for data query.<br><br>* When the Basic Auth feature is enabled, the workspace supports authentication via **username and password** or **BytePlus AK/SK** for data query. |
   |User name |Specify a username used for basic authentication.<br><br><br>* The username can contain uppercase and lowercase letters, digits, and underscores (_)`_`。<br><br>* The username must be 2 to 32 characters in length. |
   |Password |Specify the password used for basic authentication.<br><br><br>* The password can contain uppercase and lowercase letters, digits, and special characters and must contain at least three of the preceding characters.<br><br>* Special characters include`!`,`@`,`#`,`$`,`%`,`^`,`*`,`&`,`(`,`)`,`_`,`+`,`-`,`=`。<br><br>* The password must be 8 to 32 characters in length. |
   |Confirm password |Enter the password used for basic authentication again to ensure the two passwords are identical. |
   |Whether to ignore a single workspace query error |Specify whether to ignore the query errors of a single workspace during queries.<br><br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a23fe514b7cf317a3f7ce6fdc2d3a51b.png) </span>Ignores the query errors of a single workspace. If an error occurs in a workspace, only data queried from other workspaces will be returned. This is suitable for scenarios where high accuracy of monitoring data is not required.<br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b1e4b6b24897ecfec6af06c69491d3d.png) </span>Does not ignore the query errors of a single workspace. If an error occurs in a workspace, an error in the entire aggregation workspace is reported during queries. This is suitable for scenarios where high accuracy of monitoring data is required. |
   |Select the workspace to aggregate |select the workspaces that need to be aggregated for query. select **Current account** to aggregate workspaces under the current account. |
   |All Regions |whether to aggregate workspaces in different regions under the current account.<br><br><br>* **Enable**: indicates querying all workspaces under the current account across different regions. check workspaces in different regions in the workspace list to achieve cross\-region workspace aggregation.<br><br>* **Disable**: indicates querying only all workspaces under the current account in the current region. |
   

5. Click **Submit**, and wait for the system to create the workspace.


<span id="uPiMXMQk"></span>
### Scenario 2: Cross\-account workspace aggregation

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only enterprise organization administrator accounts and proxy administrator accounts support cross\-account aggregation of member accounts' workspaces within the enterprise.</div>


The cross\-account workspace aggregation scenario allows you to use enterprise organization administrator accounts and proxy administrator accounts to aggregate workspaces created by different member accounts in different regions. You can perform the following steps to configure the IAM user:


1. Log in with enterprise organization administrator account or proxy administrator account to the [VMP service console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Workspace** to go to the workspace list page.

4. Click **Create**, and click the **Aggregation workspace** tab to configure the aggregation query workspace.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfd590c78c12b2cb8faf2a6d8f59a23a.png) </span>

   
   |Parameter |DescriptionS |
   |---|---|
   |Aggregate query workspace name |Specify a name for the aggregation workspace. The name is in the string format and must be 1 to 100 characters in length. |
   |Description |Specify the description of the aggregation query workspace. You can specify the detailed information about the workspace, including the purpose and scope of the workspace. |
   |BasicAuth |Configure the Basic Auth authentication feature.<br><br><br>* When the Basic Auth feature is disabled, the workspace only supports authentication via **BytePlus AK/SK** for data query.<br><br>* When the Basic Auth feature is enabled, the workspace supports authentication via **username and password** or **BytePlus AK/SK** for data query. |
   |User name |Specify a username used for basic authentication.<br><br><br>* The username can contain uppercase and lowercase letters, digits, and underscores (_)`_`。<br><br>* The username must be 2 to 32 characters in length. |
   |Password |Specify the password used for basic authentication.<br><br><br>* The password can contain uppercase and lowercase letters, digits, and special characters and must contain at least three of the preceding characters.<br><br>* Special characters include`!`,`@`,`#`,`$`,`%`,`^`,`*`,`&`,`(`,`)`,`_`,`+`,`-`,`=`。<br><br>* The password must be 8 to 32 characters in length. |
   |Confirm password |Enter the password used for basic authentication again to ensure the two passwords are identical. |
   |Whether to ignore a single workspace query error |Specify whether to ignore the query errors of a single workspace during queries.<br><br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a23fe514b7cf317a3f7ce6fdc2d3a51b.png) </span>Ignores the query errors of a single workspace. If an error occurs in a workspace, only data queried from other workspaces will be returned. This is suitable for scenarios where high accuracy of monitoring data is not required.<br><br>* <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b1e4b6b24897ecfec6af06c69491d3d.png) </span>Does not ignore the query errors of a single workspace. If an error occurs in a workspace, an error in the entire aggregation workspace is reported during queries. This is suitable for scenarios where high accuracy of monitoring data is required. |
   |Select the workspace to aggregate |Select the workspace to aggregate query, select **All accounts in the organization**, indicating the aggregation of workspaces created by other accounts in the enterprise organization.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In the <strong>Owned account</strong> column of the workspace list, the workspaces marked with <strong>Current account</strong> indicate the workspaces created by the currently logged\-in account. Those not marked indicate the workspaces created by other accounts in the enterprise organization.</div><br> |
   |Trusted service |Enable or disable the trusted service. The default is enabled and configuration is not supported.<br><br><br>* **Enable**: enable cross\-account trusted service and allow workspaces created by other accounts in the aggregated enterprise organization.<br><br>* **Disable**: disable cross\-account trusted service and prohibit workspaces created by other accounts in the aggregated enterprise organization. |
   

5. Click **Submit**, and wait for the system to create the workspace.


<span id="lt0kGN7K"></span>
## Result validation.

<span id="kHzycGiZ"></span>
### Obtain the query URL

After the aggregation query workspace is created, you can view the workspace in the workspace list.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2374fed959a658a7ba21edd057852649.png) </span>

Click the workspace name to go to the details page of the workspace, and allow viewing and obtaining the query URL of the workspace.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7515d70ad705d860444f1ed2e37a26c9.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.</div>



* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster">Deploying Grafana in a VKE cluster and integrating Grafana with a workspace</a></div>


* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace">Deploying Grafana on an ECS instance and integrating Grafana with a workspace</a></div>



<span id="WQkOCO1B"></span>
### Query aggregation metrics

You can use the Explore feature or Grafana to view the metrics in the aggregation query workspace. The `__ws__` label will be added to the metrics, which indicates the ID of the workspace where the metrics belong, such as `__ws__: f7a69888-***`.
