---
title: "RayCluster Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/RayCluster_Quick_Start"
---

This section provides a relatively simple way to access RayCluster and execute Ray jobs.

<span id="_1-准备条件"></span>
## 1 Prerequisites


1. Deploy the Ray service in the EMR on VKE product and add the RayCluster component.

2. The RayCluster component is running properly.

3. To Submit Job to RayCluster, you can use either the kubectl command or Ray's Client SDK:

   1. Submitting via kubectl: You need to install the kubectl tool and configure the connection information for the Volcano Engine VKE cluster.

   2. Submitting via Ray SDK: You need to deploy the Ray environment.

      To quickly get started, this section demonstrates logging in to the Head console of RayCluster and submitting a Ray job.


<span id="_2-使用指导"></span>
## 2 Usage guide


1. Through the EMR on VKE console, locate the VKE cluster where RayCluster resides, find the Pod where the Head is located, and access it via the console.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6aa50b247801707a22bbe41d55708b8a.png) </span>


2. This is a python command executed interactively:


```python
import ray

ray.init()
print(ray.cluster_resources())

ds = ray.data.range(100)
ds.show(limit=10)
```



3. Package the above code into a python script named demo.py and submit it using the ray job CLI tool.


```shell
mkdir -p /tmp/ray-working-dir
cd /tmp/ray-working-dir
echo "
import ray

ray.init()
print(ray.cluster_resources())

ds = ray.data.range(100)
ds.show(limit=10)
" > demo.py
ray job submit --working-dir . -- python demo.py
```



4. Refer to [Enable Ray Dashboard metrics capability](https://docs.byteplus.com/docs/E-MapReduce/109463) to view cluster and job information.
