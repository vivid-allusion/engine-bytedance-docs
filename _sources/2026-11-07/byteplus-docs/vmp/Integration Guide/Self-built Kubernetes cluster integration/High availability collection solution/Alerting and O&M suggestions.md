---
title: "Alerting and O&M suggestions"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Alerting-and-maintenance-suggestions"
---

After you deploy the VM Agent collector, you can configure alerts related to the collector and the corresponding exporter to monitor their running status. This topic describes the common metrics and alert configurations of the VM Agent collector.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information about configuring alerts, see <a href="https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules">Creating alerting rules</a>.</div>


<span id=".5a655Zmo6LWE5rqQ6aWx5ZKM5bqm"></span>
## Container resource saturation

Container resource saturation is primarily used to monitor the CPU usage and the memory usage of the VM Agent collector and the exporter. Alerts are triggered if container resources are insufficient.

Generally, a globally unified policy is adopted for monitoring container resource saturation. No additional configuration is required for monitoring the collection add\-ons.

<span id=".5bu66K6u5ZGK6K2m6YWN572u"></span>
### Recommended alert configurations

<span id=".5a655ZmoIENQVSDnm5Hmjqc="></span>
#### Container CPU monitoring

It is recommended to use the following PromQL statement to configure container CPU monitoring: The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
max(rate(container_cpu_usage_seconds_total[5m])) by (namespace, pod, container)
  / ON(namespace, pod, container)
  kube_pod_container_resource_limits{resource="cpu"}
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P1 |\> 0.8 |1 minute |
|P2 |\> 0.6 |1 minute |


<span id=".5a655Zmo5YaF5a2Y55uR5o6n"></span>
#### Container memory monitoring

It is recommended to use the following PromQL statement to configure container memory monitoring: The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
max(container_memory_working_set_bytes) by (namespace, pod, container)
  / ON(namespace, pod, container)
  kube_pod_container_resource_limits{resource="memory"}
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P1 |\> 0.8 |Trigger immediately |
|P2 |\> 0.6 |Trigger immediately |


<span id=".6L-Q57u05bu66K6u"></span>
### O&M suggestions


