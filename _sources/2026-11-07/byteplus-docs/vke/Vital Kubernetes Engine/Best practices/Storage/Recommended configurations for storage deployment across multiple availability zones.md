---
title: "Recommended configurations for storage deployment across multiple availability zones"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Recommended_Configuration_for_Multi-Availability_Zone_Storage_Deployment"
---

Optimizing storage deployment across multiple availability zones can minimize interruptions during application release and ensure the continuity of critical business systems and applications when various failures occur. This topic describes the recommended configurations for storage deployment across multiple availability zones.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Kubernetes simplifies the process of distributing and deploying applications. However, the abstraction of the underlying hardware logic makes it hard for users to perceive the specific hardware logic. This may result in unexpected situations and application release interruption. For example, an application is not deployed in the expected availability zones. The disk is invalid when a cloud disk is created. The disk type is not supported when an application is being mounted. A node affinity conflict occurs when an application is being scheduled.

When you deploy storage across multiple availability zones, you can specify availability zones for business deployment. This reduces failures caused by insufficient availability zone resources and minimizes the preceding issues to ensure stable business operations.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

The following content introduces the proven practices of VKE. To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this topic or on the recommended resources. If you want to use another solution, consult your account manager.

<span id=".5o6o6I2Q6YWN572u"></span>
## Recommended configuration

The recommended configurations for storage deployment across multiple availability zones are as follows:


* A cluster includes three availability zones to ensure that node and storage resources meet business requirements.

* Cloud disks are used for persistent storage, which is more stable and provides higher data transmission bandwidth than FileNAS.

* High\-availability cloud disks are used to prevent cloud disk mounting failures and single points of failure.

* When all nodes in the cluster's availability zones are unavailable, immediately provision the matching nodes.

* Make sure that the application can be evenly distributed across all availability zones and nodes.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65YyF5ZCr5LiJ5Liq5Y-v55So5Yy655qE6ZuG576k"></span>
### Step 1: Create a cluster that includes three availability zones

To deploy storage across multiple availability zones, we recommend creating a cluster with three availability zones. This ensures nodes, storage, and application resources are distributed across different zones, improving disaster recovery capability.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click **Create cluster** and specify the required parameters.

   The following content outlines the key configuration items for this example scenario. You need to configure other items as needed. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   
   |Parameters |Descriptions |
   |---|---|
   |VPC |A VPC provides an isolated, self\-configurable, and self\-managed virtual network environment for clusters. In this scenario, we recommend that you select a VPC whose subnet covers multiple availability zones. |
   |Pod subnets |The networks used by pods. To ensure pods are deployed across multiple availability zones, we recommend that you select pod subnets in these zones in this scenario. |
   


<span id=".5q2l6aqk5LqM77ya5qC55o2u5o6o6I2Q6YWN572u5Yib5bu66IqC54K55rGg"></span>
### Step 2: Create node pools based on the recommended configurations

To deploy storage across multiple availability zones, each node is recommended to use a single availability zone. Therefore, when you create a node pool, make sure that each node pool corresponds to a different availability zone. In this scenario, create three availability zones, and each node pool occupies a different availability zone. 


1. In the left navigation bar of the cluster management page, click **Nodes \> Node pool**.

2. Click **Create node pool** in the upper\-left corner of the node pool list. Select an appropriate node pool type based on your business requirements, and then click **Confirm**.

3. On the Create node pool page, specify parameters related to the node pool based on your business requirements.

   The following content outlines the key configuration items for this example scenario. You need to configure other items as needed. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   
   |Parameters |Description |
   |---|---|
   |Autoscaling |Clusters can be automatically scaled based on the scheduling status of pods and the node resource usage in the clusters. In this scenario, we recommend that you enable the autoscaling feature for the node pool. For more detailed information, see [Node autoscaling](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works). |
   |Availability Zone |Availability zones are physically isolated infrastructure units within a single region, featuring independent power and networking systems. Availability zones communicate over internal networks. In this scenario, we recommend that each node pool use an availability zone. |
   |Instance type |In this scenario, we recommend that you use the same type of ECS resources across multiple availability zones, or ECS resources that support the same type of block storage. |
   |System volume/Data volume |In this scenario, we recommend that you select an ESSD cloud disk. For more details, see [Cloud disk specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications). |
   |Node taints |In this scenario, we recommend that you configure taints for all nodes in the node pool to ensure that no unexpected applications are scheduled and impact the current application. |
   


<span id=".5q2l6aqk5LiJ77ya5L2_55So6auY5Y-v55So57G75Z6L55qE5LqR55uY5Yib5bu65a2Y5YKo57G7"></span>
### Step 3: Create a StorageClass by using high\-availability cloud disks

To deploy storage across multiple availability zones, we recommend using a dynamic PV of the cloud disk type.Cloud disk storage offers more stable performance and higher data transmission bandwidth.


1. In the left navigation bar of the cluster management page, click **Storage \> StorageClass**.

