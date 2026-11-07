---
title: "Collect logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/getting_started_collecte_logs"
---

This topic describes how to use the Torch Log Service (TLS) console to collect BytePlus Elastic Compute Service (ECS) logs in single\-line full\-text mode.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Prepare a Linux server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, LogCollector supports Linux x86\-64 (64\-bit) operating systems and does not support ARM architecture and Windows operating systems.   </div>
   

* Install the systemd and wget programs on the Linux server.

* Log in to the Linux server with a user who has root privileges to complete the operations in this topic.

* Determine the network type required for installing LogCollector in advance according to the server type and location.


<span id="57e771bb"></span>
## Step 1: Install LogCollector

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Starting from version v2.2.0 of Logcollector, the name of the systemd service has been changed from <strong>filebeatd</strong> to <strong>logcollectord</strong>.</div>


<span id=".XzEt5a6J6KOFLWxvZ2NvbGxlY3Rvcg=="></span>
### Step1.1: Download the LogCollector installation script

Execute the corresponding download commands according to the region and network type of the Linux server to download the LogCollector installation script to the custom directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use the download URLs in virtual private cloud (VPC) to reduce the costs of internet traffic.</div>



<Tabs>
<Tab zoneid="zuQhkMYa33" title="VPC (Johor)">
<TabTitle>VPC (Johor)</TabTitle>

&nbsp;

```JSON
wget https://logcollector-ap-southeast-1.tos-ap-southeast-1.ibytepluses.com/logcollector.sh -O logcollector.sh; sudo chmod 755 logcollector.sh
```





</Tab>
<Tab zoneid="hPZUSA1FiX" title="Public network (Johor))">
<TabTitle>Public network (Johor))</TabTitle>

&nbsp;

```JSON
wget https://logcollector-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/logcollector.sh -O logcollector.sh; sudo chmod 755 logcollector.sh
```





</Tab>
</Tabs>


<span id="f8beb661"></span>
### Step1.2: Install LogCollector and Initialize LogCollector

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


<span id="0bec75b4"></span>
### Step1.3: Check the running status of LogCollector

Execute the following commands to check the running status of LogCollector. If the `Active` property of the returned result is `active (running)...`, it means that the installation of LogCollector is successful and the running status of LogCollector is normal.

```shell
systemctl status logcollectord.service
```


<span id="41a31f36"></span>
## Step 2: Create a host group


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource Management** \> **Host Group**.

3. On the **Host group management** page, click **Create host group**.

