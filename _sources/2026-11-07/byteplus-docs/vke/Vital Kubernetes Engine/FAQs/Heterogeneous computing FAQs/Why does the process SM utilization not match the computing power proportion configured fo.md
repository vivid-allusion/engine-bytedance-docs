---
title: "Why does the process SM utilization not match the computing power proportion configured for the mGPU?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-does-the-SM-utilization-not-match-the-mGPU-computing-power-ratio-configuration"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

The process Stream Multi\-processor (SM) utilization that is viewed through the NVIDIA Management Library (NVML) API or nvidia\-smi pmon does not match the computing power proportion configured for the mGPU.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

The SM utilization collected by official NVIDIA tools indicates the SM utilization within a fixed cycle. The computing power proportion configured for the mGPU indicates the proportion of computing power resources used by user applications throughout their lifecycle. These two metrics are measured on different time dimensions and cannot be directly compared.

To evaluate the computing power isolation capability of mGPU, you need to measure it by using performance metrics, such as QPS, of the user application.
