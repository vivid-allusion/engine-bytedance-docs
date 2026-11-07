---
title: "Install LogCollector on a host"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_logCollector_on_a_host"
---

LogCollector is a log collection client developed by Torch Log Service (TLS) team, which is used to quickly report log data. After installing LogCollector in the server, collection rules can be issued and TLS can be quickly accessed through the console or configuration files. This topic introduces operations such as installing or uninstalling LogCollector on Linux servers.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Starting from version v2.2.0 of Logcollector, the name of the systemd service has been changed from <strong>filebeatd</strong> to <strong>logcollectord</strong>.</div>


<span id=".5YeG5aSH5bel5L2c"></span>
## Before you begin


* Prepare a Linux server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, LogCollector supports Linux x86\-64 (64\-bit) operating systems and does not support ARM architecture and Windows operating systems.   </div>
   

* Install the systemd and wget programs on the Linux server.

* Log in to the Linux server with a user who has root privileges to complete the operations in this topic.

* Determine the network type required for installing LogCollector in advance according to the server type and location.


<span id=".5a6J6KOF5bm25ZCv5Yqo"></span>
## Install and start LogCollector

<span id=".XzEt5LiL6L29LWxvZ2NvbGxlY3Rvcg=="></span>
### 1 Download the LogCollector installation script

Execute the corresponding download commands according to the region and network type of the Linux server to download the LogCollector installation script to the custom directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use the download URLs in virtual private cloud (VPC) to reduce the costs of internet traffic.</div>


<span id=".56eB572R5LiL6L295Zyw5Z2A"></span>
#### VPC network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.ibytepluses.com/logcollector.sh -O logcollector.sh; sudo chmod 755 logcollector.sh
```


<span id="d2f90364"></span>
#### Public network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/logcollector.sh -O logcollector.sh; sudo chmod 755 logcollector.sh
```


<span id=".XzIt5a6J6KOFLWxvZ2NvbGxlY3Rvcg=="></span>
### 2 Install LogCollector and Initialize LogCollector

Execute the following commands to install LogCollector. After the installation is completed, the LogCollector process will be started automatically.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If LogCollector has already been installed, a prompt message <strong>do you want to continue the installation? (y/n):</strong> will be output when executing the following commands. If you want to continue the installation by default, add <strong>\-\-continue_installation true</strong> to the command.</div>


* <div data-tips="true" data-tips-type="tip">If LogCollector is running, a prompt message <strong>logcollectord is running, please stop logcollectord first</strong> will be output when executing the following commands. If you want to continue the installation by default, add <strong>\-\-directly_stop true</strong> to the command.</div>



```shell
sudo ./logcollector.sh install --region {region} --endpoint {endpoint} --secret_id {secret_id} --secret_key {secret_key} --label {label} 
```


In the command,`region`, `endpoint`, `secret_id` and `secret_key` are required parameters.


|Parameter |Required |Example |Description |
|---|---|---|---|
|region |Yes |`ap-southeast-1` |The region where a project is deployed.<br><br>For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|endpoint |Yes |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|secret_id |Yes |`AK********` |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |Yes |`TUdZ********` |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|label |Optional (recommended to set) |`http_module` |The label identifier of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add this LogCollector to a host group of the host identification type, you must set the <code>label</code> parameter. Meanwhile, when you create a host group of the host identification type, you need to set the custom identification as this label. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/host_group_overview">Overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To add the host to a host group of the host label type, set a host label. Separate multiple labels with commas ( , ).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot configure <code>ip</code> and <code>label</code> at the same time.</div><br> |
|ip |Optional |`10.1.1.*` |The IP address of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add this LogCollector to a host group of the IP type, it is recommended to set the ip parameter. At this time, the IP address of the LogCollector is the set IP address.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You cannot configure <code>ip</code> and <code>label</code> at the same time. If this parameter is not specified, LogCollector automatically retrieves the host IP address according to a specific policy. You can view the IP address from the <code>ip</code> parameter in the <code>agent_info.json</code>file under the installation path. For more information on the policies of getting an IP address, refer to <a href="https://docs.byteplus.com/docs/tls/configure_an_ip_address_for_a_host_or_container">Configure an IP address for a host or container</a>.</div><br> |


<span id=".XzQt5ZCv5YqoLWxvZ2NvbGxlY3Rvcg=="></span>
### 3 Check the running status of LogCollector

Execute the following commands to check the running status of LogCollector. If the `Active` property of the returned result is `active (running)...`, it means that the installation of LogCollector is successful and the running status of LogCollector is normal.

```shell
systemctl status logcollectord.service
```


<span id=".55u45YWz5pON5L2c"></span>
## Related operations

<span id=".5L-u5pS56Ym05p2D5Y-C5pWw44CB5py65Zmo5qCH6K-G562J6YWN572u"></span>
### 1 Modify the configuration file

During the operation of LogCollector, if it is necessary to modify authentication parameters such as `secret_id` and `secret_key`, or identification parameters of LogCollector like `label`, you can execute the following commands to modify the configuration file of LogCollector.

```YAML
sudo /usr/local/logcollector/tools/logcollector.sh update_config --region {region} --endpoint {endpoint} --secret_id {secret_id} --secret_key {secret_key} --label {label} 
```


Among them, the detailed descriptions of parameters such as `region`, `endpoint`, `secret_id`, and `secret_key` are the same as above.

<span id=".5p-l55yL6L2v5Lu254mI5pys"></span>
### 2 View software version

Run the following command to view the version of LogCollector installed on the current device.

```shell
/usr/local/logcollector/logcollector -v
```


<span id=".6L-b56iL566h55CG"></span>
### 3 Manage processes


|Action |Command |
|---|---|
|View the running status of LogCollector |```Plain```<br>```sudo systemctl status logcollectord.service```<br> |
|Start LogCollector |```Plain```<br>```sudo systemctl start logcollectord.service```<br> |
|Stop LogCollector |```Plain```<br>```sudo systemctl stop logcollectord.service```<br> |
|Restart LogCollector |```Plain```<br>```sudo systemctl restart logcollectord.service```<br> |


<span id=".5Y246L29LWxvZ2NvbGxlY3Rvcg=="></span>
### 4 Uninstall LogCollector

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If LogCollector is running, executing the following command will output a prompt message <strong>logcollectord is running, please stop logcollectord first</strong>. If you wish to proceed with the uninstallation by default, add <strong>\-\-directly_stop true</strong> to the command.</div>


Execute the following command to uninstall LogCollector.

```shell
sudo /usr/local/logcollector/tools/logcollector.sh uninstall
```