4. Specify the basic information of the host group, then click **Create**.

   
   |Parameter |Description |
   |---|---|
   |Host group name |Specify a name for the host group. |
   |Host group type |Specify the host group type. In this example, **Internet Protocol Address** is selected. |
   |Internet Protocol Address |Specify the IP address of the host.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Type the IP address of the host obtained by LogCollector. For information on how to get the IP address, refer to <a href="https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group">Create an IP address\-based host group</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you add multiple hosts to the host group, separate IP addresses with commas ( , ), spaces, or line breaks.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, Windows hosts are not supported.</div><br> |
   |LogCollector Service log |Specify whether to enable the LogCollector service log feature. After enabled, the LogCollector client records the status and collection progress in real time during the runtime.<br><br>For more information, refer to [Service log fields](https://docs.byteplus.com/docs/tls/service_log_fields). |
   |LogCollector AutoUpgrade |After creating the host group, go to the **LogCollector management** tab on the host group details page to enable this feature. |
   |IAM Project |From the drop\-down list, select the IAM project for the host group.<br><br>If you have not created an IAM project or no suitable IAM project is available, click **Create Project** to create an IAM project. If you do not specify an IAM project, TLS adds the host group to the IAM project named `default`. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you add a host to the host group, the host heartbeat status is <strong>abnormal</strong> until TLS receives the heartbeat status reported by LogCollector. If the <strong>abnormal</strong> status persists for over 1 minute, we recommend that you refer to <a href="https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_host">Host group heartbeat issues on a host</a>.</div>


<span id=".XzMt5Yib5bu66YeH6ZuG6YWN572u"></span>
## Step 3: Create a collection rule

This section explains how to create a collection rule in the console, using the single\-line full\-text mode as an example.

<span id=".XzMtMS3loavlhpnliJ3lp4vphY3nva4="></span>
### Step 3.1: Select a log space


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** page, select a collection mode.

5. Select a project and a topic, and click **Next: Select host group.** 

   The collected log data is stored in the selected topic.


<span id="a9f06b44"></span>
### Step 3.2: Select host groups


1. In the **All host groups** area, select a host group for log collection.

   If there is no host group available in the list, you need to create the host groups first. For specific operations, please refer to [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group), [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group).

2. In the **Selected host group** area, confirm the selection, and click **Next: Collection rule**.


<span id=".XzMtMi3phY3nva7ph4fpm4bop4TliJk="></span>
### Step 3.3: Configure a collection rule


1. Type a **rule name**.

   The **Rule name** is the name of the LogCollector collection rule.

   Alternatively, click **Import other collection configurations**, select a collection rule from a specified project in the current account, then import the existing collection rule. You only need to specify a collection rule name.

2. Select whether to enable **Container log collection**.

   It is disabled by default. Keep the default setting when you collect server logs or collect container logs in sidecar mode.

3. Set **Collection path**.

   **Collection path** specifies the filename and directory where the log data is stored. LogCollector matches directories to listen on log files in the directories that meet the rule. Up to 10 different collection paths can be set.

   You can specify complete directories and filenames, or use wildcards for fuzzy matching.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, a log file can only be collected into one topic and match one collection rule. If a file matches multiple collection rules, the latest collection rule applies.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the wildcard <code>**</code> is specified in log collection paths, multi\-level directory matching applies. In this case, TLS can listen on up to 8\-level directories.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, TLS supports the following wildcards: asterisks <code>*</code> , double asterisks <code>**</code>, and question marks <code>?</code> . You can configure up to one double asterisk <code>**</code> as the wildcard.   </div>
   

   The following table introduces the common methods of configuring collection paths and the corresponding examples:

   
   |Configuration methods |Example |Description |
   |---|---|---|
   |Complete directory and filename |`/var/log/access.log` |Specify a complete directory and filename without wildcards, listening on the specified file in the directory only.<br><br>In this example, TLS listens on the file named `access.log` in the `/var/log` directory. |
   |Filename fuzzy matching |`/var/log/*.log` |If you do not specify a filename, TLS listens on all log files. If you specify a filename rule, TLS only listens on files that meet the rule.<br><br>In this example, TLS listens on `.log` files in the `/var/log` directory. |
   |Path fuzzy matching |`/var/log/**/access.log`<br><br>`/var/log/*/access.log`<br><br>`/var/log/*` |When you use `*` for path fuzzy matching, TLS only listens on log files in the first\-level directory. When you use `**`, TLS listens on log files in the first\-level directory and its subdirectories. In this case, TLS can listen on up to 8\-level directories.<br><br>For example, `/var/log/**/access.log` means TLS listens on files named `access.log` in the `/var/log` directory and its subdirectories, up to 8 levels. |
   

4. Set **Collection path blacklist**.

   After you set a collection path denylist, the specified directories and files are ignored when TLS uses LogCollector to collect logs. After you check the **Enable** check\-box, set directories and files as prompted.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to 10 denylists can be set in each collection rule.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use wildcards in log paths but want to exclude some directories or files, specify the complete path or filename in the denylist. For example, if the collection path is <code>/var/log/project/*.log</code> and you want to exclude all subdirectories in <code>/var/log/project</code>, then set <strong>Collection path blacklist</strong> to <strong>File path</strong> and set the path to <code>/var/log/project/**</code>.   </div>
   

   In a denylist, you can set the path type to **Directory path** or **File path**.

   
   |Parameter |Description |
   |---|---|
   |Directory path |TLS ignores the specified directories during collection. Both exact matching and wildcard matching are supported.<br><br><br>* Exact matching: Specify a complete directory name, such as `/var/log/mydata/new`.<br><br>* Wildcard matching: Use wildcards in a directory. The supported wildcards include the single asterisks `*` and question marks `?`. For example, `/var/log/mydata/n*` means TLS ignores directories starting with n in `/var/log/mydata/` during collection. |
   |File path |TLS ignores the specified files during collection. If you select this path type, you must configure file paths and filenames. Both exact matching and wildcard matching are supported.<br><br><br>* Exact matching: Specify a complete path and filename, such as `/var/log/mydata/access.log`.<br><br>* Wildcard matching: Use wildcards in a path and a filename. The supported wildcards include the following: asterisk `*`, question mark `?` and double asterisk `**`. You can specify up to one double asterisk `**` as a wildcard. For example, `/data/nginx/log/*/*/access.log` means TLS ignores files named `access.log` in the `/data/nginx/log` directory and its first and second\-level subdirectories during collection. |
   

5. Set **Collection policy**.

   The collection policy specifies whether LogCollector collects incremental logs or full logs. By default, incremental logs are collected.

   
   |Parameter |Description |
   |---|---|
   |Full |LogCollector collects logs from the start of each file, collecting historical log data. |
   |increment |LogCollector only collects new content in files. When new logs are written to log files within the monitoring range, it triggers LogCollector to collect logs.<br><br><br>* For the first\-time collection of a log file, LogCollector will automatically determine the collection position based on the incremental threshold you specify.<br><br>   * If the size of the new file does not exceed the specified incremental threshold, LogCollector collects logs from the beginning of the new file.<br><br>   * If the size of the new file exceeds the specified incremental threshold, LogCollector collects logs from a position that is the file's end minus the incremental threshold, thus collecting only the incremental logs.<br><br>* For log files that are not being collected for the first time, LogCollector will determine the collection position based on the Checkpoint and continue collecting from there. |
   

6. Set **Collection mode**.

   The collection mode means the mode in which LogCollector parses log files. This topic uses the **Single\-line** mode as an example.

   In this mode, each log entry ends with `\n` and is encapsulated into the `__content__` field. The raw logs are no longer converted to structured data.

7. Optional: Enable **Plugin configuration**.

   If complex and unstructured business logs cannot be parsed using common log collection modes like JSON, you can use LogCollector plug\-ins to process the collected logs. For more information, refer to [LogCollector plug-ins Overview](https://docs.byteplus.com/docs/tls/plug-ins_Overview).

8. Optional: Enable **Advanced Settings**.

   Configure advanced settings as needed. We recommend that you keep the default settings unless otherwise needed.

   
   |Parameter |Description |
   |---|---|
   |Filter |Specify whether to enable log field filter rules. By default, it is disabled. After enabled, use regular expressions to set filter rules. Only logs that exactly match the regular expressions are collected, helping you collect valuable log data. |
   |Upload parsing failure log |Specify whether to upload logs that failed to be parsed. By default, it is disabled.<br><br><br>* Enable: All logs that failed to be parsed are uploaded to TLS, with a specified field acting as the key and the original log content as the value. The key can be specified using **Failure log key name**. The default key is `LogParseFailed`.<br><br>* Disable: Logs that failed to be parsed are not uploaded to TLS. |
   |Upload hostname field |Specify whether to upload the hostname field. This parameter is disabled by default.<br><br><br>* If you enable the parameter, a field is added to the original log to record the hostname of the log source. Specify the field name for **Hostname** . Default value: `hostname`.<br><br>* If you disable this parameter, the `hostname` field is not added. |
   |Parse collection path |Extract fields from the collection path using regular expressions, then add the fields as metadata to log data. By default, this feature is disabled.<br><br>After enabled, set **Sample collection path**, **Extract regular expression**, and **Extract result**.<br><br><br>* **Sample collection path**: Specify an example of the collection path in actual scenarios.<br><br>   * The example must be an absolute path.<br><br>   * The example cannot include the following wildcards: single asterisk`*`, question mark `?`, and double asterisks `**`.<br><br>* **Extract regular expression**: Specify a regular expression used to extract fields from the path. To successfully extract fields, it must match the collection path example.<br><br>* **Extract result**: It displays each field value parsed and extracted by TLS from the path example based on the regular expression. You must specify a key for each field.<br><br>   * Up to 100 keys can be configured.<br><br>   * Each key must be unique and cannot be empty. |
   |HashKey Routing Shard |Specify a HashKey to write data to a shard that meets the range requirements. By default, this feature is disabled.<br><br><br>* Enable: Use the HashKey Routing Shard mode for data collection. In this mode, data is written to the specified shard in sequence. This is suitable for scenarios requiring sequential data writes and consumption. In this case, you must set the HashKey. Then, TLS writes the data to the shard containing that key value. The HashKey value range is [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff).<br><br>* Disable: Use the load\-balanced mode for data collection. In this mode, data packets are written to an available shard in a load\-balanced manner. This is suitable for scenarios where data consumption and writes are irrelevant to shards, such as scenarios not requiring a sequential order. |
   |Upload original log |Specify whether to upload raw log data as a field to TLS. It is disabled by default.<br><br><br>* Enable: Raw log data is encapsulated in a specified field, and uploaded to TLS together with the parsed log data. The field key can be specified using **Raw log key name**. The default key is `raw`, and the actual corresponding log field is `__raw__`.<br><br>* Disable: No raw log field is added. |
   |Upload constant field |After enabled, LogCollector encapsulates the specified field keys and values in each log entry. The following limits apply to constant fields:<br><br><br>* Up to 5 constant fields can be uploaded.<br><br>* Each field key must be unique and cannot be empty. The key must be 1 to 128 characters in length. It can contain letters, digits, and the following special characters:`-_./`，It cannot start with an underscore ( _ ).<br><br>* Each value cannot be empty, with a maximum length of 512 KiB. |
   |Upload Host Group Label |Whether to upload the label information of the host group to TLS.<br><br><br>* Enable: LogCollector will upload the label information of the host group to the specified field. You can specify the field name in the **Host Group Label Key Name**, the default value is `host_group_label`.<br><br>* Disable: Do not upload the label information of the host group. |
   |Allows multiple file collections |By default, a log file can only match one collection rule and be collected into one topic. After completing this configuration, it enables a log file to match multiple collection rules simultaneously. For more information, please refer to [File logs or standard output can be collected multiple times simultaneously](https://docs.byteplus.com/docs/tls/file-repeatedly-collected). |
   |Extended configuration |Specify the extended configuration of LogCollector in JSON object format. Currently, the supported parameters include CloseInactive, CloseRemoved, CloseRenamed, CloseEOF, and CloseTimeout. For more information on the parameters, refer to [CreateRule](https://docs.byteplus.com/docs/tls/api-createrule).<br><br>For example, the configuration below means that the file handle is released if any of the following occurs:1. No log data is written to the log file for 10 seconds.2. The log file is removed or renamed.3. LogCollector reads to the end of the file.4. The monitoring duration of the log file exceeds 30 minutes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/213bf60ab3ed4bcd9db3ce9a768cd92b~tplv-goo7wpa0wc-image.image) </span> |
   

9. Confirm the collection rule, then click **Next step**.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Before you can preview the collected logs in real time or query and analyze logs in the console, you must configure indexes. For more information, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes).
