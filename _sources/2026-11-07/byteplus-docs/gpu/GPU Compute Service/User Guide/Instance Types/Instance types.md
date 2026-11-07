---
title: "Instance types"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types"
---

The cloud platform provides multiple GPU instance types for you to choose. Different types offer different virtualization capabilities for different business applications and service scenarios.

<span id="cEcsYPgG"></span>
## Background

Before viewing the characteristics and metrics of each instance type family, you may need to get the following information:


<span id="MSFJ1eLa"></span>
### Learn about instance naming and type recommendations

Before purchasing an instance, you can refer to the following documents to learn the instance naming rules and information on how to choose an instance type based on your business scenarios.


* [Instance naming and type recommendations (x86 and Bare Metal)](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice)



<span id="lWC8LjZn"></span>
### Estimate instance fee

After selecting an instance type, you may want to know the approximate instance fee under each billing method. You can view fees through the [price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2). This price is for reference only. The actual costs are the fee results displayed when you order in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance).



<span id="HtbHSGm1"></span>
### View regions where instances are available for sale

Instance types available for sale may vary in [different regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones#.5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo). You can refer to [Viewing regions where instances are available for sale](https://docs.byteplus.com/en/docs/ecs/Viewing_regions_where_instances_are_available_for_sale) to check the availability of the target instance in the target region.



<span id="yDb3QU3N"></span>
### Evaluate resource quota

Instance types available for sale may vary in [different regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones#.5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo). You can refer to [Viewing regions where instances are available for sale](https://docs.byteplus.com/en/docs/ecs/Viewing_regions_where_instances_are_available_for_sale) to check the availability of the target instance in the target region.



<span id="uFiBD884"></span>
### Directly purchase instance

Go to the [instance purchase page](https://console.byteplus.com/ecs/buy?) and make a purchase by referring to [purchasing instance based on the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). In addition, the platform provides [multiple purchasing methods](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances) for you to choose from.

If you want to purchase Heterogeneous Compute\-optimized instances, please refer to [Purchasing GPU Accelerated instances](https://docs.byteplus.com/en/docs/gpu/Buying-GPU-Accelerated-instances) and [Purchasing HPC-optimized instances](https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances).



<span id="8sk0R6gJ"></span>
### View information about instance type change

If your instance does not meet or exceeds your business requirements, refer to [Instance types supporting type change](https://docs.byteplus.com/en/docs/ecs/Overview-2) to check whether the current instance type can be changed to other types.



<span id="8zyvvw5T"></span>
### View the images supported by the instance

The images supported by different instance types vary. You can refer to [Driver installation guidelines](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide) for more details. This guide is for reference only. Please check in the console for actual supported images.


<span id="FZuiXLTc"></span>
## GPU instance type family list

Instance types are divided into different instance type families based on underlying hardware performance. Each instance type family adopts different processors, CPU\-to\-memory ratios, GPU graphics cards, volume types, and virtualization methods for network interfaces to provide differentiated computing, storage, and network performance. Based on the CPU, RAM, GPU, and other resources, an instance type family includes multiple instance types. The higher the specification, the better the performance. GPU instance type families provided by the platform are shown in the table below. To learn about the characteristics and detailed metrics for GPU instance types, please refer to the documents in the "Type" column in the table below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The Beta feature is currently not available. If you need trial use, please contact your account manager to apply. You will be able to access the features and documents after successful application.</div>


* <div data-tips="true" data-tips-type="warning">The maximum volume varies based on instance type (refer to the "Volume Quantity" column in the "Instance types and metrics" table for each instance type). If the ECS instance is created based on a CentOS 6.x image, a maximum of 8 volumes can be mounted (including one system volume).</div>



&nbsp;


|**Type** |**Instance type family** |
|---|---|
|GPU Accelerated |[pni3l](https://docs.byteplus.com/en/docs/gpu/GPU-Accelerated-gni3cl#Ej0qQ7wc) |
||[gni3c](https://docs.byteplus.com/en/docs/gpu/GPU-Accelerated-gni3cl#AmEoLCBb) |
||[ebmgni3c](https://docs.byteplus.com/en/docs/gpu/GPU-Accelerated-gni3cl#A4qG3ldp) |
||[gni3cl](https://docs.byteplus.com/en/docs/gpu/GPU-Accelerated-gni3cl#SBCQw2X5) |
|GPU Rendering |[gni3cl-vws](https://docs.byteplus.com/en/docs/gpu/GPU_Rendering#Ct0CrumL) (Beta) |
||[gni3cg-vws](https://docs.byteplus.com/en/docs/gpu/GPU_Rendering#EDy4nd9u)(Beta) |
|HPC\-optimized |[hpcpni3ln](https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h#ycaqZd1y) (Beta) |
||[ebmhpcpni3ln](https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h#WGZcMGnX) (Beta) |
||[hpcpni3le](https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h)(Beta) |
||[ebmhpcpni3l](https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h#dQ90MFyH) (Beta) |
||[hpcpni3h](https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h) (Beta) |
