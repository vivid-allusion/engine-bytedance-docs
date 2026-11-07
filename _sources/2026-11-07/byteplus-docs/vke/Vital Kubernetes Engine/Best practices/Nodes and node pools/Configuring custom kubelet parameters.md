---
title: "Configuring custom kubelet parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Custom_cluster_kubelet_parameter"
---

The kubelet provides a set of parameter configurations to define and adjust node behavior. This topic describes how to configure kubelet parameters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VKE supports configuring common kubelet parameters for nodes via the console, allowing you to modify parameters for both newly added nodes and existing nodes within a node pool. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Configuring kubelet parameters</a>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5LuA5LmI5pivLWt1YmVsZXQ="></span>
### What is kubelet?

In a Kubernetes cluster, kubelet is a critical component that runs on every node. It reports detailed node information to the control plane and manages the container lifecycle and node resources according to instructions from the control plane. Its core responsibilities include:


* **Container lifecycle management**. The kubelet starts containers, stops containers, and maintains the running state of containers based on the PodSpec (pod description) received from the API Server. It ensures containers operate in line with user\-defined specifications.

* **Health check**. The kubelet regularly performs health checks on containers to ensure that applications are running properly. If a check fails, the kubelet can restart the container to maintain application stability and availability.

* **Resource management**. The kubelet manages node resource usage, such as CPU and memory. It ensures each container gets the resources it needs while preventing over\-allocation.

* **Node status reporting**. The kubelet regularly reports the status of its hosting node to the Kubernetes control plane, including resource utilization and running containers. This helps the Kubernetes scheduler make better scheduling decisions.


<span id=".a3ViZWxldC3mm7TmlLnljp_liJk="></span>
### Principles for changing kubelet parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To meet the needs of large\-scale scenarios, VKE has enhanced the functionality and stability of the kubelet on nodes. We recommend using the default kubelet parameters directly.</div>


