---
title: "File logs or standard output can be collected multiple times simultaneously"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/file-repeatedly-collected"
---

This topic introduces how log files or the standard output of containers can match multiple collection rules simultaneously, resulting in multiple collections.

<span id="c6096547"></span>
## Background information

By default, log files or the standard output of containers can only match one collection rule at a time and be captured accordingly. When multiple collection rules match the same log file or the standard output of the same container at the same time, only the most recently created collection rule takes effect, while the other collection rules are ineffective for that log file or container standard output.

For example, use collection rule 1 and collection rule 2 to collect the following files simultaneously:


* The collection path of collection rule 1 is `/var/logs/a.log` and `/var/logs/b.log`.

* The collection path of collection rule 2 is `/var/logs/b.log` and `/var/logs/c.log`.


Collection rule 1 and collection rule 2 both match log files `/var/logs/b.log`. Assuming collection rule 1 is the most recently created, then LogCollector will collect logs from the `/var/logs/a.log` and `/var/logs/b.log` files according to collection rule 1, and it will collect logs from the `/var/logs/c.log` file only according to collection rule 2.

Starting from version v2.1.0 of LogCollector, LogCollector supports setting additional file identifiers, allowing log files or the standard output of containers to be matched and collected by multiple collection rules simultaneously.

<span id="c31da2ef"></span>
## File Identifier

By default, LogCollector uses the log file ID (including the file inode, device, and checksum of the first N bytes) as the file identifier. Starting from version v2.1.0 of LogCollector, support has been added for adding the following additional file identifiers.


* Collection rule ID (RuleID): Use the collection rule ID as an additional file identifier. That is, LogCollector will use the collection rule ID and log file ID as file identifiers.

* Log topic ID + collection rule name (TopicIDRuleName): Use the log topic ID and collection rule name as additional file identifiers. That is, LogCollector will use the log topic ID, collection rule name, and log file ID as file identifiers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using the collection rule ID, if the collection rule is rebuilt, that is, the old collection rule is deleted first and then an identical new collection rule is created, then due to the change in the collection rule ID, the new collection rule will recollect the matched log files or the standard output of the container.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using the log topic ID and collection rule name, if the collection rule is rebuilt, that is, the old collection rule is deleted first and then an identical new collection rule is created, since neither the log topic ID nor the collection rule name has changed, the new collection rule will not recollect the matched log files or the standard output of the container.   </div>
   


<span id="baedc18b"></span>
## Procedure

Currently, it is supported to set additional file identifiers through the TLS console and the configuration file of LogCollector.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Setting additional file identification configurations in the existing collection rules or in the configuration file of the running LogCollector will cause the LogCollector to collect data repeatedly. Therefore, in such scenarios, it is recommended to enable incremental collection in the collection rules.</div>


* <div data-tips="true" data-tips-type="tip">The file ID set in the LogCollector configuration file is global and most optimal. That is, after setting the file ID in the configuration file, whether you set the file ID in the TLS console or set a different file ID in the TLS console than the LogCollector configuration file, the LogCollector will refer to the file ID in the configuration file.</div>



<span id="75fa86c7"></span>
### LogCollector Configuration File

Log in to the server where LogCollector is located and add the following configuration to the LogCollector configuration file to set additional identification. The file paths are as follows:


* For versions prior to Logcollector v2.2.0: `/usr/local/filebeat-7.12.0/etc/filebeat.yml`

* For Logcollector v2.2.0 and subsequent versions: `/usr/local/logcollector/etc/logcollector.yml`


For instructions on how to check the LogCollector version, please refer to [2 View software version](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC).

```Plain
checkpointer:
  state_multi_collects_type: "Set it as RuleID or TopicIDRuleName" 
```


<span id="41af788a"></span>
### TLS console

In the **Advanced settings** area on the **Collection rule** page, enable the **Allows multiple file collections** switch that allows files to be collected multiple times and configure file identifier.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59c1602aae6e4f07a7f5bc5d088165be~tplv-goo7wpa0wc-image.image) </span>
