---
title: "Troubleshooting LogCollector operations and maintenance failures"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/LogCollector_operation_and_maintenance_failure_troubleshooting"
---

LogCollector version 2.3.1 and later supports creating three types of **manual upgrade/downgrade, configuration modification, and restart** maintenance operations in the console.

After performing the corresponding operations and maintenance tasks, the operation may fail due to certain reasons. You can use this document to troubleshoot and resolve problems.

<span id="46e629f5"></span>
## Troubleshoot manual upgrade and downgrade failures

If a manual upgrade or downgrade operation fails in the console, refer to the following troubleshooting steps. After resolving the issue, you need to recreate the manual upgrade or downgrade task so that any LogCollector instances in the failed task that were not executed or failed to execute can re\-execute the upgrade or downgrade.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS provides a LogCollector installation script that allows you to download the script and execute commands to upgrade or downgrade LogCollector. Please refer to <a href="https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host#.5omL5Yqo5Y2H57qnLWxvZ2NvbGxlY3Rvcg==">Manually upgrade LogCollector</a>.</div>


<span id="bc551e4c"></span>
### Check whether the LogCollector deployment environment is a physical machine


* Only manual upgrade and downgrade of LogCollector deployed on physical machines is supported in the console.

* Manual upgrade or downgrade operations for LogCollector deployed in Kubernetes clusters are not supported in the console. You can upgrade LogCollector using the installation script. Please refer to [Upgrade LogCollector (Kubernetes cluster)](https://arcosite.bytedance.net/sites/1698994260794/654498c0e6cb5902f84fabf2/editor/654498dd688ab004195600df?docLang=zh&bv=654498c2e6cb5902f84fabf8).


<span id="b46e04a3"></span>
### Check whether a network anomaly is causing the operation dispatch to time out


1. Enter the `/usr/local/logcollector/data/ops/` directory.

2. Check if there is an `x.change_version` file.`x`A numeric identifier indicating the file for the x\-th maintenance operation, for example `1.change_version`.

3. If this file is missing, it indicates that a network issue is preventing communication between LogCollector and the service point. Please check the server network.


<span id="a2f2e23c"></span>
### View failure log messages


1. Enter the `/usr/local/filebeat-7.12.0/data/ops/` directory.

2. If the `x.change_version` file exists, you can view the contents of the corresponding `x.change_version.fail` file and troubleshoot according to the instructions in the file.


<span id="6f67e91f"></span>
## Troubleshoot host group restart failure

<span id="0c1b3893"></span>
### Check whether a network abnormality is causing the operation dispatch to time out.


1. Go to the `/usr/local/logcollector/data/ops/` directory.

2. Check if there is an `x.restart` file.`x`A numeric sequence number indicating the file for the x\-th operation and maintenance action, for example, `1.restart`.

3. If this file is missing, it indicates that network issues are preventing communication between LogCollector and the service point. Please check the server network.


<span id="8d6da734"></span>
## Troubleshoot configuration modification failures

<span id="85df71d2"></span>
### Check whether a network abnormality is causing the operation dispatch to time out.


1. Go to the `/usr/local/logcollector/data/ops/` directory.

2. Check whether there is an `x.modify_config` file.`x`A numeric prefix representing the file for the x\-th operation and maintenance task, for example, `1.modify_config`.

3. If this file is missing, it indicates that a network issue is preventing communication between LogCollector and the service point. Please check the server network.


<span id="162051ac"></span>
### View the message content of failed configuration logs


1. Go to the `/usr/local/logcollector/data/ops/` directory.

2. If the `x.yml` file exists, you can view the contents of the corresponding `x.yml.fail` file and troubleshoot according to the prompts in the file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the configuration is modified successfully but an error in the configuration item causes LogCollector to fail to start:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Check the error messages in the <code>/usr/local/logcollector/logs/logcollector-yyyymmdd.log</code> file.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">According to the error message, modify the configuration in <code>x.yml</code>.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After modifying the configuration items again in the console, reissue the maintenance operation.   </div>
