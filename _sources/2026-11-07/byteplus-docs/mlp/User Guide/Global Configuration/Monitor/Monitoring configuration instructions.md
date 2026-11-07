---
title: "Monitoring configuration instructions"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Monitoring_configuration_instructions"
---

The Machine Learning Platform provides a monitoring dashboard for commonly used loads and presets a large number of monitoring metrics, but it may still not be able to meet the customization needs of some users. The most common is to aggregate new metrics based on some basic metrics. To solve this problem, the Machine Learning Platform allows users to archive monitoring data to the Managed Service for Prometheus (VMP) under their BytePlus account, allowing users to freely query and use the archived data flexibly.

<span id="使用前提"></span>
# premise of use


1. The current user has `MLPlatformAdminAccess`IAM policies .

2. The current account has \> = 1 VMP workspace.

   * If no work has been created under this account, users with relevant permissions such as `VMPFullAccess`IAM policies may be contacted to go to [the VMP console ](https://console.byteplus.com/prometheus/region:prometheus+cn-beijing/guide)page to create.


<span id="配置监控归档"></span>
# Configure monitoring archive


1. Go to the [global configuration] \- [monitoring] module of the Machine Learning Platform and click [authorization] to enter the configuration page.

2. Enable the ability to monitor the archive and configure the appropriate VMP workspace as the archive location.

3. After submitting the form, the monitoring data of the newly created load will be pushed to the corresponding VMP workspace, allowing users to freely process the data.


<span id="注意事项"></span>
## Precautions


1. The monitoring data of custom tasks and inference services created before opening the archive will not be pushed to VMP, but can be pushed after the development machine is turned off and then turned on.

2. After modifying the archive location, the old custom tasks and inference services will only be pushed to the old archive location, and the development machine can be pushed to the new archive location after being shut down and turned on.


<span id="如何使用归档后数据"></span>
# How to use archived data

After the monitoring data is archived to the user's VMP, various indicators can be fully viewed, and alarms can also be configured on the VMP using this part of the indicators. A detailed list of metrics and labels is detailed in the **metrics and label description** below.

<span id="vmp-explore-指标检索"></span>
## VMP Explore Index Search


1. Go to the Explore module of the VMP and select the workspace to use as the monitoring data archive.

2. Enter a metric name or a PromQL query statement in the query box.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since December 2024, the platform supports users to view monitoring by task/Dev box name and task label aggregation. See <strong>workload metrics</strong> below for new metrics and label descriptions.</div>



3. You can also do fine graining with labels and values.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6ed792e0d654afcb4046f37315e49b0~tplv-goo7wpa0wc-image.image) </span>

<span id="自建-grafana-监控看板"></span>
## Build your own Grafana monitoring dashboard

