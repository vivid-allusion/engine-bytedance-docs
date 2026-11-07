---
title: "Configure the startup parameters of LogCollector"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Configure-the-startup-parameters-of-LogCollector"
---

To prevent LogCollector from consuming excessive server resources and thus affecting the normal operation of other services, Torch Log Service(TLS) has imposed restrictions on the collection performance of LogCollector. When you need to improve the collection performance of LogCollector, you can adjust the CPU threshold and memory threshold allowed for LogCollector to use. This topic describes how to configure the startup parameters of LogCollector.

<span id="2dd224c3"></span>
## Scenarios

You can modify the startup parameters of LogCollector for the following scenarios.


* The number of log files that need to be collected is large (for example, the number of files collected simultaneously exceeds 100), occupying a large amount of memory.

* The traffic of log data is large, resulting in a high CPU usage rate of LogCollector.

* When querying logs, it is found that there is a collection delay.

* Some restrictions of LogCollector do not meet your requirements.


<span id="2fdc46f3"></span>
## Recommended parameter values

Based on practical experience, the following parameter configurations are recommended, which are applicable to the collection scenarios of ordinary JSON files. The performance of the full regular mode and delimiter mode is close to that of the JSON mode, and the performance of the single\-line full\-text and multi\-line full\-text modes is twice that of the JSON mode. Since the complexity of data and the number of collected files will both have an impact on CPU and memory consumption, please refer to the following table and adjust as needed according to the actual situation.


* Host environment

   
   |Parameter |Default collection rate |Collection rate greater than 20MB/s |Collection rate greater than 40MB/s |Collection rate greater than 60MB/s |
   |---|---|---|---|---|
   |max_procs |1 |2 |3 |4 |
   |max_mem |1GiB |2GiB |3GiB |4GiB |
   

* Container environment

   
   |parameters |Default collection rate |Collection rate greater than 20MB/s |Collection rate greater than 40MB/s |Collection rate greater than 60MB/s |
   |---|---|---|---|---|
   |max_procs |1 |2 |3 |4 |
   |max_mem |1GiB |2GiB |3GiB |4GiB |
   |resources.limits.cpu |1000MB |2000MB |3000MB |4000MB |
   |resources.limits.memory |1GiB |2GiB |3GiB |4GiB |
   

   The performance limits of LogCollector are shown in the following table.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since the test environment is different from the production environment, there may be differences in the actual collection performance.   </div>
   

   
   |Collection mode |Performance limit |
   |---|---|
   |Single\-line full\-text mode |300 MB/s |
   |Multi\-line full\-text mode |200 MB/s |
   |JSON schema |150 MB/s |
   |Delimiter pattern |120 MB/s |
   |Full regex\-based single\-line |100 MB/s |
   |Full regex\-based multi\-line |100 MB/s |
   


<span id="0f3b8e2b"></span>
## Set startup parameters


1. Modify the configuration file.

   The file path description is shown in the following table:

   
   |Logcollector version |Installation scenario |File path |
   |---|---|---|
   |Logcollector v2.2.0 and later versions |Host scenario |`/usr/local/logcollector/etc/logcollector.yml` |
   ||Container scenario |Modify the LogCollector configuration file by modifying the configmap.<br><br>```Bash```<br>```kubectl edit configmap -n kube-syetem logcollector-config```<br> |
   |Logcollector v2.2.0 and earlier |Host scenario |`/usr/local/filebeat-7.12.0/etc/filebeat.yml` |
   ||Container scenario |Modify the LogCollector configuration file by modifying the configmap.<br><br>```Bash```<br>```kubectl edit configmap -n kube-syetem logcollector-config```<br> |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">How to check the LogCollector version, please refer to <a href="https://docs.byteplus.com/docs/undefined/66558ab9941ced03077008e9#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">view the software version </a>.   </div>
   

2. Set the startup parameters according to requirements.

   An example of startup parameters is as follows:

   ```YAML
   filebeat:
     deploy_in_container: true
     autodiscover:
       providers:
         - type: kubernetes
           cleanup_timeout: 15s
   
   max_procs: 1
   max_mem: 1GiB
   log_max_bytes: 512KiB
   ...
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following table only lists the common startup parameters you need to pay attention to. For the startup parameters not listed, just keep the default configuration.   </div>
   

   
   |Parameter |Type |Description |Example |
   |---|---|---|---|
   |max_procs |int |The CPU threshold allowed for LogCollector to use.<br><br><br>* Value range: 1 to the number of CPU cores of the current machine.<br><br>* Default value: 1.<br><br><br>`max_procs` is a soft limit, and the actual CPU occupied by LogCollector may exceed the limit value. |`max_procs: 1` |
   |max_mem |string |The memory threshold allowed for LogCollector to use.<br><br><br>* Value range: 256MiB to 8GiB<br><br>* Default value: 1024MiB<br><br><br>`max_mem` is a soft limit, and the actual memory occupied by LogCollector may exceed the limit value. |`max_mem: 1GiB` |
   |log_max_bytes |string |The maximum length of each log read.<br><br><br>* Value range: 16KiB to 8MiB<br><br>* Default value: 512KiB |`log_max_bytes: 512KiB` |
   |autodiscover |autodiscover |Container discovery module. For detailed instructions, please refer to the table below. |```YAML```<br>```autodiscover:```<br>```  providers:```<br>```    - type: kuberbetes```<br>```      cleanup_timeout: 15s```<br> |
   

   * autodiscover

      
      |Parameter |Type |Description |
      |---|---|---|
      |Providers |Array of Object |The specific provider of container discovery. Currently only Kubernetes is supported. For detailed instructions, please refer to the following table. |
      

   * kubernetes

      
      |Parameter |Type |Description |Example |
      |---|---|---|---|
      |cleanup_timeout |string |The time to delay the end of collection after the Pod ends. The default value is 15 seconds. |`cleanup_timeout: 15s` |
      


&nbsp;