Changing the default kubelet parameters in a VKE cluster requires a deep understanding of Kubernetes clusters and workloads. Before changing any default settings, make sure to fully understand the purpose of each parameter and evaluate the impact of changes through testing. For a detailed description of parameters, see the [official documentation](https://kubernetes.io/zh-cn/docs/reference/command-line-tools-reference/kubelet/).

For example, in the following scenarios, you may need to modify default kubelet parameters:


* **Resource limiting**. If a node has specific resource limits or special resource requirements, you need to adjust parameters related to resource management. For example, use `--max-pods` to control the maximum number of pods per node.

* **Custom scheduling**. To run specific workloads on particular nodes, you need to adjust kubelet labels or taints. For example, use `--node-labels` to add custom labels to nodes.

* **Specific performance optimization**. To optimize performance for specific workloads, especially those with particular hardware requirements, such as applications for high performance computing, artificial intelligence, machine learning, or data science, you many need to adjust advanced parameters. For example, use `--topology-manager-policy` to specify the behavior of the Topology Manager.


<span id=".5pON5L2c5YmN6aG755-l"></span>
## Notes

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Modifying kubelet parameters for a cluster may cause instability in the cluster and services. Before making any changes, be sure to read this section carefully and exercise caution.</div>


* <div data-tips="true" data-tips-type="danger">We recommend using the console to configure common kubelet parameters for nodes. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Configuring kubelet parameters for a node pool</a>.</div>



When modifying node kubelet parameters, take note of the following information:


* This operation may cause cluster instability. Potential consequences include (but are not limited to) nodes entering the NotReady state, containers running on the node restarting, or containers being evicted. Before modifying any parameters, fully understand their purpose and validate changes in a test environment first.

* If you have multiple environments (such as test, pre\-release, and production), validate parameter changes in the test environment first.  After successful validation, proceed to the next environment. Repeat this process until you apply changes to the production environment.


When scaling out nodes in a VKE cluster, the kubelet system configuration is initialized during node installation according to the node specification and feature settings. This system configuration is saved in the `/var/lib/kubelet/kubeadm-flags.env` file of the node. The configuration file contains the following parameters:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During node upgrade, parameters are overwritten based on this file. Do not directly modify this file or the related parameters.</div>



|Parameter |Description |
|---|---|
|eviction\-hard |Hard eviction threshold. |
|kube\-reserved |Resource reservation configuration for the Kubernetes node. |
|max\-pods |Maximum number of pods per node. |
|system\-reserved |System reserved resource configuration. |
|node\-labels |Labels assigned during node initialization. |
|topology\-manager\-policy |Topology management policy. |
|topology\-manager\-scope |Resource granularity for the topology management policy. |
|feature\-gates |Feature gates. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created. The cluster and nodes in the cluster are in the **Running** state.

* The window of time for this operation does not affect your application availability. It is recommended to perform this operation during off\-peak hours.


<span id=".6YCa6L-H5o6n5Yi25Y-w6YWN572u"></span>
## Creating through the console

VKE supports configuring common kubelet parameters for nodes via the console, allowing you to modify parameters for both newly added nodes and existing nodes within a node pool. For details, see [Configuring kubelet parameters](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).

<span id=".6YCa6L-HLWNsaS3phY3nva4="></span>
## Using the CLI

<span id=".6YWN572u5paw5aKe6IqC54K55Y-C5pWw"></span>
### Configuring parameters for new nodes

For kubelet parameters not covered in the console\-based configuration, you can modify them in the cluster kubelet configuration so that new nodes can use these custom parameters.

In the `kube-system` namespace of the cluster, modify the KubeletConfiguration content in the ConfigMap named `kubelet-config`. After modification is complete, new nodes in the cluster can use the new configuration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Changing cluster parameters will not change kubelet parameter settings for existing nodes, even after a restart. If you need to modify parameter settings for existing nodes, see <a href="https://docs.byteplus.com/en/docs/vke/Custom_cluster_kubelet_parameter#.5L-u5pS55a2Y6YeP6IqC54K55Y-C5pWw">Modifying parameters for existing nodes</a>.</div>


* <div data-tips="true" data-tips-type="tip">If the control plane of the cluster is upgraded later (including a Kubernetes minor version upgrade), parameter incompatibility may occur. After the control plane upgrade completes, you must reconfigure the custom parameters in the <code>kubelet-config</code> ConfigMap to ensure new nodes added to the cluster use your desired custom configuration. For information about cluster upgrade, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Upgrading clusters</a>.</div>



```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: kubelet-config
  namespace: kube-system
data:
  kubelet: |
    apiVersion: kubelet.config.k8s.io/v1beta1
    kind: KubeletConfiguration
    address: 0.0.0.0
    authentication:
      anonymous:
        enabled: false
      webhook:
        cacheTTL: 2m0s
        enabled: true
      x509: {}
    authorization:
      mode: Webhook
      webhook:
        cacheAuthorizedTTL: 5m0s
        cacheUnauthorizedTTL: 30s
    cgroupDriver: cgroupfs
    cgroupsPerQOS: true
    clusterDNS:
    - 172.31.0.10
    clusterDomain: cluster.local
    configMapAndSecretChangeDetectionStrategy: Watch
    containerLogMaxFiles: 5
    containerLogMaxSize: 100Mi
    contentType: application/vnd.kubernetes.protobuf
    cpuCFSQuota: true
    cpuCFSQuotaPeriod: 100ms
    cpuManagerPolicy: none
    cpuManagerReconcilePeriod: 10s
    enableControllerAttachDetach: true
    enableDebuggingHandlers: true
    enableServer: true
    enableSystemLogHandler: true
    enforceNodeAllocatable:
    - pods
    eventBurst: 10
    eventRecordQPS: 5
    evictionHard:
      imagefs.available: 15%
      memory.available: 100Mi
      nodefs.available: 10%
      nodefs.inodesFree: 5%
    evictionPressureTransitionPeriod: 5m0s
    failSwapOn: true
    fileCheckFrequency: 20s
    hairpinMode: promiscuous-bridge
    healthzBindAddress: 127.0.0.1
    healthzPort: 10248
    httpCheckFrequency: 20s
    imageGCHighThresholdPercent: 85
    imageGCLowThresholdPercent: 80
    imageMinimumGCAge: 2m0s
    iptablesDropBit: 15
    iptablesMasqueradeBit: 14
    kubeAPIBurst: 10
    kubeAPIQPS: 5
    kubeReserved:
      cpu: 100m
      memory: 500Mi
    logging:
      format: text
    makeIPTablesUtilChains: true
    maxOpenFiles: 1000000
    maxPods: 0
    nodeLeaseDurationSeconds: 40
    nodeStatusMaxImages: 50
    nodeStatusReportFrequency: 5m0s
    nodeStatusUpdateFrequency: 10s
    oomScoreAdj: -999
    podPidsLimit: -1
    port: 10250
    registryBurst: 5
    registryPullQPS: 2
    resolvConf: /etc/resolv.conf
    rotateCertificates: true
    runtimeRequestTimeout: 2m0s
    serializeImagePulls: true
    shutdownGracePeriod: 0s
    shutdownGracePeriodCriticalPods: 0s
    staticPodPath: /etc/kubernetes/manifests
    streamingConnectionIdleTimeout: 4h0m0s
    syncFrequency: 1m0s
    systemReserved:
      cpu: 100m
      memory: 500Mi
    tlsCertFile: /etc/kubernetes/pki/kubelet-tls.crt
    tlsPrivateKeyFile: /etc/kubernetes/pki/kubelet-tls.key
    topologyManagerPolicy: none
    topologyManagerScope: container
    volumePluginDir: /usr/libexec/kubernetes/kubelet-plugins/volume/exec/
    volumeStatsAggPeriod: 1m0s
```


<span id=".5L-u5pS55a2Y6YeP6IqC54K55Y-C5pWw"></span>
### Modifying parameters for existing nodes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To simplify modifications of parameters on existing nodes, use the console to configure common kubelet settings. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Configuring kubelet parameters</a>.</div>


For kubelet parameters not covered in the console\-based configuration, you can modify them on an existing node by using the steps below:


1. Use kubectl to connect the clusters. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to safely drain the workloads from the target node and prohibit new workloads from being scheduled onto the node. In the command, `${node-name}` is the node name.


```bash
kubectl drain ${node-name} --ignore-daemonsets
```



3. Log in to the node and run the following command to back up the kubelet configuration file.


```bash
cp /var/lib/kubelet/config.yaml  /var/lib/kubelet/config.yaml_bak
```



4. Modify the parameter configuration in the configuration file `/var/lib/kubelet/config.yaml` as needed. For example, to enable serialized image pulls for kubelet, change the value of the `serializeImagePulls` parameter to `true`.


```bash
vim  /var/lib/kubelet/config.yaml
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_147b8c4f2cda17656d2269bea7e36480.png) </span>

5. Run the following command to restart the kubelet service.

```bash
systemctl daemon-reload 
systemctl restart kubelet
```



6. After the service restarts, run the following command to restore node scheduling. In the command, `${node-name}` is the node name.


```bash
kubectl uncordon ${node-name}
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results


1. Use kubectl to connect the clusters. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Verify whether the kubelet parameters take effect.

   1. Run the following command to confirm the node name.

   ```bash
   kubectl get node -o wide 
   ```
   

   2. Start the proxy on the node.

   ```bash
   kubectl proxy
   ```
   

   3. Open a new terminal window and run the following command to directly access kube\-apiserver and obtain the active kubelet configuration. In the command, `${node-name}` is the node name.

   ```bash
   curl -sSL http://127.0.0.1:8001/api/v1/nodes/${node-name}/proxy/configz |jq
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4e869d21e6475bf335633364ecfb43c1.png) </span>
