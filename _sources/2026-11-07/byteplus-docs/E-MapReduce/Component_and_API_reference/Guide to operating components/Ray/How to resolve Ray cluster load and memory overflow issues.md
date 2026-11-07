---
title: "How to resolve Ray cluster load and memory overflow issues"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/How_to_resolve_Ray_cluster_load_and_memory_overflow_issues"
---

In distributed computing, memory management and load balancing are two critical issues. Ray provides a range of tools and methods to help developers monitor and optimize memory usage, ensuring that the cluster remains stable under high load. This article introduces how to address Ray cluster load, as well as how to locate and resolve memory overflow issues.

<span id="ed10670e"></span>
## Monitor Ray cluster memory usage

<span id="1ed14e43"></span>
### View cluster monitoring in the EMR console

The EMR management platform provides monitoring for Ray clusters, allowing you to view cluster resource usage, including node resource status and task monitoring information.

<span id="9966db85"></span>
### Use the `ray memory` command

You can also use the `ray memory` command to view a detailed report of memory usage:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c80dd7f03934b7faf109f88f609fcd5~tplv-goo7wpa0wc-image.image" width="2266px" /></div>


This command outputs the objects currently in object storage and their memory usage, helping to identify which objects are consuming large amounts of memory.

<span id="d47f6dc3"></span>
### View logs in Ray

Ray records memory usage in the logs. If a task fails due to insufficient memory, relevant information can also be found in the logs.

Log files are usually located in the `/tmp/ray/session_latest/logs` directory or `/var/log/emr/ray/session_latest/logs`.

You can also view logs in the Ray dashboard interface.

<span id="e99bd80f"></span>
## Approaches to resolving memory overflow

<span id="770a37e2"></span>
### Reduce the load on the Head node

A Ray cluster consists of one Head node and multiple worker nodes, where the Head node plays a crucial role. It is not only responsible for cluster management and coordination, but also undertakes many key functions: cluster management, task scheduling, logging, monitoring, and more. If the Head node fails, the operation of the entire cluster will be severely affected.

Therefore, in large\-scale clusters, it is recommended to dedicate the Head node to cluster management tasks and not to execute compute tasks; that is, avoid starting worker processes on the Head node. By adding the parameter “`num-cpus: '0'`” when starting the Ray Head, Ray workloads with non\-zero CPU requirements will be prevented from being scheduled to the Head node.

**Example**

Taking RayJob as an example, in the corresponding Yaml file below, configure “`num-cpus: '0'`” when starting the Head:

```YAML
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1 
spec:
  entrypoint: python /home/ray/samples/sample_code.py
      
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.30.0' # should match the Ray version in the image of the containers
    # Ray Head pod template
    HeadGroupSpec:
      rayStartParams:
        dashboard-host: '0.0.0.0'
        num-cpus: '0'
      template:
        spec:
          containers:
            - name: ray-Head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.30.0-py3.11-ubuntu20.04-207-1.5.0
              ports:
                - containerPort: 6379
                  name: gcs-server
                - containerPort: 8265 # Ray dashboard
                  name: dashboard
                - containerPort: 10001
                  name: client
              resources:
                limits:
                  cpu: "5"
                  memory: 20Gi
                requests:
                  cpu: "5"
                  memory: 20Gi
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.30.0-py3.11-ubuntu20.04-207-1.5.0
                lifecycle: 
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "5"
                    memory: 20Gi
                  requests:
                    cpu: "5"
                    memory: 20Gi
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    import time
    def map1(n):
        time.sleep(1)
        return n

    def column_udf_class(col, udf):
        class UDFClass:
            def __call__(self, row):
                return {col: udf(row[col])}
        return UDFClass

    ray.data.range(20).map_batches(
            column_udf_class("id", map1),
            concurrency=(10),
            num_cpus = 0.5
        ).show()
```


In this example, the job script `/home/ray/samples/sample_code.py` launches 10 task jobs. In Ray's UI, you can see that all 10 jobs are running on the worker node.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1df11ff7af845dfa1c5c29bb43a7d42~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c09b6a4795245ac8de6a360f02ca83c~tplv-goo7wpa0wc-image.image) </span>

<span id="e50980a5"></span>
### Reduce task concurrency

In high\-concurrency environments, running multiple tasks simultaneously consumes a large amount of memory resources, which may lead to insufficient memory. By reducing concurrency, you can decrease the number of tasks running at the same time, thereby reducing memory usage and avoiding OOM issues.


* Configure the `num_cpus` parameter.

   By increasing the `num_cpus` parameter in [ray.remote()](https://docs.ray.io/en/latest/ray-core/api/doc/ray.remote.html#ray.remote), you can control task concurrency. Increasing CPU requirements can reduce the number of tasks running simultaneously, thus lowering memory usage.

   **Example**

   ```Python
   import ray
   
   ray.init()
   
   # 定义一个内存密集型任务，并增加 num_cpus 参数
   @ray.remote(num_cpus=2)  # 每个任务需要 2 个 CPU
   def memory_intensive_task():
       # 模拟内存密集型操作
       large_array = [0] * (10**8)
       return len(large_array)
   
   # 提交多个任务
   tasks = [memory_intensive_task.remote() for _ in range(20)]
   
   # 获取结果
   results = ray.get(tasks)
   
   print(results)
   ```
   

* In the ray.data module, some APIs allow you to adjust concurrency by configuring the concurrency parameter.

   **Example**

   [ray.data.Dataset.map_batches](https://docs.ray.io/en/latest/data/api/doc/ray.data.Dataset.map_batches.html#ray.data.Dataset.map_batches)

   ```Python
   import ray
   import time
   
   # 初始化 Ray
   ray.init()
   
   # 定义两个模拟的 UDF（用户定义函数），每个函数都会睡眠 1 秒钟
   def map1(n):
       time.sleep(1)
       return n
   
   def map2(n):
       time.sleep(1)
       return n
   
   # 定义一个类，用于将列名和 UDF 结合起来
   def column_udf_class(col, udf):
       class UDFClass:
           def __call__(self, row):
               return {col: udf(row[col])}
       return UDFClass
   
   # 创建一个包含 1000 个整数的 Ray Dataset
   dataset = ray.data.range(1000)
   
   # 使用 map_batches 处理数据集，并设置并发度
   processed_dataset = (
       dataset.map_batches(
           column_udf_class("id", map1),
           concurrency=2,  # 设置并发度为 2
       )
       .map_batches(
           column_udf_class("id", map2),
           concurrency=3,  # 设置并发度为 3
       )
   )
   
   # 显示处理后的数据集
   processed_dataset.show()
   ```
   


<span id="8aaadb4a"></span>
### Increase Ray node memory configuration

When starting a Ray cluster, increasing the memory of both the worker and Head nodes can reduce the risk of insufficient memory. Especially when processing large\-scale datasets or memory\-intensive tasks, increasing memory configuration can significantly improve task success rates and cluster stability.

<span id="dd39d74c"></span>
### Release object storage in a timely manner

After a task is completed, promptly delete objects that are no longer needed to reduce memory usage in object storage. You can use the `ray._private.internal_api.free` function to manually delete objects that are no longer needed.

**Example**

```Python
import numpy as np
import ray

ray.init()

@ray.remote
def create_large_object():
    return np.zeros(1000000)

object_id = create_large_object.remote()

# 使用对象
result = ray.get(object_id)

# 删除对象
ray._private.internal_api.free([object_id])
```
