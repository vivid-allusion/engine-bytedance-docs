---
title: "nvidia-device-plugin metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-DCGM"
---

nvidia\-device\-plugin serves as a device management component for NVIDIA GPUs in Vital Kubernetes Engine (VKE) cluster. It allows NVIDIA GPUs to be used in containers. It monitors NVIDIA GPUs by using NVIDIA DCGM in Linux systems. This topic describes the common metrics of nvidia\-device\-plugin in the VKE cluster.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="QhKBUiT9"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|DCGM_FI_DEV_XID_ERRORS |Basic metric |
|DCGM_FI_DEV_SM_CLOCK |Basic metric |
|DCGM_FI_DEV_POWER_USAGE |Basic metric |
|DCGM_FI_DEV_NVLINK_BANDWIDTH_TOTAL |Basic metric |
|DCGM_FI_DEV_MEMORY_TEMP |Basic metric |
|DCGM_FI_DEV_MEM_COPY_UTIL |Basic metric |
|DCGM_FI_DEV_GPU_UTIL |Basic metric |
|DCGM_FI_DEV_GPU_TEMP |Basic metric |
|DCGM_FI_DEV_FB_USED |Basic metric |
|DCGM_FI_DEV_FB_FREE |Basic metric |
|DCGM_FI_DEV_ENC_UTIL |Basic metric |
|DCGM_FI_DEV_DEC_UTIL |Basic metric |
|DCGM_EXP_XID_ERRORS_COUNT |Basic metric |


<span id="2ZPeOXFY"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|DCGM_FI_PROF_NVLINK_TX_BYTES |Other metrics |
|DCGM_FI_PROF_NVLINK_RX_BYTES |Other metrics |
|DCGM_FI_PROF_PIPE_FP16_ACTIVE |Other metrics |
|DCGM_FI_PROF_PIPE_FP32_ACTIVE |Other metrics |
|DCGM_FI_PROF_PIPE_FP64_ACTIVE |Other metrics |
|DCGM_FI_PROF_SM_OCCUPANCY |Other metrics |
|DCGM_FI_PROF_SM_ACTIVE |Other metrics |
|DCGM_FI_DEV_ROW_REMAP_FAILURE |Other metrics |
|DCGM_FI_DEV_CORRECTABLE_REMAPPED_ROWS |Other metrics |
|DCGM_FI_DEV_UNCORRECTABLE_REMAPPED_ROWS |Other metrics |
|DCGM_FI_DEV_RETIRED_DBE |Other metrics |
|DCGM_FI_DEV_RETIRED_SBE |Other metrics |
|DCGM_FI_DEV_RELIABILITY_VIOLATION |Other metrics |
|DCGM_FI_DEV_LOW_UTIL_VIOLATION |Other metrics |
|DCGM_FI_DEV_BOARD_LIMIT_VIOLATION |Other metrics |
|DCGM_FI_DEV_SYNC_BOOST_VIOLATION |Other metrics |
|DCGM_FI_DEV_THERMAL_VIOLATION |Other metrics |
|DCGM_FI_DEV_POWER_VIOLATION |Other metrics |
|DCGM_CUSTOM_XID_ERRORS_TOTAL_COUNTER |Basic metric |
|DCGM_FI_PROF_PIPE_TENSOR_ACTIVE |Other metrics |
|DCGM_FI_PROF_PCIE_TX_BYTES |Other metrics |
|DCGM_FI_PROF_PCIE_RX_BYTES |Other metrics |
|DCGM_FI_PROF_GR_ENGINE_ACTIVE |Other metrics |
|DCGM_FI_PROF_DRAM_ACTIVE |Other metrics |
|DCGM_FI_DEV_VGPU_LICENSE_STATUS |Other metrics |
|DCGM_FI_DEV_TOTAL_ENERGY_CONSUMPTION |Other metrics |
|DCGM_FI_DEV_PCIE_REPLAY_COUNTER |Other metrics |
|DCGM_FI_DEV_MEM_CLOCK |Other metrics |
|DCGM_CUSTOM_XID_ERRORS_COUNTER |Other metrics |
|DCGM_EXP_CLOCK_EVENTS_COUNT |Other metrics |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about other DCGM metrics, refer to <a href="https://docs.nvidia.com/datacenter/cloud-native/gpu-telemetry/dcgm-exporter.html">About GPU Telemetry</a>.</div>
