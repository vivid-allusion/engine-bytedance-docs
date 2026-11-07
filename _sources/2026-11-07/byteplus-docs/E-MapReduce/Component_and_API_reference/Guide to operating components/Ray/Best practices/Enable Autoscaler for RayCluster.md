---
title: "Enable Autoscaler for RayCluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Enable_Autoscaler_for_RayCluster"
---

By configuring Ray Autoscaler, automatic scaling of the cluster can be achieved. The Autoscaler adjusts the number of nodes (Ray Pods) in the cluster based on the resources required by tasks, actors, or placement groups. The Autoscaler scales the cluster based on logical resource requests (expressed by ray.remote), rather than physical resource utilization. Additionally, the Autoscaler can reduce workload costs, but increases node startup overhead.

Ray Autoscaler operates as a separate entity within a sidecar container in the Ray head Pod, as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_16012d51e66c6e23fc6d1b35ed31bd81.png) </span>

<span id="_1-准备条件"></span>
## 1. Prerequisites


1. Deploy the Ray service in the EMR on VKE product.

2. Submit Job to RayCluster, which can be done using the kubectl command or Ray's Client SDK. It is necessary to install the kubectl command and deploy the Ray environment. Refer to the usage guide section.


<span id="_2-使用指导"></span>
## 2. Usage guide


1. When deploying the RayCluster service, use the "Add via YAML" method, and set enableInTreeAutoscaling to true in the YAML file:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_31f90530e829ca0df971d831790fa809.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_730917e9b2f240f1407c9073e68c3f89.png) </span>

2. After RayCluster deployment is complete, check in the VKE container service. In the head pod, verify the status of the autoscaler to see if it is Running.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5850ccf475a386deca906538a6ca3dac.png) </span>

3. Run the following Job in the Ray Cluster.


Define a `long_running_task` remote function that sleeps for 600 seconds. Submit 10 `long_running_task` tasks:

```python
import ray
import time
import os

# Start Ray using the autoscaler configuration file
ray.init(address='auto')

@ray.remote(num_cpus=1)
def long_running_task():
    print(f"Sleeping for 600 seconds on node {os.uname()[1]}")
    time.sleep(600)
    return "Task completed"

# Submit multiple tasks, which will trigger the autoscaler to add nodes as needed
object_refs = [long_running_task.remote() for _ in range(10)]

# Wait for all tasks to complete
ray.get(object_refs)

print("All tasks completed.")
```



4. Check the worker pod information; there are 10 pods:

   ```shell
   kubectl get pod -n <命名空间> -w
   ```
   


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ada8e89d9e677cacff981a310a9fa850.png) </span>

You can also check the autoscaler logs. The 10 `long_running_task` tasks require 10 workers to execute. This can also be seen from the logs below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_876ddaea592bc2a6367b566de48b236f.png) </span>

<span id="_3-相关文档"></span>
## 3 **related articles**

For more information, refer to the official website [KubeRay Autoscaling](https://docs.ray.io/en/latest/cluster/kubernetes/user-guides/configuring-autoscaling.html#enabling-autoscaling).
