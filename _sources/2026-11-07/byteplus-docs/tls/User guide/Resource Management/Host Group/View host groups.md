---
title: "View host groups"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/View_a_host_group"
---

After creating a host group, you can go to Host group detail page to view its information, including basic information, the heartbeat status of all machines in the group, the associated collection configuration, and LogCollector management.

<span id="ee745708"></span>
## Steps


1. Log in to the [Torch log service console](https://console.byteplus.com/tls).

2. Select the region where torch log service(TLS) is located from the top navigation bar.

3. On the left navigation bar, select **Resource management \>**   **Host group**.

4. On the **Host group management** page, click the name of the specified host group.

   The host group details page includes the **Host group information** section, **Heartbeat status** tab, **Associated collection configuration** tab, and **LogCollector management** tab.


<span id=".5p-l55yL5Z-65pys5L-h5oGv"></span>
## View host group information

The **Host group information** section displays the basic details of the current host group, including the host group ID, type, and creation time.


|Display item |Description |
|---|---|
|Host group ID |ID of the current host group. |
|Host group type |The host group type refers to either IP address type or host identification type. |
|Host identification |Host identification that is configured for the host group. Displayed only when **host group type** is set to **host identification**. |
|Create on |The creation time of host group. |
|Modified on |Last modification time for host group configuration. |
|IAM Project |The IAM project to which the host group belongs. |


<span id=".5p-l55yL5b-D6Lez54q25oCB"></span>
## View heartbeat status

In **Heartbeat status** tab, you can view lists of all hosts, abnormal hosts, or normal hosts.

The list displays the status and LogCollector versions for each host. In the upper right corner of this section, you can enter IP address in the search box to view details for a specific IP address.


|Display item |Description |
|---|---|
|IP |The IP address of the servers in the host group. By default, the first network interface's IP address is used.<br><br>You can also specify another IP address during initialization via the `ip` parameter. For details, see [Install LogCollector](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host). |
|Status |LogCollector connection status with the server and TLS.<br><br><br>* **Normal**: LogCollector is successfully installed on this host; the connection between LogCollector and TLS is normal.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When <strong>host group type</strong> is <strong>host identification</strong>, only servers with <strong>Normal</strong> heartbeat status are displayed (i.e., host that is configured with host identification and maintains normal communication with the server). If the number of servers with <strong>host identification</strong> configured does not match the number shown in the host group, some servers may have a failed LogCollector heartbeat. Refer to <a href="https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_container">FAQ</a> for troubleshooting.   </div><br>   <br><br>* **Abnormal**: LogCollector connection on this machine is abnormal. Refer to [Troubleshoot host group heartbeat](https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_host) for troubleshooting.<br><br>   If the abnormal situation does not affect your business and too many records exist, click **Clear abnormal hosts** to remove all abnormal heartbeat records in one step. |
|LogCollector version |The installed LogCollector version on the corresponding server. |


<span id=".5p-l55yL5YWz6IGU6YeH6ZuG6YWN572u"></span>
## View associated collection configurations

The **Associated collection configurations** tab shows the list of associated collection configurations. The list displays the configuration name, ID, and log type.


|Actions |Description |
|---|---|
|View collection configuration |Click the specified collection configuration name to enter the details page. Information like basic information, collection rules, and host group information are displayed.<br><br>You can edit collection rules, associate host groups, and delete or pause the collection configuration on this page. |
|Associate collection configuration |First click **Collection rule association**. Then select the collection configuration to associate and click **OK**. |
|Unbind collection configuration |Locate the specified associated collection configuration, click **Unbind host group** in **Actions** column. Confirm the information, and then click **OK.** <br><br>After the host is unbound, servers in the host group will stop collecting logs according to this collection rule. For detailed steps, see [LogCollector collection configuration management](https://docs.byteplus.com/docs/tls/logcollector_collection_rule_management). |


<span id="10493721"></span>
## Manage LogCollector

In **LogCollector management** tab, you can manually upgrade or downgrade LogCollector, enable automatic upgrades, and restart host groups in batches.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">LogCollector V2.3.1 and later support the <strong>LogCollector management</strong> tab. </div>


* <div data-tips="true" data-tips-type="tip">Only LogCollector that is deployed on physical machine supports upgrading and downgrading.</div>




|Actions |Description |
|---|---|
|Manual upgrade or downgrade |Shows whether the current LogCollector can be manually upgraded or downgraded in the console. This feature is supported only by LogCollector version V2.3.1 and later. For manual upgrades or downgrades for other versions, see [Upgrade LogCollector (Host)](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host) and [Upgrade LogCollector (Kubernetes Cluster)](https://docs.byteplus.com/docs/tls/upgrade_logcollector_in_a_kubernetes_cluster).<br><br><br>* If the **upgrade and downgrade** button is greyed out: manual upgrade and downgrade are currently not supported.<br><br>* If the **upgrade and downgrade** button is available: manual upgrade and downgrade are currently supported. Click **Upgrade and downgrade** and select the LogCollector version that you want to upgrade or downgrade. Then click **OK** to manually complete the LogCollector version upgrade or downgrade.<br><br>   LogCollector stops collecting data during the upgrade or downgrade period. We suggest that you schedule the upgrade or downgrade time appropriately. |
|Auto upgrade |Shows whether the automatic upgrade feature for LogCollector is enabled.<br><br><br>* **Enabled**: Automatic upgrade is enabled, and the upgrade time is displayed. To change the automatic upgrade time or disable the automatic upgrade feature, click **Modify**.<br><br>* **Disable**: The automatic upgrade feature is not enabled. To enable the automatic upgrade feature and set the upgrade time, click **Modify**. |
|Restart host groups in bulk |Show whether host groups can be restarted in batches.<br><br><br>* If **Restart** button is disabled: Batch restart host group is not supported for now.<br><br>* If **Restart** button is available: Batch restart host group is supported. To batch restart host groups, click **Restart**, and confirm the prompts before you click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Do not rename or delete log files during the restart process. Otherwise, some logs may fail to be collected.   </div><br>    |
|Configuration |Displays startup parameters, total configuration assignments, successful assignments, and failed assignments. For details on startup parameters, see [Configure LogCollector startup parameters](https://docs.byteplus.com/docs/tls/Configure-the-startup-parameters-of-LogCollector).<br><br>If no configuration item is present, click **Add configuration**, and then enter the configuration details before you click **OK**. The system will deliver the configuration later. |