Grafana is a cross\-platform open\-source measurement analysis and visualization tool that allows users to query and visualize their data. For specific operation steps, please refer to [How to Build a Visualization Dashboard for Monitoring Metrics Using Grafana_Taking GPU Resource Total Dashboard as an Example](https://docs.byteplus.com/docs/mlp/40174). You can deploy Grafana through the images BytePlus provides you, or you can deploy it using open\-source images. The way to deploy Grafana is as follows:


* Method 1: Deploy Grafana in BytePlus Container Service VKE.

* Method 2: Deploy Grafana in BytePlus Cloud as a Service ECS.

   * Go to ECS to create an instance and install Grafana in the instance.

   * Bind the public IP for ECS and set the SecurityGroup rule: In the Inbound rule, allow the Grafana port (default 3000).

   * In the browser to access `http://< public IP >: < "Grafana port" >`, the initial username and password are `admin`.

   * Add a new data source in the Grafana settings, select Prometheus, and fill in the VMP's Basic Auth and Query URLs (the above information can be obtained from the VMP workspace details page).


<span id="通过-vmp-配置告警"></span>
## Configure alarms via VMP

Since all monitoring data has been pushed to the user's VMP, users can flexibly configure alarm rules by writing PromQL query statements, and send alarm messages to the corresponding alarm contact group in a timely manner when the monitoring metrics of the workload of the Machine Learning Platform appear abnormal.

<span id="promql检索示例"></span>
## PromQL Search Example

MLP provides multiple preset Kanban in VMP. For detailed introduction of preset Kanban variables and PromQL query statements, please refer to the [Preset Kanban Introduction of MLP in VMP](https://docs.byteplus.com/docs/mlp/Preset_Kanban_Introduction_of_MLP_in_VMP). Here are some examples of searching for common metrics.


* CPU usage.


```plain
irate(container_cpu_usage_seconds_total{name!=""}[5m])
```



* CPU usage.


```plain
irate(container\_cpu\_usage\_seconds\_total{name!=""}\[5m\])/on (pod,name) (container\_spec\_cpu\_quota/1000/100) * 100
```



* Memory utilization.


```plain
avg by(gpu, pod)(DCGM_FI_DEV_FB_USED{pod="%s"} / (DCGM_FI_DEV_FB_FREE{pod="%s"} + DCGM_FI_DEV_FB_USED{pod="%s"}) * 100)
```



* Check the average GPU utilization for each custom task (since a custom task will have multiple pods, it needs to be aggregated by task id).


```plain
avg (DCGM_FI_DEV_GPU_UTIL * ON(pod) group_left(mlp_customtask) mlp_customtask_instance_info) by (mlp_customtask)
```



* Achieve the average utilization of custom tasks for a queue (q\-20211224114108\-78qvl) within 10 days (average utilization over the lifetime of each task).


```plain
avg_over_time(
    (avg (
        DCGM_FI_DEV_GPU_UTIL * ON(pod) group_left(mlp_customtask) mlp_customtask_instance_info{mlp_resource_queue="q-20211224114108-78qvl"}) by (mlp_customtask)) 
[10d:30s])
```



* GPU usage in 10 days for a task (t\-20230519123538\-vr2nl).

   * The number of GPUs used by this task monitors how many data curves are displayed in the chart.


```plain
count_over_time(DCGM_FI_DEV_GPU_UTIL AND ON(pod) mlp_customtask_instance_info{mlp_customtask="t-20230519123538-vr2nl"} [10d:1m])
```



* According to the dimension of the task, the total card time used for each GPU model in the past 5 days is counted.

   * Query statement parsing:

      * `count_over_time ()`: Calculates the number of samples within the specified time frame. In this example, it is used to calculate the number of samples per minute for the past 1 day.

      * `DCGM_FI_DEV_GPU_UTIL`: The `DCGM_FI_DEV_GPU_UTIL`metric is selected in this example to calculate usage time

      * `* ON (pod) group_left (mlp_customtask) mlp_customtask_instance_info`: To filter custom tasks in this example, you need to match the DCGM indicator and the custom tasks instance indicator according to the same pod. Since a single pod may have multiple cards, many\-to\-one matching is required using group_left operations and custom tasks ID `mlp_customtask`passed to the final result. For detailed matching rules, please refer to the official PromQL documentation.

      * `Sum by (mlp_customtask, modelName)`: For data points with the same `mlp_customtask`and `modelName`tag values, add their count values to get a total.

         * Where `modelName`is the label that comes with DCGM, referring to the GPU model.


```plain
sum by (mlp_customtask, modelName) (count_over_time((DCGM_FI_DEV_GPU_UTIL * ON(pod) group_left(mlp_customtask) mlp_customtask_instance_info)[5d:1m]))
```


<span id="指标及其说明"></span>
# Indicators and their descriptions

<span id="rdma整机监控指标"></span>
## RDMA machine monitoring indicators

<span id="指标描述"></span>
### indicator description


|Metric |Value Type |unit |Description |
|---|---|---|---|
|mlp_node_exporter_infiniband_link_downed_total |Counter |time |The number of times a link failed to recover from an error state and stopped functioning. |
|mlp_node_exporter_infiniband_link_error_recovery_total |Counter |time |The number of times the link successfully recovered from an error state. |
|mlp_node_exporter_infiniband_physical_state_id |Gauge |*  |The physical state of the port (0: no change, 1: sleep, 2: polling, 3: disabled, 4: shift, 5: link up, 6: link error recovered, 7: phytest). |
|mlp_node_exporter_infiniband_state_id |Gauge |*  |Port status (0: no change, 1: down, 2: init, 3: armed, 4: active, 5: act deferred). |
|mlp_node_exporter_infiniband_excessive_buffer_overrun_errors_total |Counter |time |Number of consecutive overflow errors during flow control updates. |
|mlp_node_exporter_infiniband_local_link_integrity_errors_total |Counter |time |The number of times the local physical error count exceeds the threshold specified by LocalPhyErrors. |
|mlp_node_exporter_infiniband_port_constraint_errors_received_total |Counter |a |The number of data packets received on the switch physical port is discarded. |
|mlp_node_exporter_infiniband_port_constraint_errors_transmitted_total |Counter |a |The number of data packets not transferred from the switch physical port. |
|mlp_node_exporter_infiniband_port_errors_received_total |Counter |a |The number of erroneous data packets received on this port. |
|mlp_node_exporter_infiniband_port_receive_remote_physical_errors_total |Counter |a |The number of data packets received at this port marked with the end of bad packet delimiter (EBP). |
|mlp_node_exporter_infiniband_port_receive_switch_relay_errors_total |Counter |a |Switch The number of data packets that cannot be forwarded. |
|mlp_node_exporter_infiniband_symbol_error_total |Counter |a |The number of minor link errors detected on one or more physical channels. |
|mlp_rdma_exporter_infiniband_implied_nak_seq_err_total |Counter |time |Read response out of order times. |
|mlp_rdma_exporter_infiniband_local_ack_timeout_err_total |Counter |time |Number of timeouts in the exit direction. |
|mlp_rdma_exporter_infiniband_np_cnp_sent_total |Counter |a |The number of CNP packets sent by the network interface card during the outgoing acquisition period. It means that there is congestion on the path of the receiving end, and the sending end needs to be notified to reduce sending. |
|mlp_rdma_exporter_infiniband_np_ecn_marked_roce_packets_total |Counter |a |The number of ECN marked packets received by the network interface card during the incoming acquisition period. Represents congestion on the path. |
|mlp_rdma_exporter_infiniband_out_of_sequence_total |Counter |time |The number of times the direction is out of order. The increase in this indicator may be due to a link problem. |
|mlp_rdma_exporter_infiniband_packet_seq_err_total |Counter |time |The number of times the direction is out of order. |
|mlp_rdma_exporter_infiniband_port_data_received_bytes_total |Counter |bytes |Drives inbound traffic, including TCP/IP and RDMA. |
|mlp_rdma_exporter_infiniband_port_data_transmitted_bytes_total |Counter |bytes |Drive layer outgoing traffic, including TCP/IP and RDMA. |
|mlp_rdma_exporter_infiniband_port_packets_received_total |Counter |packets |The number of incoming packets at the driver level, including TCP/IP and RDMA. |
|mlp_rdma_exporter_infiniband_port_packets_transmitted_total |Counter |packets |The number of outgoing packets at the driver level, including TCP/IP and RDMA. |
|mlp_rdma_exporter_infiniband_rdma_data_received_bytes_total |Counter |bytes |RDMA incoming direction flow. |
|mlp_rdma_exporter_infiniband_rdma_data_transmitted_bytes_total |Counter |bytes |RDMA outlet direction flow. |
|mlp_rdma_exporter_infiniband_rdma_packets_received_total |Counter |packets |Number of incoming RDMA packets. |
|mlp_rdma_exporter_infiniband_rdma_packets_transmitted_total |Counter |packets |Number of RDMA outgoing packets. |
|mlp_rdma_exporter_infiniband_rp_cnp_handled_total |Counter |a |The number of CNP packets processed by the network interface card during the incoming acquisition period. The transmission frequency needs to be reduced. |
|mlp_rdma_exporter_infiniband_rp_cnp_ignored_total |Counter |a |The number of CNP packets ignored by the network interface card during the incoming acquisition period. This indicator should not increase. If the growth to see whether the network interface card congestion control configuration is normal, whether to enable ECN/CNP. |
|mlp_rdma_exporter_infiniband_rx_pause_duration_seconds |Counter |s |Incoming direction pause duration. This indicator generally points to network congestion, which represents the PFC packet received by the network interface card as the sender, which means that the receiver is severely congested and the receiver requires the network interface card to stop sending. |
|mlp_rdma_exporter_infiniband_tx_pause_duration_seconds |Counter |s |Outgoing direction pause duration. This indicator generally points to the host abnormality, the network interface card sends a PFC packet, which means that the network interface card is seriously congested as the receiving end, and the network interface card requires the sending end to stop sending. |
|mlp_rdma_exporter_infiniband_rx_pause_total |Counter |a |The number of PFC pause messages received in the incoming direction. |
|mlp_rdma_exporter_infiniband_tx_pause_total |Counter |a |The number of PFC pause messages sent in the outgoing direction. |
|mlp_node_exporter_infiniband_max_link_speed |Gauge |GT/s |RDMA network interface card PCIE maximum rate |
|mlp_node_exporter_infiniband_max_link_width |Gauge |a |RDMA network interface card PCIE maximum bandwidth |
|mlp_node_exporter_infiniband_current_link_speed |Gauge |GT/s |RDMA network interface card PCIE current rate |
|mlp_node_exporter_infiniband_current_link_width |Gauge |a |RDMA network interface card PCIE current bandwidth |
|mlp_node_exporter_nvidia_max_link_speed |Gauge |GT/s |Nvidida GPU PCIE maximum rate |
|mlp_node_exporter_nvidia_max_link_width |Gauge |a |Maximum bandwidth of Nvidida GPU PCIE |
|mlp_node_exporter_nvidia_current_link_speed |Gauge |GT/s |Nvidida GPU PCIE current rate |
|mlp_node_exporter_nvidia_current_link_width |Gauge |a |Nvidida GPU PCIE's current bandwidth |
|mlp_node_exporter_infiniband_rate_bytes_per_second |Gauge |bytes/s |RDMA network interface card maximum rate |


<span id="标签描述"></span>
### label description

<span id="公共标签"></span>
#### public label


|label signature |Sample Value |Description |
|---|---|---|
|device |mlx5_0 |RDMA device name |
|pod |t\-20240101120000\-abcde\-worker\-0 |Pod ID using RDMA |
|namespace |mlplatform\-customtask |The namespace name to which it belongs |


<span id="dcgm常见指标"></span>
## DCGM common indicators

<span id="指标描述"></span>
### indicator description


|Metric |Value Type |unit |Description |
|---|---|---|---|
|DCGM_FI_DEV_SM_CLOCK |Gauge |MHz |SM clock frequency |
|DCGM_FI_DEV_MEM_CLOCK |Gauge |MHz |SMS Memory Clock Frequency |
|DCGM_FI_DEV_POWER_USAGE |Gauge |W |power |
|DCGM_FI_DEV_TOTAL_ENERGY_CONSUMPTION |Counter |mJ |Energy consumption |
|DCGM_FI_DEV_PCIE_REPLAY_COUNTER |Counter |time |PCIe replay count |
|DCGM_FI_DEV_GPU_UTIL |Gauge |% (1\-100) |Percentage of time per unit time when at least one kernel function is active |
|DCGM_FI_DEV_MEM_COPY_UTIL |Gauge |% (1\-100) |Memory bandwidth utilization |
|DCGM_FI_DEV_ENC_UTIL |Gauge |% (1\-100) |encoder utilization |
|DCGM_FI_DEV_DEC_UTIL |Gauge |% (1\-100) |decoder utilization |
|DCGM_FI_DEV_XID_ERRORS |Gauge |*  |The error code of the last XID error that occurred |
|DCGM_FI_DEV_POWER_VIOLATION |Counter |μs |Cumulative duration of violations due to power caps |
|DCGM_FI_DEV_THERMAL_VIOLATION |Counter |μs |Cumulative duration of violations due to heat restrictions |
|DCGM_FI_DEV_SYNC_BOOST_VIOLATION |Counter |μs |Cumulative duration of violations due to synchronous lift restrictions |
|DCGM_FI_DEV_BOARD_LIMIT_VIOLATION |Counter |μs |Cumulative duration of violations due to board restrictions |
|DCGM_FI_DEV_LOW_UTIL_VIOLATION |Counter |μs |Cumulative duration of violations due to low utilization restrictions |
|DCGM_FI_DEV_RELIABILITY_VIOLATION |Counter |μs |Cumulative duration of violations due to board reliability limitations |
|DCGM_FI_DEV_FB_FREE |Gauge |MB |Unused BAR1 |
|DCGM_FI_DEV_FB_USED |Gauge |MB |Used BAR1 |
|DCGM_FI_DEV_RETIRED_SBE |Counter |a |Deactivated pages due to single bit error |
|DCGM_FI_DEV_RETIRED_DBE |Counter |a |A page disabled due to a two\-bit error |
|DCGM_FI_PROF_GR_ENGINE_ACTIVE |Gauge |Percentage (0\-1) |The percentage of time that a Graphics or Compute engine is Active over a period of time |
|DCGM_FI_PROF_SM_ACTIVE |Gauge |Percentage (0\-1) |The proportion of time that at least one thread bundle is active on a SM during a time interval. This is the average of all SM's. |
|DCGM_FI_PROF_SM_OCCUPANCY |Gauge |Percentage (0\-1) |The ratio of thread bundles residing on a SM to the maximum residing thread bundle for that SM over a time interval. This is the average of all SM's. |
|DCGM_FI_PROF_PIPE_TENSOR_ACTIVE |Gauge |Percentage (0\-1) |Period Fraction of Average Active Tensor Pipes per Unit Time |
|DCGM_FI_PROF_DRAM_ACTIVE |Gauge |Percentage (0\-1) |Memory copy active cycle fraction (100% if there is one DRAM instruction in a cycle) |
|DCGM_FI_PROF_PIPE_FP64_ACTIVE |Gauge |Percentage (0\-1) |Period Fraction of Average Active F64 Pipes per Unit Time |
|DCGM_FI_PROF_PIPE_FP32_ACTIVE |Gauge |Percentage (0\-1) |Period Fraction of Average Active F32 Pipes per Unit Time |
|DCGM_FI_PROF_PIPE_FP16_ACTIVE |Gauge |Percentage (0\-1) |Period Fraction of Average Active F16 Pipes per Unit Time |
|DCGM_FI_PROF_PCIE_TX_BYTES |Counter |B/s |Data traffic transmitted over the PCIe bus |
|DCGM_FI_PROF_PCIE_RX_BYTES |Counter |B/s |Data traffic received via the PCIe bus |
|DCGM_FI_PROF_NVLINK_RX_BYTES |Counter |B/s |Data traffic transmitted via NVLink |
|DCGM_FI_PROF_NVLINK_TX_BYTES |Counter |B/s |Data traffic received through NVLink |


<span id="标签描述"></span>
### label description

<span id="公共标签"></span>
#### public label


|label signature |Sample Value |Description |
|---|---|---|
|Hostname |dcgm\-exporter\-abcde |Indicator source dcgm\-exporter instance name |
|UUID |GPU\-000000000\-0000\-0000\-0000\-000000000000 |GPU UUID identifier |
|container |mljob |Container name using the GPU |
|device |nvidia1 |GPU device name |
|gpu |1 |GPU number |
|instance |t\-20240101120000\-abcde\-worker\-0 |Instance ID using GPU |
|modelName |NVIDIA A10 |GPU model |
|namespace |mlplatform\-customtask |The namespace Kubernetes instance |


<span id="cadvisor常见指标"></span>
## cAdvisor Common Metrics

<span id="指标描述"></span>
### indicator description


|classification |Metric |Value Type |unit |Indicator meaning |
|---|---|---|---|---|
|CPU |container_cpu_load_average_10s |gauge |*  |The average load of container CPUs in the past 10 seconds |
||container_cpu_usage_seconds_total |counter |s |Container CPU cumulative usage |
||container_cpu_system_seconds_total |counter |s |System CPU cumulative usage time |
||container_cpu_user_seconds_total |counter |s |User CPU cumulative usage time |
|Memory |container_memory_max_usage_bytes |gauge |Byte |The maximum memory usage of the container |
||container_memory_usage_bytes |gauge |Byte |The current memory usage of the container, including freeable memory such as the cache |
||container_memory_working_set_bytes |gauge |Byte |The current memory usage of the container |
||container_spec_memory_limit_bytes |gauge |Byte |Memory usage limit for containers |
||machine_memory_bytes |gauge |Byte |Total memory of the current host |


<span id="标签描述"></span>
### label description

<span id="公共标签"></span>
#### public label


|label signature |Sample Value |Description |
|---|---|---|
|id |/kubepods/burstable/pod\-id/container\-name |Global ID ID of the container |
|image |python:3.10 |The name and version label of the container image |
|name |container\-name |container name |
|namespace |mlplatform\-service |Owned namespace name |
|pod |s\-20240101120000\-abcde\-abcde |Pod id to which the container belongs |
|job |kubernetes\-cadvisor |Fixed collection source name |


<span id="资源组指标"></span>
## Resource group metrics

<span id="指标描述"></span>
### indicator description


|Metric |Value Type |unit |Description |
|---|---|---|---|
|mlp_resourcegroup_info |Gauge |*  |The metadata of ResourceGroup, the value is always 1. |
|mlp_resourcegroup_created_timestamp_seconds |Gauge |s |Creation time (UNIX timestamp) |
|mlp_resourcegroup_resource_capacity |Gauge |*  |The ResourceCapability field of the ResourceGroup resource, which takes the value of the specific resource and is converted to the unit that won the bidding bet |
|mlp_resourcegroup_flavor_capacity |Gauge |a |The FlavorCapability field of the ResourceGroup resource, which describes the maximum number of instances for each specification of the resource group |
|mlp_resourcegroup_flavor_allocated |Gauge |a |The FlavorAllocated field of the ResourceGroup resource, which describes the number of assigned instances for each specification of the resource group |
|mlp_resourcegroup_volume_capacity |Gauge |GiB |The VolumeCapability field of the ResourceGroup resource describes the upper limit of cloud disk capacity for each specification of the resource group |
|mlp_resourcegroup_volume_allocated |Gauge |GiB |The VolumeAllocated field of the ResourceGroup resource describes the allocated cloud disk capacity for each specification of the resource group |
|mlp_resourcegroup_expired_timestamp_seconds |Gauge |s |The ExpiredTime field of the ResourceGroup resource, which is converted to a Unix timestamp. |
|mlp_resourcegroup_state |Gauge |*  |The State field of the ResourceGroup resource, the value logic is, if the current state is the corresponding value of the state label, take 1, otherwise take 0 |


<span id="标签描述"></span>
### label description

<span id="公共标签"></span>
#### public label


|label signature |Sample Value |Label meaning |
|---|---|---|
|mlp_resource_group |r\-20240101120000\-abcde |Resource group id |


<span id="专有标签"></span>
#### proprietary label


|Metric |label signature |Sample Value |Label meaning |
|---|---|---|---|
|mlp_resourcegroup_info |charge_type |PrePaid |Resource group billing method |
|mlp_resourcegroup_resource_capacity |resource |GPU |Resource type, optional values: VCPU, Memory, RDMA_ENI, GPU_Memory, GPU |
||gpu_type |NVIDIA A10 |Specific GPU model (null value for non\-GPU resources) |
||unit |core |Units of measurement, optional values: core, GiB, count |
|mlp_resourcegroup_flavor_capacity |flavor |ml.g1ie.large |instance specification |
||availability_zone |cn\-beijing\-a |Availability Zone |
|mlp_resourcegroup_flavor_allocated |flavor |ml.g1ie.large |instance specification |
||availability_zone |cn\-beijing\-a |Availability Zone |
|mlp_resourcegroup_volume_capacity |flavor |ml.essd.pl1 |Cloud disk specifications |
||availability_zone |cn\-beijing\-a |Availability Zone |
|mlp_resourcegroup_volume_allocated |flavor |ml.essd.pl1 |Cloud disk specifications |
||availability_zone |cn\-beijing\-a |Availability Zone |
|mlp_resourcegroup_state |state |Running |Enumeration value for the resource group State field |


<span id="队列指标"></span>
## cohort metrics

<span id="指标描述"></span>
### indicator description


|Metric |Value Type |unit |Description |
|---|---|---|---|
|mlp_resourcequeue_info |Gauge |*  |The metadata for the queue. The value is always 1. |
|mlp_resourcequeue_created_timestamp_seconds |Gauge |s |Creation time (UNIX timestamp) |
|mlp_resourcequeue_quota_capacity |Gauge |*  |The QuotaCapability field of the ResourceQueue resource, which takes the value of the specific resource and is converted to the unit that won the bidding bet |
|mlp_resourcequeue_quota_allocated |Gauge |*  |The QuotaAllocated field of the ResourceQueue resource, which takes the value of the specific resource and is converted to the unit that won the bidding bet |
|mlp_resourcequeue_flavor_resources |Gauge |a |The FlavorResources field of the ResourceQueue resource, describing the number of instances of each specification of the queue |
|mlp_resourcequeue_volume_capacity |Gauge |GiB |The VolumeCapability field of the ResourceQueue resource describes the upper limit of the cloud disk capacity of each specification of the queue |
|mlp_resourcequeue_volume_allocated |Gauge |GiB |The VolumeAllocated field of the ResourceQueue resource describes the allocated cloud disk capacity for each specification of the queue |
|mlp_resourcequeue_state |Gauge |*  |The State field of the ResourceQueue resource, the value logic is, if the current state is the corresponding value of the state label, take 1, otherwise take 0 |


<span id="标签描述"></span>
### label description

<span id="公共标签"></span>
#### public label


|label signature |Sample Value |Label meaning |
|---|---|---|
|mlp_resource_queue |q\-20240101120000\-abcde |queue id |


<span id="专有标签"></span>
#### proprietary label


|Metric |label signature |Sample Value |Label meaning |
|---|---|---|---|
|mlp_resourcequeue_info |mlp_resource_group |r\-20240101120000\-abcde |The ID of the resource group to which the queue belongs |
||availability_zone |cn\-beijing\-a |Availability Zone |
||charge_type |PrePaid |Resource group billing method |
|mlp_resourcequeue_quota_capacity |resource |GPU |Resource type, optional values: VCPU, Memory, RDMA_ENI, GPU_Memory, GPU |
||gpu_type |NVIDIA A10 |Specific GPU model (null value for non\-GPU resources) |
||unit |core |Units of measurement, optional values: core, GiB, count |
|mlp_resourcequeue_quota_allocated |resource |GPU |Resource type, optional values: VCPU, Memory, RDMA_ENI, GPU_Memory, GPU |
||gpu_type |NVIDIA A10 |Specific GPU model (null value for non\-GPU resources) |
||unit |core |Units of measurement, optional values: core, GiB, count |
|mlp_resourcequeue_flavor_resources |flavor |ml.g1ie.large |instance specification |
|mlp_resourcequeue_volume_capacity |flavor |ml.essd.pl1 |Cloud disk specifications |
|mlp_resourcequeue_volume_allocated |flavor |ml.essd.pl1 |Cloud disk specifications |
|mlp_resourcequeue_state |state |Running |Enumeration value for the Queue State field |


<span id="工作负载指标"></span>
## workload metrics

<span id="指标描述"></span>
### indicator description


|classification |Metric |Value Type |unit |Indicator meaning |
|---|---|---|---|---|
|custom tasks |mlp_customtask_info |Gauge |*  |Custom tasks metadata. The value is always 1. |
||mlp_customtask_instance_info |Gauge |*  |Custom tasks instance metadata. The value is always 1. |
||mlp_customtask_alias |Gauge |*  |Custom tasks names. |
||mlp_customtask_tag |Gauge |*  |Custom tasks tag. |
|inference services |mlp_service_info |Gauge |*  |Inference services metadata. The value is always 1. |
||mlp_deployment_info |Gauge |*  |Inference services deployment metadata. The value is always 1. |
||mlp_deployment_instance_info |Gauge |*  |Inference services instance metadata. The value is always 1. |
|Dev boxes |mlp_devinstance_info |Gauge |*  |Dev boxes metadata. The value is always 1. |
||mlp_devinstance_alias |Gauge |*  |Dev boxes name |
|example |mlp_instance_pod_status_phase |Gauge |*  |Kubernetes Pod Phase state of the load instance |
||mlp_instance_pod_status_ready |Gauge |*  |Kubernetes Pod Ready Status of Load Instances |
||mlp_instance_created_timestamp_seconds |Gauge |s |Instance creation time (UNIX timestamp) |
||mlp_instance_resource_requests |Gauge |*  |Logical resources occupied by the instance |


<span id="标签描述"></span>
### label description


|classification |Metric |label signature |Label meaning |
|---|---|---|---|
|custom tasks |mlp_customtask_info |mlp_customtask |Resource ID |
|||mlp_pipeline |Owned pipeline ID |
|||mlp_resource_group |Task Owned Resource Group ID |
|||mlp_resource_queue |task owning queue ID |
||mlp_customtask_instance_info |mlp_customtask |Task ID to which the instance belongs |
|||namespace |K8 namespace |
|||pod |K8 Pod corresponding to the instance |
|||role |instance role |
|||role_index |Instance number (by role) |
|||flavor |Example specifications, such as ml.g1ie.large |
|||mlp_pipeline |Owned pipeline ID |
|||mlp_resource_group |Task Owned Resource Group ID |
|||mlp_resource_queue |task owning queue ID |
|||availability_zone |Availability Zone |
||mlp_customtask_alias |mlp_customtask |Resource ID |
|||alias |resource name |
||mlp_customtask_tag |mlp_customtask |Resource ID |
|||tag |resource tag |
|inference services |mlp_service_info |mlp_service |Resource ID |
|||type |Service type, uppercase hump format, such as General or Credible |
||mlp_deployment_info |mlp_deployment |Resource ID |
|||mlp_service |The ID of the service to which the deployment belongs |
|||type |Deployment type, uppercase hump format, such as Stable, Canary, and Debug |
|||mlp_resource_group |Resource group ID |
|||mlp_resource_queue |queue ID |
|||availability_zone |Availability Zone |
||mlp_deployment_instance_info |mlp_deployment |The ID of the deployment to which the instance belongs |
|||mlp_service |The ID of the service to which the instance belongs |
|||mlp_service_instance |Instance ID |
|||role |instance role |
|||role_index |Instance number (by role) |
|||namespace |K8 namespace |
|||pod |K8 Pod corresponding to the instance |
|||flavor |Example specifications, such as ml.g1ie.large |
|||mlp_resource_group |Resource group ID |
|||mlp_resource_queue |queue ID |
|||availability_zone |Availability Zone |
|Dev boxes |mlp_devinstance_info |mlp_devinstance |Dev boxes ID |
|||namespace |K8 namespace |
|||pod |K8 Pod corresponding to the instance |
|||flavor |Example specifications, such as ml.g1ie.large |
|||mlp_resource_group |Resource group ID |
|||mlp_resource_queue |queue ID |
|||availability_zone |Availability Zone |
||mlp_devinstance_alias |mlp_devinstance |Resource ID |
|||alias |resource name |
|example |mlp_instance_pod_status_phase |pod |Pod Name |
|||phase |The enumeration value of the Pod phase, including Failed, Pending, Running, Succeeded, Unknown, the indicator value of the current phase is 1, and the other phase is 0. |
||mlp_instance_pod_status_ready |pod |Pod Name |
|||ready |The enumeration value of the Ready condition, including True/False/Unknown, the current ready state of the pod is 1, and the other is 0. |
||mlp_instance_created_timestamp_seconds |pod |Pod Name |
||mlp_instance_resource_requests |pod |Pod Name |
|||resource |Optional values: VCPU, Memory, GPU |
|||gpu_type |Specific GPU model (null value for non\-GPU resources) |
|||unit |Units of measurement, optional values: core, GiB, count |
||mlp_instance_info |pod |Pod Name |
|||mlp_resource_queue |instance owning queue ID |
|||mlp_resource_group |Resource group ID to which the instance belongs |
|inference services |mlp_deployment_info |mlp_deployment |Resource ID |
|||mlp_service |The ID of the service to which the deployment belongs |
|||type |Deployment type, uppercase hump format, such as Stable, Canary, and Debug |
|||mlp_resource_group |Resource group ID |
|||mlp_resource_queue |queue ID |
|||availability_zone |Availability Zone |
||mlp_deployment_instance_info |mlp_role_name |role name |
