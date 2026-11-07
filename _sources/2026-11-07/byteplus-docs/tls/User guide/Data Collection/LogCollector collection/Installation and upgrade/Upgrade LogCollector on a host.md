---
title: "Upgrade LogCollector on a host"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/upgrade_logcollector_on_a_host"
---

LogCollector supports both automatic upgrade and manual upgrade. This topic describes how to upgrade LogCollector using different methods.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Starting from version v2.2.0 of Logcollector, the name of the systemd service has been changed from <strong>filebeatd</strong> to <strong>logcollectord</strong>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

To ensure the stability and high efficiency of log collection, it is recommended that you always use the latest version of LogCollector to collect text logs on Linux servers. Torch Log Service (TLS) provides two upgrade methods: automatic upgrade of LogCollector and manual upgrade of LogCollector.


|Upgrade methods |Description |
|---|---|
|Automatic upgrade |After you enable **Automatic upgrade** when creating a host group, LogCollector will conduct an upgrade check within the specified automatic upgrade time. If the upgrade conditions are met, LogCollector will be automatically upgraded to the latest online version. It is recommended that you set the automatic upgrade time to the off\-peak period of your business.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The automatic upgrade of LogCollector will restart LogCollector, but it won't cause LogCollector to collect logs repeatedly or miss collecting logs.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only LogCollector installed on Linux servers supports automatic upgrade. Self\-built Kubernetes machines, BytePlus VKE and BytePlus VCI don't support automatic upgrades for the time being.</div><br> |
|Manual upgrade |After you disable **Automatic upgrade** or the version of LogCollector installed on the hosts in the host group does not support automatic upgrade, you must manually upgrade LogCollector.<br><br>That is to say, you need to manually download the latest installation script and manually execute the upgrade. |


<span id=".6Ieq5Yqo5Y2H57qnLWxvZ2NvbGxlY3Rvcg=="></span>
## Automatic upgrade

<span id=".6Ieq5Yqo5Y2H57qn5p2h5Lu2"></span>
### Criteria for automatic upgrade

LogCollector will only perform the automatic upgrade operation when all of the following upgrade conditions are met.


|Check Item |Description |
|---|---|
|Whether the current LogCollector version is v 1.0.8 or later. |If the current version of LogCollector does not meet the requirements, please refer to [Manual upgrade](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host#.5omL5Yqo5Y2H57qnLWxvZ2NvbGxlY3Rvcg==). After manually upgrading it to the latest version, you can then use the automatic upgrade function. |


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the project is located.

3. In the left\-side navigation pane, choose **Resource management** \> **Host group**.

4. On the **Host group** **management** page, find the host group for which you want to enable the automatic upgrade feature, then click **Edit** in the **Actions** column.

5. Enable **LogCollector AutoUpgrade**, and set **Upgrade time**.

6. Click **Save**.

   After the automatic upgrade feature is enabled, **Open** is displayed for the host group in the **Automatic upgrade** column.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">We recommend that you specify a time range within the off\-peak hours for performing automatic upgrade. LogCollector may restart during the upgrade process, but this does not lead to log data loss.</div>


* <div data-tips="true" data-tips-type="tip">To enable automatic upgrade for multiple host groups, select multiple host groups in the host group list, click <strong>Automatic upgrade</strong>, then complete the configurations.</div>



<span id=".5omL5Yqo5Y2H57qnLWxvZ2NvbGxlY3Rvcg=="></span>
## Manual upgrade

<span id="3c66d11d"></span>
### 1 Download the LogCollector installation script

Execute the corresponding download commands according to the region and network type of the Linux server, and download the LogCollector installation script to the specified directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to use the private network download address to save the traffic cost of the public network.</div>


<span id="3Zua2s3N"></span>
#### VPC network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.ibytepluses.com/logcollector.sh -O logcollector.sh; sudo chmod 755 logcollector.sh
```


<span id="1cV7aQT4"></span>
#### Public network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/logcollector.sh -O logcollector.sh; sudo chmod 755 logcollector.sh
```


<span id="3f7aa69a"></span>
### Upgrade and start LogCollector

Execute the following commands to manually upgrade LogCollector.

```Bash
sudo ./logcollector.sh upgrade --region {region}
```


Among them, `region` is a required parameter, and the detailed description is as follows.


|Parameter |Required |Example |Description |
|---|---|---|---|
|region |Yes |`ap-southeast-1` |The region where a project is deployed.<br><br>For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
