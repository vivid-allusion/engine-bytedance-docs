---
title: "How to troubleshoot abnormal log collection on the host machine?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How-to-troubleshoot-abnormal-log-collection-on-the-host-machine"
---

After using LogCollector to collect logs, if the logs are not successfully collected, you can refer to the steps in this article for troubleshooting.

<span id="d3f17ced"></span>
## 1. Troubleshoot whether the logs are being printed in real time

The LogCollector collection configuration created through the console is incremental collection by default, which means that only the newly generated logs after the configuration takes effect will be collected.


* If the log file has not been updated after the collection configuration is created, LogCollector will not collect this file.

* If the log file has been updated after the creation of the collection configuration, please refer to the next step to continue the inspection.


<span id="b71df940"></span>
## 2 Troubleshoot whether the heartbeat of the machine group is normal

Check the heartbeat status of the machine group on the TLS console. For specific operations, please refer to [View heartbeat statuses of hosts](https://docs.byteplus.com/docs/tls/View_a_host_group#%E6%9F%A5%E7%9C%8B%E5%BF%83%E8%B7%B3%E7%8A%B6%E6%80%81).


* If the heartbeat of the target server is abnormal, please refer to [Host group heartbeat issues on a host](https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_host) for troubleshooting.

* If the heartbeat of the target server is normal, please refer to the next step to continue the inspection.


<span id="db8c4b94"></span>
## 3 Troubleshoot whether the collection configuration is correct

Confirm on the TLS console that the LogCollector collection configuration has been created and is correct.


* If the collection configuration has not been created, please create the collection configuration first. For specific operations, please refer to [Collect logs in Single-line full-text mode](https://docs.byteplus.com/docs/tls/single_line_full_text_mode).

* If the collection configuration has already been created, please confirm that the collection configuration is correct. For example:

   * The collection path in the collection configuration matches the path of the log file in the current server.

   * The log file matches the collection configuration normally.

      By default, a log file can only match one collection configuration. If the logs in the file need to be collected in multiple copies simultaneously, please refer to [File logs or standard output can be collected multiple times simultaneously](https://docs.byteplus.com/docs/tls/file-repeatedly-collected).

* If there are no problems, please refer to the next step to continue the inspection.


<span id="c1624045"></span>
## 4 Troubleshoot whether the collection configuration has been bound to the machine group

Check whether the collection configuration has been bound to the machine group on the machine group details interface. For specific operations, please refer to [View a host group](https://docs.byteplus.com/docs/tls/View_a_host_group).


* If it has not been bound to the machine group, please refer to [LogCollector collection rule management](https://docs.byteplus.com/docs/tls/logcollector_collection_rule_management) to complete the configuration.

* If it has already been bound to the machine group, please refer to the next step to continue the inspection.


<span id="a432b0ba"></span>
## 5. Troubleshoot error messages

Check whether there are error messages in the LogCollector logs. The LogCollector client will record key information as well as all WARNING logs and ERROR logs. You can view the logs in the installation directory of LogCollector. The log file paths are as follows:


|Logcollector Version |Installation Scenarios |File paths |
|---|---|---|
|Logcollector v2.2.0 and Subsequent Versions |Host Scenario |`/usr/local/logcollector/logs` |
||Container Scenario |`/usr/local/container/logcollector/logs` |
|Versions Prior to Logcollector v2.2.0 |Host Scenario |`/usr/local/filebeat-7.12.0/logs` |
||Container Scenario |`/usr/local/container/filebeat-7.12.0/logs` |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For instructions on how to check the LogCollector version, please refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">2 View software version</a>.</div>


After completing the above inspections, if the problem remains unresolved, please submit a ticket and provide the key information found during the troubleshooting process in the ticket.
