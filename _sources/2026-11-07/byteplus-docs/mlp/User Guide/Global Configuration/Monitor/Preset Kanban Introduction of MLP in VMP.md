---
title: "Preset Kanban Introduction of MLP in VMP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Preset_Kanban_Introduction_of_MLP_in_VMP"
---

The Machine Learning Platform is equipped with multiple preset Kanban on VMP. The following are provided Kanban variables and PromQL query statements for your quick use.

<span id="自定义任务看板-mlp-customtask-dashboard"></span>
# Custom tasks Kanban mlp\-customtask\-dashboard

<span id="变量"></span>
## variable


|variable name |display name |query statement |regular |
|---|---|---|---|
|ResourceGroup |Resource Group |mlp_resourcegroup_info |/.*mlp_resource_group="(.* ?)".\*/ |
|ResourceQueue |queue |mlp_resourcequeue_info |/.*mlp_resource_queue="(.* ?)".\*/ |
|CustomTask |custom tasks |mlp_customtask_info |/.*mlp_customtask="(.* ?)"/ |
|Instance |example |mlp_customtask_instance_info |/.*pod="(.* ?)".\*/ |
|TopK |TopK/BottomK Filter Quantity |*  |*  |


<span id="资源利用率的grafana看板json文件"></span>
## Grafana dashboard json file for resource utilization

Resource utilization json dashboard preview download please click the file below

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b34fb5592da435a80535811dc53f934~tplv-goo7wpa0wc-image.image" name="Resource utilization json dashboard.txt">Resource utilization json dashboard.txt</Attachment>


<span id="promql查询语句"></span>
## PromQL query statement

<span id="gpu资源总量"></span>
### total GPU resources

```plain
sum(mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="GPU"})
```


<span id="cpu资源总量-core"></span>
### Total CPU resources (core)

```plain
sum(mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="VCPU"})
```


<span id="memory资源总量"></span>
### Total Memory Resources

```plain
sum(mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="MEMORY"})
```


<span id="实例总数"></span>
### total number of instances

