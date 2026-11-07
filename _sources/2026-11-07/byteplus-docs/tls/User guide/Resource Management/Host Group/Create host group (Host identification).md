---
title: "Create host group (Host identification)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_a_label-based_host_group"
---

This topic describes how to create a host group with host identifiers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A server is prepared as the log source. If the server is a BytePlus ECS, it must be in the same region as the project.

* If you do not enable **ECS**, you must install LogCollector of version 1.0.3 or later versions on the server before adding multiple ECS servers to the host group. We recommend that you use the latest version. For download and installation instructions, see [Install LogCollector](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Each BytePlus primary account can create up to 200 host groups in each region.


* Currently, only Linux servers are supported.

* Only LogCollector V1.0.8 and later versions support auto\-upgrade. If you need to enable auto\-upgrade, make sure all servers that are ready to join host group have the required version installed before you create the host group. Otherwise, LogCollectors that do not meet the version requirements can not be auto\-upgraded. To upgrade LogCollector V1.0.7 and previous versions, refer to [Manual LogCollector upgrade](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host#.5omL5Yqo5Y2H57qnLWxvZ2NvbGxlY3Rvcg==).

* LogCollector does not support auto\-upgrade in container scenarios. If needed, replace the image manually.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps

<span id=".XzEt6YWN572u5py65Zmo5qCH6K-G"></span>
### 1. Configure host identification (when ECS is disabled)

If you need to add a server to a host group with host identification, specify the `label` parameter during LogCollector initialization on the server and enter a custom identifier.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For detailed initialization steps, see <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host">LogCollector installation and upgrade</a>.</div>


* <div data-tips="true" data-tips-type="tip">The identifier length must be 2–128 characters. It can include lowercase letters, numbers, hyphens (\-), and underscores (_).</div>


* <div data-tips="true" data-tips-type="tip">Host groups identify different containers by using IP addresses. By default, the IP address is the primary network interface address obtained by LogCollector. To make it easier to manage host groups, you can modify the IP address obtaining policy in LogCollector. For details, see <a href="https://docs.byteplus.com/docs/tls/configure_an_ip_address_for_a_host_or_container">Setting IP addresses for hosts or containers</a>.</div>



If you do not specify the `label` parameter during initialization, you need to stop LogCollector first. Then re\-run the initialization command with the correct parameter. After that, restart LogCollector. If you need to modify the machine identifier after setting it, you can follow the steps below.


1. Stop LogCollector.

   ```Bash
   sudo systemctl stop logcollectord.service
   ```
   

2. Re\-run the initialization command.

   For details of each parameter, see [2 Install and start LogCollector](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#be68b4c4).

   ```Bash
   sudo ./logcollector.sh install --region {region} --endpoint {endpoint} --secret_id {secret_id} --secret_key {secret_key} --label {label} 
   ```
   

3. Start LogCollector.

   ```Bash
   sudo systemctl start logcollectord.service
   ```
   


<span id=".XzIt5Yib5bu65py65Zmo57uE"></span>
### 2 Create a host group


1. Log in to the [Torch log service console](https://console.byteplus.com/tls).

2. Select the region where torch log service(TLS) is located from the top navigation bar.

3. On the left navigation bar, select **Resource management \>**   **Host group**.

4. On the **Host group management** page, click **Create host group**.

5. In the **Create host group** dialog box, enter the basic information for the host group, and then click **Create**.

   
   |Parameter |Description |
   |---|---|
   |Host group name |Name of the host group. |
   |Host group type |The type of host group. Select **Host identification**. |
   |Host identification |Enter the host identification you configured on your server. |
   |ECS |If enabling ECS,  ECS instances can be added to the current host group. After enabling, you must manually select the ECS instance that needs to be added.<br><br><br>* Only supports adding ECS instances with Cloud Assistant installed and both Cloud Assistant and the instance are in **Running** status.<br><br>* The system automatically installs LogCollector for selected ECS instances.<br><br>* ECS instances that have started installing LogCollector cannot be stopped or uninstalled. Proceed with caution. |
   |LogCollector service log |You can choose whether to enable the LogCollector service log. When enabled, the LogCollector client records information like runtime status and collection progress in real time during operation.<br><br>For detailed instructions, see [service logs](https://docs.byteplus.com/docs/tls/service_logs_overview). |
   |LogCollector auto upgrade |LogCollector V1.0.8 and later versions support automatic upgrades. Once enabled, the log service will run an upgrade check at the specified time each day. If all upgrade criteria are met, LogCollector will upgrade automatically. No manual action is required.<br><br>For automatic upgrades, we recommend that you set it during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.<br><br><br>* Versions before LogCollector V2.3.1: Click the switch to enable or disable the automatic upgrade feature.<br><br>   * Set the automatic upgrade time after enabling the feature.<br><br>   * If you need a newer version of LogCollector after disabling auto upgrade, refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host) for steps.<br><br>* LogCollector V2.3.1 and later versions: After creating the host group, go to the **LogCollector management** tab on the host group details page to enable it. For details, see [View host group](https://docs.byteplus.com/docs/tls/View_a_host_group). |
   |IAM Project |Select the IAM project to which the currently created host group belongs from the dropdown list.<br><br>If you have not created any IAM project or can not find a suitable one, click **Create project** to create a new IAM project. If no IAM project is specified, TLS categorizes the host project into the IAM project named `default`. |
   


<span id=".5ZCO57ut5pON5L2c"></span>
## View host group LogCollector connection status

The host machine with LogCollector installed regularly reports its heartbeat status to TLS. You can check whether LogCollector and TLS are connected properly based on the heartbeat status. After successfully creating a host group, you can click the host group name on the **Host group management** page to view the heartbeat status of each server in the host group.

The **Heartbeat status** tab displays the IP addresses in the **IP** column for servers with the same server identifier. Servers within the host group are identified and distinguished by their IP addresses. By default, IP address is the current server address obtained by LogCollector, i.e., the IP address of the first network card.

You can verify that the number of IP addresses matches the number of servers actually configured with identifiers, and view the heartbeat status of each server.


* If the status column shows **Normal**: TLS has successfully identified this server, and both the server LogCollector and TLS connection status are normal.

* If the status column shows **Abnormal**: some machines in the host group are in abnormal status. To view the IP addresses of servers with heartbeat anomalies, click the host group name.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After adding servers to the host group, the server heartbeat status will briefly show as <strong>Abnormal</strong> until LogCollector successfully reports the heartbeat status to TLS. If the server heartbeat status remains <strong>Abnormal</strong> for more than 1 minute, we recommend that you refer to <a href="https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_host">Host group heartbeat issue troubleshooting</a> for step\-by\-step diagnosis and resolution.</div>


* <div data-tips="true" data-tips-type="tip">For host groups based on host identification, if you restart a server that is in abnormal status, the IP address of the server will change. TLS will fail to check the heartbeat status via original IP address. Therefore, the abnormal IP address record will remain. In this case, we recommend that you check the number of hosts with normal heartbeat status. If the number matches the actual number of servers, the error message for the abnormal status can be ignored.</div>