2. Click **Create with Yaml**, enter the prepared YAML configuration, and then click **Confirm** to create the StorageClass.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following content provides a standard template for the configurations of a StorageClass. You can modify the configurations based on your business requirements.</div>


```Yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: sc-disk-essd
parameters:
  ChargeType: PostPaid
  type: ESSD_PL0
  zone: cn-beijing-a
provisioner: ebs.csi.volcengine.com
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
```


The following content outlines the key configuration items for this example scenario. You need to configure other items as needed. For details, see [Using EBS dynamic PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes).


|Parameters |Description |
|---|---|
|provisioner |The storage type. In this scenario, ebs.csi.volcengine.com is used, which indicates csi\-ebs storage. |
|parameters |The storage parameters. Different types of storage support different parameters.<br><br><br>* **type**: The type of cloud disk storage. ESSD_PL0 * and *  ESSD_FlexPL are supported. You can select an appropriate type based on your business requirements. ESSD_FlexPL provides additional performance scalability. For detailed configuration and description, see [Creating StorageClasses](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes#.5q2l6aqk5LiA77ya5Yib5bu6LXN0b3JhZ2VjbGFzcw==).<br><br>* **zone**: This parameter is used to select the availability zone to which the EBS cloud disk belongs. In this scenario, we recommend that you restrict the topology used to create the PV to a specific region. |
|reclaimPolicy |The reclaim policy for the cloud disk. It can be Delete or Retain. We recommend that you select Retain to prevent accidental data deletions.<br><br><br>* **Delete**: When you delete the PVC, the PV and cloud disk will also be deleted.<br><br>* **Retain**: When you delete the PVC, the PV and cloud disk will not be deleted. You need to manually delete them. |
|allowVolumeExpansion |Defines whether PVs created by this StorageClass support dynamic scale\-out. In this scenario, we recommend that you set the value to true. |
|volumeBindingMode |Select a binding mode for the cloud disk. The following information is included:<br><br><br>* **Immediate**: Performs PV binding and allocation when the PVC is created.<br><br>* **WaitForFirstConsumer**: Delays PV binding and allocation until a pod that uses the PVC is created. |


<span id=".5q2l6aqk5Zub77ya5Yib5bu65bqU55So5bm25YiG5biD5Zyo5LiN5ZCM5Y-v55So5Yy6"></span>
### Step 4: Create an application and distribute it across different availability zones

To deploy storage across multiple availability zones, we recommend that you distribute an application to nodes in different availability zones to minimize interruptions during application release.


1. In the left navigation bar of the cluster management page, click **Workload \> StatefulSet**.

2. Click **Create with Yaml**, enter the prepared YAML configuration, and then click **Confirm** to create the StatefulSet.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following content provides a standard template for the configurations of a StatefulSet. You can modify the configurations based on your business requirements.</div>


```Yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: nginx
  namespace: default
spec:
  serviceName: "nginx"
  selector:
    matchLabels: 
      app: nginx
  template:
    metadata:
      labels: 
        app: nginx
    spec:
      topologySpreadConstraints:
      - labelSelector:
          matchLabels:
            app: nginx
        maxSkew: 1
        topologyKey: topology.kubernetes.io/zone
        whenUnsatisfiable: ScheduleAnyway
      containers:
      - image: nginx:latest
        name: nginx
        env:
        - name: NGINX_ROOT_PASSWORD
          value: "nginx"
        volumeMounts: 
        - name: disk-csi
          mountPath: /var/lib/nginx
      tolerations:
      - key: "app"
        operator: "Exists"
        effect: "NoSchedule"
  volumeClaimTemplates:
  - metadata:
      name: disk-csi
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: sc-disk-essd
      resources:
        requests:
          storage: 40Gi
```


The following content outlines the key configuration items for this example scenario. You need to configure other items as needed. For details, see [Creating StatefulSets](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet).


|Parameters |Descriptions |
|---|---|
|topologySpreadConstraints |Try to distribute high\-availability pods across different availability zones. For more details, see [Topology Spread Constraints](https://kubernetes.io/zh-cn/docs/concepts/scheduling-eviction/topology-spread-constraints/).<br><br><br>* **labelSelector**: This field is used to find matching pods. Pods matching this label selector are counted to determine the number of pods in the topology domain.<br><br>* **maxSkew**: The value of maxSkew indicates the maximum difference in the number of matched pods between topology domains of the specified topology type. This value is used to measure the unevenness of pod distribution and must be greater than 0.<br><br>* **topologyKey**: The key of the node label. If two nodes use the same key and label value, the scheduler deems these nodes to be in the same topology and attempts to distribute pods evenly across the topology domains.<br><br>* **whenUnsatisfiable**: Specifies how the scheduler handles a pod when the pod does not meet spreading constraints. Valid values: DoNotSchedule and ScheduleAnyway. DoNotSchedule is used by default, which specifies that the pod will not be scheduled. ScheduleAnyway specifies that the pod will still be scheduled, with preference given to nodes that minimize skew. |
|volumeClaimTemplates |Automatically create the corresponding number of cloud disks based on the specified number of replicas to achieve quick scale\-out. |