```plain
count(mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="运行中实例总数"></span>
### Total number of running instances

```plain
sum(mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} * ON(pod) mlp_instance_pod_status_phase{phase="Running"})
```


<span id="ready-实例总数"></span>
### Total Ready Instances

```plain
sum(mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} * ON(pod) mlp_instance_pod_status_ready{ready="True"})
```


<span id="gpu利用率-sm-active"></span>
### GPU utilization (SM_ACTIVE)

```plain
Avg: avg(DCGM_FI_PROF_SM_ACTIVE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max(DCGM_FI_PROF_SM_ACTIVE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min(DCGM_FI_PROF_SM_ACTIVE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} )
```


<span id="显存利用率"></span>
### Memory Utilization Rate

```plain
Avg: avg((DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED)) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max((DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED)) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min((DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED)) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="nvlink流入带宽"></span>
### NVLINK inflow bandwidth

```plain
Avg: avg(DCGM_FI_PROF_NVLINK_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max(DCGM_FI_PROF_NVLINK_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min(DCGM_FI_PROF_NVLINK_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="nvlink流出带宽"></span>
### NVLINK outflow bandwidth

```plain
Avg: avg(DCGM_FI_PROF_NVLINK_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} )
Max: max(DCGM_FI_PROF_NVLINK_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} )
Min: min(DCGM_FI_PROF_NVLINK_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} )
```


<span id="gpu-pcie流入带宽"></span>
### GPU PCIE inflows bandwidth

```plain
Avg: avg(DCGM_FI_PROF_PCIE_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max(DCGM_FI_PROF_PCIE_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min(DCGM_FI_PROF_PCIE_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="gpu-pcie流出带宽"></span>
### GPU PCIE outflow bandwidth

```plain
Avg: avg(DCGM_FI_PROF_PCIE_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max(DCGM_FI_PROF_PCIE_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min(DCGM_FI_PROF_PCIE_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="出现xid错误gpu卡数"></span>
### XID error occurred GPU card count

```plain
count(DCGM_FI_DEV_XID_ERRORS AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"}) - count((DCGM_FI_DEV_XID_ERRORS == 0) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="显存已停用页面计数"></span>
### video memory disabled page count

```plain
SBE: sum(DCGM_FI_DEV_RETIRED_SBE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
DBE: sum(DCGM_FI_DEV_RETIRED_DBE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="cpu利用率"></span>
### CPU utilization

```plain
Avg: avg((rate(container_cpu_usage_seconds_total[30s]) / ON(pod) container_spec_cpu_shares * 1000) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max((rate(container_cpu_usage_seconds_total[30s]) / ON(pod) container_spec_cpu_shares * 1000) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min((rate(container_cpu_usage_seconds_total[30s]) / ON(pod) container_spec_cpu_shares * 1000) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="内存利用率"></span>
### Memory utilization

```plain
Avg: avg((container_memory_working_set_bytes / container_spec_memory_limit_bytes) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Max: max((container_memory_working_set_bytes / container_spec_memory_limit_bytes) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
Min: min((container_memory_working_set_bytes / container_spec_memory_limit_bytes) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"})
```


<span id="平均gpu利用率-sm-active-topk实例"></span>
### Average GPU Utilization (SM_ACTIVE) TopK Instances

```plain
{{pod}} : topk($TopK, avg(DCGM_FI_PROF_SM_ACTIVE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"}) by (pod))
```


<span id="平均显存利用率-topk实例"></span>
### Average Memory Utilization TopK instance

```plain
{{pod}} : topk($TopK, avg((DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE)) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"}) by (pod))
```


<span id="平均gpu利用率-sm-active-bottomk实例"></span>
### Average GPU Utilization (SM_ACTIVE) BottomK Instances

```plain
{{pod}} : bottomk($TopK, avg(DCGM_FI_PROF_SM_ACTIVE AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"}) by (pod))
```


<span id="平均显存利用率-bottomk实例"></span>
### Average Memory Utilization BottomK Instances

```plain
{{pod}} : bottomk($TopK, avg((DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE)) AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"}) by (pod))
```


<span id="平均nvlink流入带宽-topk实例"></span>
### Average NVLINK Inflow Bandwidth TopK Instances

```plain
{{pod}} : topk($TopK, avg(DCGM_FI_PROF_NVLINK_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均nvlink流出带宽-topk实例"></span>
### Average NVLINK Outflow Bandwidth TopK Example

```plain
{{pod}} : topk($TopK, avg(DCGM_FI_PROF_NVLINK_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均pcie流入带宽-topk实例"></span>
### Average PCIE Inflow Bandwidth TopK Instances

```plain
{{pod}} : topk($TopK, avg(DCGM_FI_PROF_PCIE_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均pcie流出带宽-topk实例"></span>
### Average PCIE Outflow Bandwidth TopK Example

```plain
{{pod}} : topk($TopK, avg(DCGM_FI_PROF_PCIE_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均nvlink流入带宽-bottomk实例"></span>
### Average NVLINK Inflow Bandwidth BottomK Instances

```plain
{{pod}} : bottomk($TopK, avg(DCGM_FI_PROF_NVLINK_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均nvlink流出带宽-bottomk实例"></span>
### Average NVLINK Outflow Bandwidth BottomK Instances

```plain
{{pod}} : bottomk($TopK, avg(DCGM_FI_PROF_NVLINK_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均pcie流入带宽-bottomk实例"></span>
### Average PCIE Inflow Bandwidth BottomK Instances

```plain
{{pod}} : bottomk($TopK, avg(DCGM_FI_PROF_PCIE_RX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="平均pcie流出带宽-bottomk实例"></span>
### Average PCIE Outflow Bandwidth BottomK Example

```plain
{{pod}} : bottomk($TopK, avg(DCGM_FI_PROF_PCIE_TX_BYTES AND ON(pod) mlp_customtask_instance_info{mlp_customtask=~"$CustomTask"} ) by (pod))
```


<span id="实例gpu利用率-sm-active"></span>
### Instance GPU utilization (SM_ACTIVE)

```plain
Avg: avg(DCGM_FI_PROF_SM_ACTIVE{pod=~"$Instance"})
GPU{{gpu}}: DCGM_FI_PROF_SM_ACTIVE{pod=~"$Instance"}
```


<span id="实例显存利用率"></span>
### instance memory utilization

```plain
Avg: avg(DCGM_FI_DEV_FB_USED{pod=~"$Instance"} / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED))
GPU{{gpu}}: DCGM_FI_DEV_FB_USED{pod=~"$Instance"} / (DCGM_FI_DEV_FB_FREE + DCGM_FI_DEV_FB_USED)
```


<span id="实例内分卡nvlink流入带宽"></span>
### In\-instance sub\-card NVLINK inflow bandwidth

```plain
Avg: avg(DCGM_FI_PROF_NVLINK_RX_BYTES{pod=~"$Instance"})
GPU{{gpu}}: DCGM_FI_PROF_NVLINK_RX_BYTES{pod=~"$Instance"}
```


<span id="实例内分卡nvlink流出带宽"></span>
### In\-instance sub\-card NVLINK outflow bandwidth

```plain
Avg: avg(DCGM_FI_PROF_NVLINK_TX_BYTES{pod=~"$Instance"})
GPU{{gpu}}: DCGM_FI_PROF_NVLINK_TX_BYTES{pod=~"$Instance"}
```


<span id="实例内分卡pcie流入带宽"></span>
### In\-instance sub\-card PCIE inflow bandwidth

```plain
Avg: avg(DCGM_FI_PROF_PCIE_RX_BYTES{pod=~"$Instance"})
GPU{{gpu}}: DCGM_FI_PROF_PCIE_RX_BYTES{pod=~"$Instance"}
```


<span id="实例内分卡pcie流出带宽"></span>
### In\-instance sub\-card PCIE outflow bandwidth

```plain
Avg: DCGM_FI_PROF_PCIE_TX_BYTES{pod=~"$Instance"}
GPU{{gpu}}: DCGM_FI_PROF_PCIE_TX_BYTES{pod=~"$Instance"}
```


<span id="实例-xid-error-详细信息"></span>
### Instance XID Error Details

```plain
GPU{{gpu}}: DCGM_FI_DEV_XID_ERRORS{pod=~"$Instance"}
```


<span id="实例显存已停用页面分卡计数"></span>
### instance memory deactivated page sub\-card count

```plain
GPU{{gpu}}: DBE  : DCGM_FI_DEV_RETIRED_DBE{pod=~"$Instance"} 
GPU{{gpu}}: SBE  : DCGM_FI_DEV_RETIRED_SBE{pod=~"$Instance"}
```


<span id="实例cpu利用率"></span>
### instance CPU utilization

```plain
(rate(container_cpu_usage_seconds_total{pod=~"$Instance"}[30s]) / ON(pod) container_spec_cpu_shares{pod=~"$Instance"} * 1000)
```


<span id="实例内存饱和度"></span>
### instance memory saturation

```plain
container_memory_working_set_bytes{pod=~"$Instance"} / container_spec_memory_limit_bytes
```


<span id="队列资源看板-mlp-gpu-resource-dashboard"></span>
## Queue Resource Kanban mlp\-gpu\-resource\-dashboard

<span id="变量"></span>
### variable


|variable name |display name |query statement |regular |
|---|---|---|---|
|ResourceGroup |Resource Group |mlp_resourcegroup_info |/.*mlp_resource_group="(.* ?)".\*/ |
|ResourceQueue |queue |mlp_resourcequeue_info |/.*mlp_resource_queue="(.* ?)".\*/ |
|TopK |Top/Bottom k Value | | |


<span id="promql查询语句"></span>
## PromQL query statement

<span id="gpu资源总量"></span>
### total GPU resources

```plain
sum(mlp_resourcequeue_quota_capacity{mlp_resource_queue=~"$ResourceQueue", resource="GPU"})
```


<span id="gpu申请量"></span>
### GPU applications

```plain
sum(mlp_resourcequeue_quota_allocated{mlp_resource_queue=~"$ResourceQueue", resource="GPU"})
```


<span id="自定义任务数"></span>
# Number of custom tasks

```plain
sum(mlp_customtask_info{mlp_resource_queue=~"$ResourceQueue"}) or vector(0)
```


<span id="自定义任务实例数"></span>
### Number of custom tasks instances

```plain
sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"}) or vector(0)
```


<span id="在线服务数"></span>
### Number of inference services

```plain
sum(mlp_deployment_info{mlp_resource_queue=~"$ResourceQueue"}) or vector(0)
```


<span id="在线服务实例数"></span>
### Instances of inference services

```plain
sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"}) or vector(0)
```


<span id="开发机数"></span>
### Dev boxes

```plain
sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"}) or vector(0)
```


<span id="开发机实例数"></span>
### Dev boxes instances

```plain
sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"}) or vector(0)
```


<span id="队列gpu申请率"></span>
### queue GPU application rate

<span id="总和申请率"></span>
#### total application rate

```plain
sum(mlp_resourcequeue_quota_allocated{resource="GPU", mlp_resource_queue=~"$ResourceQueue"}) by (mlp_resource_queue) / sum(mlp_resourcequeue_quota_capacity{resource="GPU"}) by (mlp_resource_queue)
```


<span id="自定义任务"></span>
#### custom tasks

```plain
sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="GPU"}) / sum(mlp_resourcequeue_quota_capacity{resource="GPU", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="开发机"></span>
#### Dev boxes

```plain
sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) mlp_instance_resource_requests{resource="GPU"}) / sum(mlp_resourcequeue_quota_capacity{resource="GPU", mlp_resource_queue=~"$ResourceQueue"}) 
```


<span id="在线服务"></span>
#### inference services

```plain
sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) mlp_instance_resource_requests{resource="GPU"}) / sum(mlp_resourcequeue_quota_capacity{resource="GPU", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="负载类型平均gpu利用率-sm-active"></span>
### Load Type Average GPU Utilization (SM_ACTIVE)

<span id="均值"></span>
#### mean

```plain
avg ( mlp_instance_info{mlp_resource_queue=~"$ResourceQueue"} *  ON(pod) group_right(mlp_resource_queue) DCGM_FI_PROF_SM_ACTIVE ) by (mlp_resource_queue)
```


<span id="自定义任务"></span>
#### custom tasks

```plain
avg ( mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} *  ON(pod) group_right(mlp_resource_queue) DCGM_FI_PROF_SM_ACTIVE ) by (mlp_resource_queue)
```


<span id="在线服务"></span>
#### inference services

```plain
avg ( mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} *  ON(pod) group_right(mlp_resource_queue) DCGM_FI_PROF_SM_ACTIVE ) by (mlp_resource_queue)
```


<span id="开发机"></span>
#### Dev boxes

```plain
avg ( mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} *  ON(pod) group_right(mlp_resource_queue) DCGM_FI_PROF_SM_ACTIVE ) by (mlp_resource_queue)
```


<span id="负载类型平均显存利用率"></span>
### Load Type Average Memory Utilization

<span id="均值"></span>
#### mean

```plain
avg(mlp_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_resource_queue) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_resource_queue)
```


<span id="自定义任务"></span>
#### custom tasks

```plain
avg(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_resource_queue) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_resource_queue)
```


<span id="在线服务"></span>
#### inference services

```plain
avg(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_resource_queue) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_resource_queue)
```


<span id="开发机"></span>
#### Dev boxes

```plain
avg(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_resource_queue) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_resource_queue)
```


<span id="队列自定义任务gpu资源申请量-top-k"></span>
### Queuing custom tasks GPU resource requests Top k

```plain
{{mlp_customtask}}: topk($Topk, sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="GPU"}) by (mlp_customtask))
```


<span id="队列在线服务gpu资源申请量-top-k"></span>
### Queue inference services GPU resource requests Top k

```plain
{{mlp_deployment}}: topk($Topk, sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) mlp_instance_resource_requests{resource="GPU"}) by (mlp_deployment))
```


<span id="队列开发机gpu资源申请量-top-k"></span>
### Dev boxes GPU resource requests Top k

```plain
{{mlp_devinstance}}: topk($Topk, sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) mlp_instance_resource_requests{resource="GPU"}) by (mlp_devinstance))
```


<span id="自定义任务gpu利用率-sm-active-top-k"></span>
### Custom tasks GPU utilization (SM_ACTIVE) Top k

```plain
{{mlp_customtask}}: topk($Topk, avg(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) DCGM_FI_PROF_SM_ACTIVE) by (mlp_customtask))
```


<span id="在线服务gpu利用率-sm-active-top-k"></span>
### Inference services GPU utilization (SM_ACTIVE) Top k

```plain
{{mlp_deployment}}: topk($Topk, avg(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) DCGM_FI_PROF_SM_ACTIVE) by (mlp_deployment))
```


<span id="开发机gpu利用率-sm-active-top-k"></span>
### Dev boxes GPU utilization (SM_ACTIVE) Top k

```plain
{{mlp_devinstance}}: topk($Topk, avg(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) DCGM_FI_PROF_SM_ACTIVE) by (mlp_devinstance))
```


<span id="自定义任务gpu利用率-sm-active-bottom-k"></span>
### Custom tasks GPU utilization (SM_ACTIVE) Bottom k

```plain
{{mlp_customtask}}: bottomk($Topk, avg(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) DCGM_FI_PROF_SM_ACTIVE) by (mlp_customtask))
```


<span id="在线服务gpu利用率-sm-active-bottom-k"></span>
### Inference services GPU utilization (SM_ACTIVE) Bottom k

```plain
{{mlp_deployment}}: bottomk($Topk, avg(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) DCGM_FI_PROF_SM_ACTIVE) by (mlp_deployment))
```


<span id="开发机gpu利用率-sm-active-bottom-k"></span>
### Dev boxes GPU utilization (SM_ACTIVE) Bottom k

```plain
{{mlp_devinstance}}: bottomk($Topk, avg(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) DCGM_FI_PROF_SM_ACTIVE) by (mlp_devinstance))
```


<span id="自定义任务显存利用率-top-k"></span>
### Custom tasks memory utilization Top k

```plain
{{mlp_customtask}}: topk($Topk, avg(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_customtask))
```


<span id="在线服务显存利用率-top-k"></span>
### Memory utilization of inference services Top k

```plain
{{mlp_deployment}}: topk($Topk, avg(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_deployment))
```


<span id="开发机显存利用率-top-k"></span>
### Dev boxes Utilization Top k

```plain
{{mlp_devinstance}}: topk($Topk, avg(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_devinstance))
```


<span id="自定义任务显存利用率-bottom-k"></span>
### Custom tasks Memory utilization Bottom k

```plain
{{mlp_customtask}}: bottomk($Topk, avg(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_customtask))
```


<span id="在线服务显存利用率-bottom-k"></span>
### Memory utilization of inference services Bottom k

```plain
{{mlp_deployment}}: bottomk($Topk, avg(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_deployment))
```


<span id="开发机显存利用率-bottom-k"></span>
### Dev boxes Utilization Bottom k

```plain
{{mlp_devinstance}}: bottomk($Topk, avg(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) (DCGM_FI_DEV_FB_USED / (DCGM_FI_DEV_FB_USED + DCGM_FI_DEV_FB_FREE))) by (mlp_devinstance))
```


<span id="cpu资源总量-core"></span>
### Total CPU resources (core)

```plain
mlp_resourcequeue_quota_capacity{resource="VCPU", mlp_resource_queue=~"$ResourceQueue"}
```


<span id="cpu资源申请量-core"></span>
### CPU resource request (core)

```plain
mlp_resourcequeue_quota_allocated{mlp_resource_queue=~"$ResourceQueue", resource="VCPU"}
```


<span id="memory资源总量"></span>
### Total Memory Resources

```plain
mlp_resourcequeue_quota_capacity{resource="Memory", mlp_resource_queue=~"$ResourceQueue", unit="GiB"}
```


<span id="memory资源申请量"></span>
### Memory resource requests

```plain
mlp_resourcequeue_quota_allocated{mlp_resource_queue=~"$ResourceQueue", resource="Memory"}
```


<span id="云盘总量"></span>
### total cloud disk

```plain
sum(mlp_resourcequeue_volume_capacity{mlp_resource_queue=~"$ResourceQueue"})
```


<span id="云盘容量申请量"></span>
### Cloud disk capacity application volume

```plain
sum(mlp_resourcequeue_volume_allocated{mlp_resource_queue=~"$ResourceQueue"})
```


<span id="队列cpu申请率"></span>
### queue CPU request rate

<span id="总和申请率"></span>
#### total application rate

```plain
mlp_resourcequeue_quota_allocated{resource="VCPU", mlp_resource_queue=~"$ResourceQueue"} / mlp_resourcequeue_quota_capacity
```


<span id="自定义任务申请率"></span>
#### Customs tasks application rate

```plain
sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="VCPU"}) / sum(mlp_resourcequeue_quota_capacity{resource="VCPU", mlp_resource_queue=~"$ResourceQueue"}) 
```


<span id="开发机申请率"></span>
#### Dev boxes application rate

```plain
sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) mlp_instance_resource_requests{resource="VCPU"}) / sum(mlp_resourcequeue_quota_capacity{resource="VCPU", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="在线服务申请率"></span>
#### Inference services request rate

```plain
sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) mlp_instance_resource_requests{resource="VCPU"}) / sum(mlp_resourcequeue_quota_capacity{resource="VCPU", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="队列memory申请率"></span>
### Queue Memory Request Rate

<span id="总和申请率"></span>
#### total application rate

```plain
mlp_resourcequeue_quota_allocated{resource="Memory", mlp_resource_queue=~"$ResourceQueue"} / mlp_resourcequeue_quota_capacity
```


<span id="开发机申请率"></span>
#### Dev boxes application rate

```plain
sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) mlp_instance_resource_requests{resource="MEMORY"}) / sum(mlp_resourcequeue_quota_capacity{resource="Memory", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="自定义任务申请率"></span>
#### Customs tasks application rate

```plain
sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="MEMORY"}) / sum(mlp_resourcequeue_quota_capacity{resource="Memory", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="在线服务申请率"></span>
#### Inference services request rate

```plain
sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) mlp_instance_resource_requests{resource="MEMORY"}) / sum(mlp_resourcequeue_quota_capacity{resource="Memory", mlp_resource_queue=~"$ResourceQueue"})
```


<span id="队列云盘容量申请率"></span>
### queue cloud disk capacity application rate

```plain
{{flavor}}: mlp_resourcequeue_volume_allocated / mlp_resourcequeue_volume_capacity{mlp_resource_queue=~"$ResourceQueue"}
```


<span id="队列自定义任务cpu资源申请量-top-k-core"></span>
### Queuing custom tasks CPU resource requirementsTop k (core)

```plain
{{mlp_customtask}}: topk($Topk, sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="VCPU"}) by (mlp_customtask))
```


<span id="队列在线服务cpu资源申请量-top-k-core"></span>
### Queue inference services CPU resource request Top k (core)

```plain
{{mlp_deployment}}: topk($Topk, sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) mlp_instance_resource_requests{resource="VCPU"}) by (mlp_deployment))
```


<span id="队列开发机cpu资源申请量-top-k-core"></span>
### Dev boxes CPU resource request Top k (core)

```plain
{{mlp_devinstance}}: topk($Topk, sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) mlp_instance_resource_requests{resource="VCPU"}) by (mlp_devinstance))
```


<span id="队列自定义任务memory资源申请量-top-k"></span>
### Queue custom tasks Memory resource requests Top k

```plain
{{mlp_customtask}}: topk($Topk, sum(mlp_customtask_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_customtask) mlp_instance_resource_requests{resource="MEMORY"}) by (mlp_customtask))
```


<span id="队列在线服务memory资源申请量-top-k"></span>
### Queue inference services Memory resource requests Top k

```plain
{{mlp_deployment}}: topk($Topk, sum(mlp_deployment_instance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_deployment) mlp_instance_resource_requests{resource="MEMORY"}) by (mlp_deployment))
```


<span id="队列开发机memory资源申请量-top-k"></span>
### Dev boxes Memory resource request

```plain
{{mlp_devinstance}}: topk($Topk, sum(mlp_devinstance_info{mlp_resource_queue=~"$ResourceQueue"} * ON(pod) group_right(mlp_devinstance) mlp_instance_resource_requests{resource="MEMORY"}) by (mlp_devinstance))
```
