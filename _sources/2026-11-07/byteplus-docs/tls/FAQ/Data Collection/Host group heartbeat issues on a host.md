---
title: "Host group heartbeat issues on a host"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/host_group_heartbeat_issues_on_a_host"
---

When you use LogCollector to collect text logs of servers, the heartbeat status of hosts in the host group may be abnormal, resulting in issues such as log collection failures. This topic introduces how to troubleshoot such issues and restore the heartbeat status of hosts.

<span id="背景信息"></span>
## Background

LogCollector is a self\-developed log collection client of Torch Log Service (TLS), which can be used to quickly report log data of servers. After you install LogCollector on a host, LogCollector periodically sends heartbeat packets to the server. if the status of certain IP addresses is **abnormal** on the host group configuration page in the TLS console, it means a client\-server connection failure occurs.

<span id="问题现象"></span>
## Issue description

On the host group details page in the TLS console, if the status of certain IP addresses is **abnormal** in the **Heartbeat status** area, the LogCollector heartbeat status of the host is abnormal. This means the LogCollector client on the host fails to be connected to the server.

When the heartbeat status is abnormal, the LogCollector client on the host cannot report the collected log data to the server. As a result, the logs cannot be collected into topics, and you cannot search or query new log data in real time in the TLS console.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ead480f9f144701bef755db5a4350f8~tplv-goo7wpa0wc-image.image) </span>

<span id="排查方案"></span>
## Troubleshooting

<span id="_1-检查-logcollector-状态"></span>
### Step 1: Verify the LogCollector status

Log on to the host, then run the following command to view the LogCollector status:

```bash
systemctl status filebeatd.service
```



* If the response displays **Unit filebeatd.service could not be found**, it means LogCollector is not installed on the host. To solve the issue, install and run LogCollector. For more information, refer to [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).

   Make sure that LogCollector is installed correctly based on the Region where TLS is deployed and the network type.

* If the response displays **active (running)** , it means LogCollector is installed on the host and is running properly.

   If the LogCollector heartbeat status is still **abnormal** in the console, perform the following steps for further troubleshooting.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4fe8853824a0708d13adc7c6ef1fbbe9) </span>


<span id="_2-检查鉴权参数配置"></span>
### Step 2: Verify the authentication parameter settings

After you install LogCollector, execute an initialization script. During the initialization, configure authentication parameters for authentication and connecting to TLS. Incorrect parameter settings may cause LogCollector heartbeat errors.

Run the following command to open the `filebeat.yml` file and verify the authentication parameters:

```bash
cat /usr/local/filebeat-7.12.0/etc/filebeat.yml
```


The following table describes the authentication parameters:


|Parameter |Example |Description |How to Get |
|---|---|---|---|
|endpoint |https://tls\-ap\-southeast\-1.bytepluses.com |The endpoint of TLS, that is, the service URL. |Log on to the BytePlus console, and view the endpoint on the project details page. |
|secret_id |AKLY\*\*\*\*\*\*\*\*\* |The AccessKey ID of a BytePlus account. |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |TUdZ\*\*\*\*\*\*\*\* |The AccessKey secret of a BytePlus account. |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|region |ap\-southeast\-1 |The Region where a project is deployed. |In the top menu bar of the TLS console, view the Region where the project resides. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In <code>output.tls</code>, you cannot configure the ip and label parameters at the same time. Otherwise, heartbeat errors occur.</div>


An example of a configuration file is offered as follows:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8bb37a93783d53574b160ce61271482c) </span>

If the authentication parameters are incorrectly configured, modify them, restart LogCollector, and view the status of the host group later. If the LogCollector heartbeat status is still **abnormal** in the console, perform the following steps for further troubleshooting.

<span id="_3-检查-logcollector-是否为最新版本"></span>
### Step 3: Verify whether the latest LogCollector version is used

LogCollector supports host groups since v 1.0.1. If the version of LogCollector installed on the host is not v 1.0.1 or later, the LogCollector heartbeat status may be abnormal, and the server cannot recognize this LogCollector. Therefore, if the LogCollector heartbeat status is abnormal, verify whether the LogCollector version meets the requirements.

Run the following command to view the LogCollector version. The version of the currently installed LogCollector can be found in the response. We recommend that you use the latest LogCollector version. For more information, refer to [Upgrade LogCollector on a host](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host).

```bash
/etc/init.d/filebeatd -v
```


A response similar to the following example is returned:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_cc644ec99aef7a6b5fb63a9dd1487a93) </span>

If the LogCollector heartbeat status of the host is still **abnormal** in the console after you upgrade LogCollector, perform the following steps for further troubleshooting.

<span id="_4-检查机器组-ip-地址配置"></span>
### Step 4: Verify the IP address settings of a host group

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an IP address\-based host group is used, refer to this step for troubleshooting.</div>


By default, LogCollector reads the IP address of the first network interface of its host, and records the IP address in the `agent_info.json` file as the IP address of the host. When you create an IP address\-based host group in the console, type the IP address recorded in the `agent_info.json` file into the host group, to add the specified host to the host group.

If the IP address configured in the host group is inconsistent with that in the `agent_info.json` file, the console displays that the LogCollector heartbeat status of the host is abnormal and logs cannot be collected.

Run the following command to view the `agent_info.json` file and verify whether the IP address in the `ip` field is consistent with that in the console.


* View the `agent_info.json` file.

   ```bash
   cat /usr/local/filebeat-7.12.0/agent_info.json
   ```
   

   In the following response, the `ip` field indicates the current host IP address obtained by LogCollector, that is, the IP address of the first network interface.

   ```bash
   {
       hostname :  C02G64T1MD6R ,
       ip : 10.*.*.* ,
       logcollect_version :  1.0.2 ,
       update_time :  2022.01.07 18:38:12 
   }
   ```
   

* View the IP address configured in the console.

   On the details page of the host group, view the IP addresses of all hosts in the host group. If the IP address configured in the console is inconsistent with that in the `agent_info.json` file, modify the host group setting and verify the host status later.


<span id="_5-检查机器标识配置"></span>
### Step 5: Verify the host label settings

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a label\-based host group is used, refer to this step for troubleshooting.</div>


In a label\-based host group, the host label must be consistent with that configured in the LogCollector configuration file. Otherwise, the LogCollector heartbeat status cannot be found in the host group.

Run the following command to view the LogCollector configuration file:

```Plain
cat /usr/local/filebeat-7.12.0/etc/filebeat.yml
```


In the following response, the value of `label` is the host label configured in LogCollector. If this value is inconsistent with the host label configured in the host group, modify the host group setting and verify the host status later.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79b55f2869647045c25614d9fc1844ce.png) </span>
