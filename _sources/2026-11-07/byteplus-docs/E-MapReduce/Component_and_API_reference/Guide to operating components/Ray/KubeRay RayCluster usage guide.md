---
title: "KubeRay RayCluster usage guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/KubeRay_RayCluster_usage_guide"
---

This section describes how to submit Ray jobs using RayCluster in VKE. You can also refer to the official website [Getting Started with KubeRay](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started.html) for instructions.

<span id="前置条件"></span>
## **Prerequisites**

Ray jobs can be submitted when the Ray cluster is healthy.

<span id="通过-kubectl-命令提交ray-job"></span>
## **Submit Ray jobs using the kubectl command**


1. Obtain the name of the Head pod


```shell
export NAMESPACE=<命名空间>
export HEAD_POD=$(kubectl get pods --selector=ray.io/node-type=head -o custom-columns=POD:metadata.name --no-headers  -n $NAMESPACE)
echo $HEAD_POD
```



2. Connect to the Head pod to submit a Ray job and retrieve resource information


```shell
# 打印集群资源信息
kubectl exec -it $HEAD_POD  -n $NAMESPACE -- python -c "import ray; ray.init(); print(ray.cluster_resources())"
```



3. Connect to the Head pod to submit a Ray job and execute a Python file


```shell
# 将本地python文件上传到head pod中
echo '
import ray
ray.init()
print(ray.cluster_resources())' > test.py
kubectl exec -it $HEAD_POD -n $NAMESPACE -c ray-head -- mkdir -p /home/ray/work_dir
kubectl cp  test.py -n $NAMESPACE -c ray-head $HEAD_POD:/home/ray/work_dir

# 执行python文件
kubectl exec -n $NAMESPACE -it $HEAD_POD -- ray job submit --working-dir /home/ray/work_dir  -- python /home/ray/work_dir/test.py
```