* The kube\-state\-metrics agent and the VM Agent collector support sharding. You can increase the number of shards without the need to adjust the quota when resources are insufficient. For more details, refer to [Scaling out agents](https://docs.byteplus.com/en/docs/vmp/Scaling-up-components).

* After an alert is triggered, you can increase the requests and limits of container resources for other agents. It is recommended to increase both requests and limits by 100% during each adjustment.


<span id=".5a655Zmo6L-Q6KGM54q25oCB"></span>
## Container operational status

Container operational status is mainly used to monitor the operational status and memory usage of the VM Agent collector and the exporter. Alerts are triggered when containers are in an abnormal status or the memory is insufficient.

Generally, a globally unified policy is adopted. No additional configuration is required for monitoring the collection add\-ons.

<span id=".5bu66K6u5ZGK6K2m6YWN572u"></span>
### Recommended alert configurations

<span id=".5a655Zmo54q25oCB55uR5o6n"></span>
#### Container status monitoring

It is recommended to use the following PromQL statement to configure container status monitoring. The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
kube_pod_status_phase{phase!~"Running|Succeeded|Pending"}
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P0 |= 1 |5 minutes |
|P1 |= 1 |Trigger immediately |


<span id=".6L-Q57u05bu66K6u"></span>
### O&M suggestions


* The kube\-state\-metrics agent and the VM Agent collector support sharding. You can increase the number of shards without the need to adjust the quota when resources are insufficient. For more details, refer to [Scaling out agents](https://docs.byteplus.com/en/docs/vmp/Scaling-up-components).


<span id=".6IqC54K56LWE5rqQ6aWx5ZKM5bqm"></span>
## Node resource saturation

Node resource saturation is primarily used to monitor the CPU usage and the memory usage of nodes. Even if container resource usage has not reached the quota, insufficient virtual machine resources may still cause resource\-related issues.

<span id=".5bu66K6u5ZGK6K2m6YWN572u"></span>
### Recommended alert configurations

<span id=".6IqC54K5IENQVSDnm5Hmjqc="></span>
#### Node CPU monitoring

It is recommended to use the following PromQL statement to configure node CPU monitoring: The following table shows the relationship between alert thresholds and alert levels.

```Plain Text
node_load5 / ON(node) machine_cpu_cores
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P1 |\> 2 |1 minute |
|P2 |\> 1 |1 minute |


<span id=".6IqC54K55YaF5a2Y55uR5o6n"></span>
#### Node memory monitoring

It is recommended to use the following PromQL statements to configure node memory monitoring: The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P1 |< 0.2 |Trigger immediately |
|P2 |< 0.4 |Trigger immediately |


<span id=".6L-Q57u05bu66K6u"></span>
### O&M suggestions


* Add node resources to the cluster.

* Run the `kubectl delete pod` command to delete pods that can be restarted, forcing the pods to be rescheduled to nodes with more available resources.


<span id=".6YeH6ZuG5Zmo5a-5IFZNUCDlhpnor7fmsYI="></span>
## Write requests from collectors to VMP

The success rate of write requests from the collector to VMP is primarily used to monitor the success rate of data writing to a VMP workspace by the collector. If the collector fails to write data to the VMP workspace, your monitoring data may be lost.

<span id=".5bu66K6u5ZGK6K2m6YWN572u"></span>
### Recommended alert configurations

<span id=".6K-35rGC5aSx6LSl546H"></span>
#### Request failure rate

It is recommended to use the following PromQL statement to configure the failure rate of data write requests for the collector: The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
sum(
  sum(rate(vmagent_remotewrite_errors_total[5m])) without (url) /
  sum(rate(vmagent_remotewrite_requests_total[5m])) without (status_code, url)
) without (instance, pod)
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P0 |\> 0.5 |Trigger immediately |
|P1 |\> 0.1 |Trigger immediately |
|P2 |\> 0 |Trigger immediately |


<span id=".5piv5ZCm5a2Y5Zyo6K-35rGC5oyH5qCH"></span>
#### Whether request metrics exist

We recommend using the following PromQL statement to check whether the collector's request metrics are present. The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
absent(vmagent_remotewrite_requests_total)
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P0 |= 1 |Trigger immediately |


<span id=".6L-Q57u05bu66K6u"></span>
### O&M suggestions


* It is recommended to configure this monitoring item after the collector runs as expected. During the installation phase, first check the connectivity between your environment and VMP and check whether the authentication information is valid.

* If related alerts are triggered during operation, submit a ticket for assistance.


<span id=".6YeH6ZuG55uu5qCH54q25oCB"></span>
## Collection target status

The collection target status is mainly used to monitor whether the connectivity between the collector and the collection target is healthy, and whether the target itself is in a normal status. If the connection between the collector and the collection target is abnormal, or the collection target status is abnormal, the collector will fail to collect valid data.

<span id=".5bu66K6u5ZGK6K2m6YWN572u"></span>
### Recommended alert configurations

<span id=".6K-35rGC5oiQ5Yqf546H"></span>
#### Request success rate

We recommend using the following PromQL statement to monitor the collector's data scrape request status. The following table shows the relationship between alerting thresholds and alert levels.

```Plain Text
vm_promscrape_targets{status="down"}
```



|Alert Level |Trigger Threshold |Duration |
|---|---|---|
|P1 |= 1 |5 minutes |
|P2 |= 1 |Trigger immediately |


<span id=".6L-Q57u05bu66K6u"></span>
### O&M suggestions


* Check the network connectivity between the collector and the monitored service. Focus on the security group configurations and whether the collector and the business nodes can ping each other.

* Check whether the monitored service is healthy and whether the metrics interface is running as expected.
