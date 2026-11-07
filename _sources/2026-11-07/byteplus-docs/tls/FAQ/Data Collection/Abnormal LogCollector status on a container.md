---
title: "Abnormal LogCollector status on a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/abnormal_logcollector_status_on_a_container"
---

If the LogCollector heartbeat status of a container is abnormal, verify the LogCollector status in the corresponding pod first. If the status is Running, it means LogCollector is installed and running properly. If the status is not Running, it means an installation or running error occurs. This topic introduces how to troubleshoot such errors.

<span id="检查容器-logcollector-运行状态"></span>
## Verifying the LogCollector status in the container

Log on to the Kubernetes cluster, then run the following command to view the LogCollector status:

```shell
kubectl -n ${namespace}  get pods  | grep ${Daemonset}
```


In the following example, the name of the DaemonSet is log\-collector, and its namespace is tls\-log.

```shell
kubectl -n tls-log  get pods  | grep log-collector
```


If all values of the `STATUS` field are Running in the response, it means LogCollector is installed in the Kubernetes cluster and is running properly. If no status information is returned or the status is Evicted or another value, refer to the following solutions for further troubleshooting.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_182808c0c288bd7375bae3ad7d4246ea.png) </span>

<span id="处理方案"></span>
## Solutions

<span id="没有状态信息"></span>
### No status information

**Issue description**: In the response, no pod named log\-collector\-xxxxx is returned for the NAME field.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2376f89d944299a6e161a2bcdeb96467.png) </span>

**Cause**: LogCollector is not installed in the Kubernetes cluster.

**Solution**:


1. Install and run LogCollector. For more information, refer to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet) and [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Make sure that LogCollector is installed correctly based on the Region where Torch Log Service is deployed and the network type.   </div>
   

2. Run the following command again to verify the LogCollector status. If the status is Running, it means LogCollector is installed properly.

   ```shell
   kubectl -n tls-log  get pods  | grep log-collector
   ```
   


<span id="状态为-evicted"></span>
### Evicted status

**Issue description**: In the response, Evicted is returned for the Status field of the specified pod.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2018624e805f952438f32b1460de662d.png) </span>

**Cause**: If the status is Evicted for the pod, it means a taint exists on the node and no toleration is set for the LogCollector DaemonSet. As a result, the LogCollector pod cannot be scheduled to the node. For more information on taints and tolerations, refer to [Kubernetes documentation](https://kubernetes.io/zh-cn/docs/concepts/scheduling-eviction/taint-and-toleration/).

**Solution**:

Set a toleration for the LogCollector DaemonSet. Assume that a node has a taint `key1=value1:NoSchedule`, where `key1` is the key, `value1` is the value, and `NoSchedule` is the effect. This means that no pod can be scheduled to the node unless it has a matching toleration.


1. In `logcollector_ds.yaml`, set a toleration for the LogCollector DaemonSet.

   In the `spec.template.spec` part of `logcollector_ds.yaml`, add the following toleration to match the taint `key1=value1:NoSchedule` of the node, ensuring that the LogCollector pod can be scheduled to the node:

   ```yaml
   apiVersion: apps/v1
   kind: DaemonSet
   metadata:
     ......
   spec:
     ......
     template:
       ......
       spec:
         tolerations:
           - key: "key1"
             operator: "Equal"
             value: "value1"
             effect: "NoSchedule"
         ......
         containers:
           ......
   ```
   

2. Run the following command again to verify the LogCollector status. If the status is Running, it means LogCollector is installed properly.

   ```shell
   kubectl -n tls-log  get pods  | grep log-collector
   ```
