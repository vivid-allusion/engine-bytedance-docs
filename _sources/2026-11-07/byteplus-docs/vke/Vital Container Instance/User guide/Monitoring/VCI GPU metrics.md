---
title: "VCI GPU metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-GPU-metrics"
---

This topic describes the GPU monitoring metrics supported by VCI and the methods for querying these metrics.

<span id=".5oyH5qCH6K-05piO"></span>
## Metrics

The GPU Exporter used for VCI GPU monitoring is compatible with the monitoring metrics provided by the open\-source DCGM Exporter. For more information about the DCGM Exporter, see [Common DCGM metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-DCGM).

<span id=".5oyH5qCH6I635Y-W5pa55byP"></span>
## Metric querying

By default, VCIs expose monitoring data externally on port 1025. You can query VCI GPU monitoring metrics by using the following command:

```Bash
curl http://<pod-ip>:1025/metrics
```


In the command, replace the variable `<pod-ip>` with the IP address of the actual VCI (pod IP address). A complete command example is as follows:

```Bash
curl http://10.16.**.**:1025/metrics
```


<span id=".ZGNnbS3mlK_mjIHnmoTmjIfmoIc="></span>
## Metrics supported by DCGM

<span id=".6aKR546H"></span>
### Frequency


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_SM_CLOCK |Gauge |MHz |Clock frequency of GPU streaming multiprocessors. |
|DCGM_FI_DEV_MEM_CLOCK |Gauge |MHz |GPU memory clock frequency. |


<span id=".5YaF5a2Y"></span>
### Memory


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_FB_FREE |Gauge |MiB |Framebuffer memory free. |
|DCGM_FI_DEV_FB_USED |Gauge |MiB |Framebuffer memory used. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a GPU, graphics card memory (video memory) is also known as frame buffer.</div>


<span id=".5rip5bqm5ZKM5Yqf546H"></span>
### Temperature and power


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_GPU_TEMP |Gauge |℃ |Current GPU temperature. |
|DCGM_FI_DEV_MEMORY_TEMP |Gauge |°C |Current temperature of GPU video memory. |
|DCGM_FI_DEV_POWER_USAGE |Gauge |W |Current GPU power consumed. |
|DCGM_FI_DEV_TOTAL_ENERGY_CONSUMPTION |Counter |mJ |Total energy consumption since the last driver load. |


<span id=".5Yip55So546H"></span>
### Utilization


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_GPU_UTIL |Gauge |% |GPU utilization. |
|DCGM_FI_DEV_MEM_COPY_UTIL |Gauge |% |GPU memory utilization. |
|DCGM_FI_DEV_ENC_UTIL |Gauge |% |GPU encoder utilization. |
|DCGM_FI_DEV_DEC_UTIL |Gauge |% |GPU decoder utilization. |


<span id=".eGlkLemUmeivry3ov53op4Q="></span>
### XID errors and violations


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_XID_ERRORS |Gauge |\- |Value of the last XID error encountered. |
|DCGM_FI_DEV_BOARD_LIMIT_VIOLATION |Counter |μs |Cumulative throttling duration due to board limit constraints. |
|DCGM_FI_DEV_LOW_UTIL_VIOLATION |Counter |μs |Cumulative throttling duration due to low utilization. |
|DCGM_FI_DEV_POWER_VIOLATION |Counter |μs |Cumulative throttling duration due to power constraints. |
|DCGM_FI_DEV_RELIABILITY_VIOLATION |Counter |μs |Cumulative throttling duration due to reliability constraints. |
|DCGM_FI_DEV_SYNC_BOOST_VIOLATION |Counter |μs |Cumulative throttling duration due to sync\-boost constraints. |
|DCGM_FI_DEV_THERMAL_VIOLATION |Counter |μs |Cumulative throttling duration due to thermal constraints. |
|DCGM_CUSTOM_XID_ERRORS_COUNTER |Counter |Count |Total number of XID device errors detected by DCGM at the pod level. |
|DCGM_CUSTOM_XID_ERRORS_TOTAL_COUNTER |Counter |Count |Total number of XID device errors detected by DCGM at the node level. |


<span id=".5YmW5p6Q"></span>
### Profiling


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_PROF_PCIE_RX_BYTES |Counter |B/s |Number of bytes received over the PCIe bus. |
|DCGM_FI_PROF_PCIE_TX_BYTES |Counter |B/s |Number of bytes transmitted over the PCIe bus. |
|DCGM_FI_DEV_PCIE_REPLAY_COUNTER |Counter |Count |Number of retries on the GPU PCIe bus. |
|DCGM_FI_DEV_NVLINK_BANDWIDTH_TOTAL |Counter |\- |Total number of NVLink bandwidth counters for all GPU lanes. |
|DCGM_FI_PROF_GR_ENGINE_ACTIVE |Gauge |% |Ratio of time the graphics or compute engine is active within a time interval. |
|DCGM_FI_PROF_SM_ACTIVE |Gauge |% |Fraction of time at least one warp was active on an SM (Streaming Multiprocessor) within a time interval.<br><br>This value is averaged over all SMs. |
|DCGM_FI_PROF_SM_OCCUPANCY |Gauge |% |Fraction of warps on a multiprocessor relative to the total concurrent warps supported within a time interval.<br><br>This value is averaged over all SMs. |
|DCGM_FI_PROF_PIPE_TENSOR_ACTIVE |Gauge |% |Ratio of cycles the tensor (HMMA) pipe is active per unit time. |
|DCGM_FI_PROF_DRAM_ACTIVE |Gauge |% |Fraction of cycles DRAM is active (a cycle is counted as 100% if there is one DRAM read/write instruction within the cycle). |
|DCGM_FI_PROF_PIPE_FP64_ACTIVE |Gauge |% |Ratio of cycles the F64 pipes are active per unit time. |
|DCGM_FI_PROF_PIPE_FP32_ACTIVE |Gauge |% |Ratio of cycles the fp16 pipes are active per unit time. |
|DCGM_FI_PROF_PIPE_FP16_ACTIVE |Gauge |% |Ratio of cycles the F16 pipes are active per unit time. |


<span id=".5YGc55So55qE5YaF5a2Y6aG16Z2i"></span>
### Disabled memory pages


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_RETIRED_SBE |Counter |Count |Number of retired pages due to single\-bit errors. |
|DCGM_FI_DEV_RETIRED_DBE |Counter |Count |Number of retired pages due to double\-bit errors. |


<span id=".5YW25LuW"></span>
### Others


|Metric name |Metric type |Unit |Metric meaning |
|---|---|---|---|
|DCGM_FI_DEV_VGPU_LICENSE_STATUS |Gauge |\- |vGPU license status. |
|DCGM_FI_DEV_UNCORRECTABLE_REMAPPED_ROWS |Counter |\- |Number of remapped rows for uncorrectable errors. |
|DCGM_FI_DEV_CORRECTABLE_REMAPPED_ROWS |Counter |\- |Number of remapped rows for correctable errors. |
|DCGM_FI_DEV_ROW_REMAP_FAILURE |Gauge |\- |Whether remapping of rows has failed. |
|DCGM_FI_DRIVER_VERSION |Label |\- |GPU driver version. |
|DCGM_FI_PROF_NVLINK_RX_BYTES |Gauge |B/s |Data reception rate over NVLink, including headers and payload. |
|DCGM_FI_PROF_NVLINK_TX_BYTES |Gauge |B/s |Data transmission rate over NVLink, including both headers and payload. |
