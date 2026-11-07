---
title: "Create host group (IP address)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_an_IP_address-based_host_group"
---

This topic describes how to create an IP address\-based host group.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A server is prepared as the log source. If the server is a BytePlus ECS, it must be in the same region as the project.

* If **BytePlus ECS** is not enabled, install the latest version of LogCollector on servers before adding ECS servers to the host group in batches. For details, see [Install LogCollector](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Under each BytePlus primary account, up to 200 host groups can be created per region. In each host group, up to 200 IP addresses can be added.

* Currently, only Linux servers are supported.

* Servers in a host group are identified and distinguished by IP address. By default, the IP address of the first network card is used for identification. You can also specify a different IP address via the `ip` parameter during initialization. For details, see [Install LogCollector](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).

* Only LogCollector V1.0.8 and later versions support auto\-upgrade. If you need to enable auto\-upgrade, make sure all servers that are ready to join host group have the required version installed before you create the host group. Otherwise, LogCollectors that do not meet the version requirements can not be auto\-upgraded. For LogCollector V1.0.7 and previous versions, refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host) for upgrade instructions.

* LogCollector does not support auto\-upgrade in container scenarios. If needed, replace the image manually.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Obtain the IP address of the host machine (configured when ECS is not enabled).

   Servers in a host group are identified by IP address. Before creating IPaddress\-based host group, obtain the IP address reported by LogCollector from the host machine or container. You can view this IP address in `ip` field under `/usr/local/logcollector/agent_info.json` file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the Logcollector version is below v2.2.0, the configuration file path is <code>/usr/local/filebeat-7.12.0/agent_info.json</code>. To check the LogCollector version, see <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">Checking the software version</a>.   </div>
   

   As shown below, log in to the specified host machine and check the `ip` field in the `/usr/local/logcollector/agent_info.json` file.

   ```Bash
   hostname:/home # cat /usr/local/logcollector/agent_info.json
    {
            "hostname": "logcollector-dnwwc",
            "ip": "10.56.*.*",
            "logcollect_version": "2.2.1",
            "update_time": "2025.01.14 15:19:29"
    }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, LogCollector takes the IP address of the first network card as the IP address of current host or container and reports it to the server. You can also manually specify the IP address or modify the IP address obtaining policy in LogCollector. For details, see <a href="https://docs.byteplus.com/docs/tls/configure_an_ip_address_for_a_host_or_container">Setting IP address for host or container</a>.   </div>
   

2. Log in to the [Torch log service console](https://console.byteplus.com/tls).

3. Select the region where TLS is located from the top navigation bar.

4. On the left navigation bar, select **Resource management \>**   **Host group**.

5. On the **Host group management** page, click **Create host group**.

6. In the **Create host group** dialog box, fill in the basic information of the host group, and then click **Create**.

   
   |Parameter |Description |
   |---|---|
   |Host group name |Name of the host group. |
   |Host group type |Type of host group. Set this as the **IP address**. |
   |ECS |If enabling ECS, ECS instances can be added to the current host group. After enabling, you must manually select the ECS instance that needs to be added.<br><br><br>* Only supports adding ECS instances with Cloud Assistant installed and both Cloud Assistant and the instance are in **Running** status.<br><br>* The system automatically installs LogCollector for the selected ECS instances.<br><br>* ECS instances that have started installing LogCollector cannot be stopped or uninstalled. Proceed with caution. |
   |IP address |Server IP address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Enter the server IP address you obtained in step 1.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding multiple machines to the host group, you can separate IP addresses with Chinese commas, English commas, spaces, or newlines.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Servers with Windows are not supported for now.</div><br> |
   |LogCollector service log |You can choose whether to enable the LogCollector service log. When enabled, the LogCollector client records runtime status and collection progress information in real time during operation.<br><br>For detailed instructions, see [service logs](https://docs.byteplus.com/docs/tls/service_logs_overview). |
   |LogCollector auto upgrade |LogCollector V1.0.8 and later versions support automatic upgrades. Once enabled, the log service will run an upgrade check at the specified time each day. If all upgrade criteria are met, LogCollector will upgrade automatically. No manual action is required.<br><br>For automatic upgrades, we recommend that you set it during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.<br><br><br>* Versions before LogCollector V2.3.1: Click the switch to enable or disable the automatic upgrade feature.<br><br>   * Set the automatic upgrade time after enabling the feature.<br><br>   * If you need a newer version of LogCollector after disabling auto upgrade, refer to [Upgrade LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host) for steps.<br><br>* LogCollector V2.3.1 and later versions: After creating the host group, go to the **LogCollector management** tab on the host group details page to enable it. For details, see [View host group](https://docs.byteplus.com/docs/tls/View_a_host_group). |
   |IAM Project |Select the IAM project to which the currently created host group belongs from the dropdown list.<br><br>If you have not created any IAM project or can not find a suitable one, click **Create project** to create a new IAM project. If no IAM project is specified, TLS categorizes the host project into the IAM project named `default`. |
   


<span id=".5ZCO57ut5pON5L2c"></span>
## View the LogCollector connection status for the host group

The host machine with LogCollector installed regularly reports its heartbeat status to TLS. You can check whether LogCollector and TLS are connected properly based on the heartbeat status. After successfully creating a host group, you can view the overall heartbeat status on the **host group management** page.

The **heartbeat status** column displays the number of IP addresses and the number of servers in each status.


* **Normal**: The connection between LogCollector on the server and TLS is normal.

* **Abnormal**: Some machines in the host group are in abnormal status. To view the IP addresses of servers with heartbeat abnormalities, click the host group name.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After adding servers to the host group, the server heartbeat status will briefly show as <strong>Abnormal</strong> until LogCollector successfully reports the heartbeat status to TLS. If the server heartbeat status remains <strong>Abnormal</strong> for more than 1 minute, we recommend that you refer to <a href="https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_host">Host group heartbeat issue troubleshooting</a> for resolution.</div>
