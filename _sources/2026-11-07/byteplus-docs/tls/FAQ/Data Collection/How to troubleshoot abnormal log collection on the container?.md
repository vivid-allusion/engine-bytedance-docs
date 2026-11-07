---
title: "How to troubleshoot abnormal log collection on the container?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How-to-troubleshoot-abnormal-log-collection-on-the-container"
---

After using LogCollector to collect container logs, if the logs are not successfully collected, you can refer to the steps in this article for troubleshooting.

<span id="118f9c36"></span>
## 1 Check whether the heartbeat of the machine group is normal

Check the heartbeat status of the machine group on the Log Service console. For specific operations, please refer to [View heartbeat statuses of hosts](https://docs.byteplus.com/docs/tls/View_a_host_group#%E6%9F%A5%E7%9C%8B%E5%BF%83%E8%B7%B3%E7%8A%B6%E6%80%81).


* If the number of normal heartbeats of the target machine group is not equal to the number of nodes, please refer to [Host group heartbeat issues on a container](https://docs.byteplus.com/docs/tls/host_group_heartbeat_issues_on_a_container) for troubleshooting.

* If the target machine group has no heartbeat, please reinstall LogCollector. For specific operations, please refer to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet).

* If the heartbeat of the target machine group is normal and the number is also normal, please refer to the next step to continue troubleshooting.


<span id="2834e8e2"></span>
## 2 Check whether the collection configuration is correct

Confirm on the Log Service console that the LogCollector collection configuration has been created and is correct.


* If the collection configuration has not been created, please create the collection configuration first. For specific operations, please refer to [Collect container logs overview](https://docs.byteplus.com/docs/tls/collect_container_logs_overview).

* If the collection configuration has already been created, please check:

   * The file path in the collection configuration is the absolute path inside the container.

   * The soft link path inside the container is not used as the collection path.

   * The container filtering rules in the collection configuration meet your collection requirements.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The label in the general container collection rules is the container\-level label, not the label in the Kubernetes Pod. You can temporarily delete the container filtering rules. If normal logs can be collected at this time, it indicates that the abnormal collection is caused by incorrect configuration of the container filtering rules.      </div>
      

   * The log file matches the collection configuration normally.

      By default, a log file can only match one collection configuration. If the logs in the file need to be collected in multiple copies simultaneously, please refer to [File logs or standard output can be collected multiple times simultaneously](https://docs.byteplus.com/docs/tls/file-repeatedly-collected).

* If there are no problems, please refer to the next step to continue troubleshooting.


<span id="82f8ebd5"></span>
## 3 Check whether the collection configuration has been bound to the machine group

Check whether the collection configuration has been bound to the machine group on the machine group details interface. For specific operations, please refer to [View a host group](https://docs.byteplus.com/docs/tls/View_a_host_group).


* If it has not been bound to the machine group, please refer to please refer to [LogCollector collection rule management](https://docs.byteplus.com/docs/tls/logcollector_collection_rule_management) to complete the configuration.

* If it has already been bound to the machine group, please refer to the next step to continue checking.


<span id="bc3e1c8d"></span>
## 4 Check the container to be collected

Confirm that the container to be collected meets the following conditions:


* Please ensure that the container survives for at least 10 seconds before LogCollector can collect the log.

* LogCollector supports both Docker and Containerd container runtimes, but not other container runtimes.

* If you are using Docker as a container runtime and want to capture container standard output, make sure you have added "log\-driver": "json\-file" to the Docker configuration file daemon.json`"log-driver": "json-file" to the Docker configuration file daemon.json.`


<span id="f0224eb0"></span>
## 5 Check the error message

Check the LogCollector log for error messages. The LogCollector client side logs critical information and all WARNING and ERROR logs. You can view the logs in the installation directory of LogCollector. The log file paths are as follows:


|Logcollector Version |Installation Scenarios |File paths |
|---|---|---|
|Logcollector v2.2.0 and Subsequent Versions |Host Scenario |`/usr/local/logcollector/logs` |
||Container Scenario |`/usr/local/container/logcollector/logs` |
|Versions Prior to Logcollector v2.2.0 |Host Scenario |`/usr/local/filebeat-7.12.0/logs` |
||Container Scenario |`/usr/local/container/filebeat-7.12.0/logs` |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For instructions on how to check the LogCollector version, please refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">2 View software version</a>.</div>


After completing the above inspections, if the problem remains unresolved, please submit a ticket and provide the key information found during the troubleshooting process in the ticket.
