---
title: "mGPU metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-mGPU"
---

mGPU is a container\-sharing GPU solution provided by BytePlus, leveraging kernel\-level virtualization for GPU isolation combined with a self\-developed scheduling framework. This topic describes the common query metrics of mGPU.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="GYw7RHcx"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|nvml_pod_mem_utilization |Basic metric |
|nvml_pod_mem_usage |Basic metric |
|nvml_pod_mem_request |Basic metric |
|nvml_pod_core_utilization |Basic metric |
|nvml_pod_core_usage |Basic metric |
|nvml_pod_core_request |Basic metric |
|nvml_container_mem_utilization |Basic metric |
|nvml_container_mem_usage |Basic metric |
|nvml_container_mem_request |Basic metric |
|nvml_container_core_utilization |Basic metric |
|nvml_container_core_usage |Basic metric |
|nvml_container_core_request |Basic metric |
|DCGM_FI_DEV_DEC_UTIL |Basic metric |
|DCGM_FI_DEV_ENC_UTIL |Basic metric |
|DCGM_FI_DEV_FB_FREE |Basic metric |
|DCGM_FI_DEV_FB_USED |Basic metric |
|DCGM_FI_DEV_GPU_TEMP |Basic metric |
|DCGM_FI_DEV_GPU_UTIL |Basic metric |
|DCGM_FI_DEV_MEM_COPY_UTIL |Basic metric |
|DCGM_FI_DEV_NVLINK_BANDWIDTH_TOTAL |Basic metric |
|DCGM_FI_DEV_POWER_USAGE |Basic metric |
|DCGM_FI_DEV_XID_ERRORS |Basic metric |


<span id="XP5gBCCp"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|nvml_container_mem_copy_util |Other metrics |
|nvml_pod_mem_copy_util |Other metrics |
|DCGM_FI_DEV_PCIE_TX_THROUGHPUT |Other metrics |
|DCGM_FI_DEV_PCIE_RX_THROUGHPUT |Other metrics |
|DCGM_FI_DEV_ECC_SBE_VOL_TOTAL |Other metrics |
|DCGM_FI_DEV_ECC_DBE_VOL_TOTAL |Other metrics |
|DCGM_FI_DEV_ECC_SBE_AGG_TOTAL |Other metrics |
|DCGM_FI_DEV_ECC_DBE_AGG_TOTAL |Other metrics |
|DCGM_FI_DEV_RETIRED_PENDING |Other metrics |
|DCGM_FI_DEV_NVLINK_CRC_FLIT_ERROR_COUNT_TOTAL |Other metrics |
|DCGM_FI_DEV_NVLINK_CRC_DATA_ERROR_COUNT_TOTAL |Other metrics |
|DCGM_FI_DEV_NVLINK_REPLAY_ERROR_COUNT_TOTAL |Other metrics |
|DCGM_FI_DEV_NVLINK_RECOVERY_ERROR_COUNT_TOTAL |Other metrics |
|DCGM_FI_DEV_NVLINK_BANDWIDTH_L0 |Other metrics |
|DCGM_FI_DEV_MEM_CLOCK |Other metrics |
|DCGM_FI_DEV_PCIE_REPLAY_COUNTER |Other metrics |
|DCGM_FI_DEV_TOTAL_ENERGY_CONSUMPTION |Other metrics |
|DCGM_FI_DEV_VGPU_LICENSE_STATUS |Other metrics |
|DCGM_FI_PROF_DRAM_ACTIVE |Other metrics |
|DCGM_FI_PROF_GR_ENGINE_ACTIVE |Other metrics |
|DCGM_FI_PROF_PCIE_RX_BYTES |Other metrics |
|DCGM_FI_PROF_PCIE_TX_BYTES |Other metrics |
|DCGM_FI_PROF_PIPE_TENSOR_ACTIVE |Other metrics |
|DCGM_FI_DEV_POWER_VIOLATION |Other metrics |
|DCGM_FI_DEV_THERMAL_VIOLATION |Other metrics |
|DCGM_FI_DEV_SYNC_BOOST_VIOLATION |Other metrics |
|DCGM_FI_DEV_BOARD_LIMIT_VIOLATION |Other metrics |
|DCGM_FI_DEV_LOW_UTIL_VIOLATION |Other metrics |
|DCGM_FI_DEV_RELIABILITY_VIOLATION |Other metrics |
|DCGM_FI_DEV_RETIRED_SBE |Other metrics |
|DCGM_FI_DEV_UNCORRECTABLE_REMAPPED_ROWS |Other metrics |
|DCGM_FI_DEV_CORRECTABLE_REMAPPED_ROWS |Other metrics |
|DCGM_FI_DEV_ROW_REMAP_FAILURE |Other metrics |
|DCGM_FI_PROF_SM_ACTIVE |Other metrics |
|DCGM_FI_PROF_SM_OCCUPANCY |Other metrics |
|DCGM_FI_PROF_PIPE_FP64_ACTIVE |Other metrics |
|DCGM_FI_PROF_PIPE_FP32_ACTIVE |Other metrics |
|DCGM_FI_PROF_PIPE_FP16_ACTIVE |Other metrics |
|DCGM_FI_DEV_RETIRED_DBE |Other metrics |
|DCGM_FI_PROF_NVLINK_RX_BYTES |Other metrics |
|DCGM_FI_PROF_NVLINK_TX_BYTES |Other metrics |
