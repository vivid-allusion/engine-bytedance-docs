---
title: "Best practices for cloud disk persistent storage"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/EBS-persistent-storage-best-practices"
---

This topic describes how to achieve cloud disk persistent storage through VKE by dynamically creating PVs.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenario

Typically, Deployments are used to deploy stateless services, and StatefulSets are used to deploy stateful services. This topic mainly describes how to achieve persistent data storage by mounting stateful services to EBS. StatefulSets are used in the following scenarios:


* **Stable deployment order**: Pods are sequentially deployed or scaled out based on a defined order (such as from 0 to N). Before a pod can be launched, all its preceding pods must be in the Running and Ready state.

* **Stable scale\-in order**: Pods are sequentially scaled in or deleted based on a defined order (such as from N to 0). Before a pod stops execution, all its preceding pods must be deleted.

* **Stable ID**: After a pod is rescheduled, its PodName and HostName remain unchanged.

* **Persistent storage**: With PVC, a pod can still access the same persistent data after being rescheduled.


Storage for pods managed by a StatefulSet must be dynamically provisioned through a StorageClass. A PVC that corresponds to a pod is created based on the VolumeClaimTemplate defined in a StatefulSet, and the PVC automatically creates a PV by using a StorageClass and mounts the PV to the pod. Therefore, you need to create a StorageClass first to adopt the dynamic creation mode.

<span id=".5LqR55uY57G75Z6L"></span>
## Background information

<span id=".5LqR55uY57G75Z6L"></span>
### Cloud disk type

Cloud disks, which are also known as EBS, are categorized into system volumes and data volumes based on usage.


* **System volume**: A system volume is used to store the operating system, which can only be created with an instance, and its life cycle is the same as the mounted ECS instance.

* **Data volume**: A data volume is used to store application data, which applies to I/O\-intensive applications, relational databases, NoSQL databases, development and testing, and other scenarios. You can mount a data volume when or after an ECS instance is created.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed descriptions of EBS specifications, see <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specifications">EBS specifications</a>.   </div>
   

<span id="LkhlTD7f"></span>
### PVs

The following content briefly introduces the resource types involved in creating PVs and the differences between dynamic and static PVs.


* A PVC is an abstract PV type in Kubernetes. It defines the expression of a data volume for a specific storage type, which can be consumed by the application layer and can be associated with a specific PV.

* A PV is a volume of a specific storage type in Kubernetes. A PV defines the specific storage type and volume parameters, and Kubernetes performs storage mounting by referencing the storage information in the PV.


In terms of storage consumption, the application layer declares a storage requirement (PVC) during use. Kubernetes then selects a PV that best matches the PVC requirement and binds it to the PVC. PVs are categorized into dynamic PVs and static PVs based on the creation method.


* Static PVs: PVs manually created by administrators.

* Dynamic PVs: PVs that are automatically created by the provisioner plug\-in. The provisioner plug\-in is a registered plug\-in that is used to create PVs.


<span id="rSUAw87e"></span>
#### Static PVs

Static PVs are typically provisioned by cluster administrators, who plan the storage media in advance based on the storage requirements of the cluster and create the corresponding PVs for consumption by PVCs. If a PVC requirement is defined in a workload, Kubernetes will bind the PVC to a matched PV based on related rules, which enables the application to access storage services.

<span id="scd6gn8z"></span>
#### Dynamic PVs

After a cluster administrator configures a storage resource pool and creates a StorageClass, when a PVC needs to consume a PV, the provisioner plug\-in dynamically creates a PV based on the requirements defined in the PVC and the storage template information defined in the StorageClass.

<span id="3b5PExFZ"></span>
#### Differences between static and dynamic PVs

The difference between dynamic PVs and static PVs lies in that dynamic PVs are automatically created by the plug\-in, and static PVs are manually created by cluster administrators.

Advantages of dynamic PVs:


* Support automatic life cycle management of PVs, for which creation and deletion are performed by add\-ons.

* Reduce configuration complexity and the operation and maintenance workload for system administrators.

* Ensure better storage capacity planning.


<span id="YrUpG0lI"></span>
### Selection of PV binding mode

When you define a StorageClass, you can select a binding mode for PVs, including


|Binding mode |Description |
|---|---|
|Immediate |Create now |
|WaitForFirstConsumer |Delayed creation |


In the following example, the `volumeBindingMode` field in the YAML file is used to define the binding mode for dynamically created PVs. `WaitForFirstConsume` indicates that creation is delayed until a pod that uses the corresponding PVC is created.

```yaml
allowVolumeExpansion: true
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-ssd
parameters:
  ChargeType: PostPaid
  type: ESSD_PL0
provisioner: ebs.csi.volcengine.com
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
```


<span id="myXJzQab"></span>
#### Immediate binding mode

When a user creates a PVC, the cluster searches for a suitable PV to bind. If no suitable PV is found, a PV will be automatically created.


1. If the newly created PVC specifies a StorageClass name, the provisioner plug\-in that corresponds to the StorageClass will automatically create a PV.

2. The provisioner plug\-in creates a PV based on the parameters defined in the PVC and the StorageClass.

3. The provisioner plug\-in creates a data volume in the storage resource pool and then creates a PV by using the data volume information.

4. After the PV is created, it is bound to the PVC.


In summary, if a StorageClass defines the immediate binding mode for binding PVs and PVCs, when a PVC is created, it will be immediately bound to an existing suitable PV. If no suitable PV is available, a new suitable PV will be immediately created for binding.

<span id="Gam0UF1K"></span>
#### WaitForFirstConsumer binding mode

After a user creates a PVC, the PVC will not be immediately bound to a PV until it is consumed by a pod. The binding process is as follows:


1. When a pod is created and consumes this PVC, the system detects that the PVC uses delayed binding.

2. The scheduler continues scheduling and synchronizes the scheduling results to both the metadata of the PVC.

3. The provisioner plug\-in detects that scheduling information is written into the PVC and determines details related to the target storage, such as the node and the availability zone, based on the scheduling information.

4. Trigger PV creation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you mount a cloud disk, a restriction exists based on the availability zone. Only cloud disks and nodes in the same availability zone can be mounted. This restriction may lead to the following issues during use.</div>



* <div data-tips="true" data-tips-type="tip">A cloud disk is created in Availability Zone A. However, node resources in Availability Zone A are insufficient. In this case, pods starting on nodes in Availability Zone B cannot mount the cloud disk.</div>


* <div data-tips="true" data-tips-type="tip">When multiple availability zones exist, users find it hard to assess and plan the appropriate number of PVs for each availability zone in advance.</div>



When multiple availability zones exist, you can use the `WaitForFirstConsumer` binding mode to prevent the preceding issues. When a user creates a PVC, the provisioner plug\-in will no longer immediately bind it to a PV or create a PV. Instead, it will wait until the PVC is consumed by a pod before performing the creation process. In this mode, when a pod is started, it is first scheduled to a node. After the location of the pod is confirmed, a PV and cloud disk are created based on the availability zone information of the pod. This ensures that both the node running the pod and the cloud disk are in the same availability zone. Therefore, in a cluster environment with multiple availability zones, we recommend that you use the `WaitForFirstConsumer` binding mode.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

The following content introduces the proven practices of VKE. To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this topic or on the recommended resources. If you want to use another solution, consult your account manager.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* A cloud disk can be mounted to ECS instances only in the same availability zone. After you create a cloud disk, you cannot change its availability zone. Carefully select the availability zone when you create the cloud disk.

* The number of cloud disks that can be mounted to a single ECS instance is limited. The capacity limits and performance levels of each cloud disk vary based on its type. Select an appropriate instance type and cloud disk type based on your business requirements.

   
   |Item |Restrictions |
   |---|---|
   |Maximum number of cloud disks that can be mounted to a single ECS instance |The number of cloud disks that can be mounted varies based on the instance type. For more details, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |
   |Capacity of a single system volume |ESSD: 40 GiB to 500 GiB |
   |Capacity of a single data volume |ESSD: 20 GiB to 32,768 GiB |
   |Whether the ECS instance of the local disk supports mounting new local disks |Not supported. Local disks are created and destroyed together with ECS instances. |
   |Maximum usage for a single cloud disk type |For each cloud disk type, each account can use up to 64 TiB of capacity in each region.<br><br>To increase the quota, you can [submit a ticket](https://console.byteplus.com/workorder/create). |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a2Y5YKo57G7"></span>
### Step 1: Create a StorageClass


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of VKE console, click **Cluster**.

3. Click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Storage\> StorageClass**.

5. Click **Create StorageClass**. Enter the StorageClass name, select the StorageClass type, availability zone, reclaim policy, binding mode, and other information, and then click **Confirm** to create the StorageClass.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this operation guide, select EBS as the StorageClass type. If you want to use the file storage type, see <a href="https://docs.byteplus.com/en/docs/vke/NAS-persistent-storage-best-practices">Best practices for NAS persistent storage</a>.   </div>
   

<span id=".5q2l6aqk5LqM77ya5Yib5bu65pyJ54q25oCB5bel5L2c6LSf6L29"></span>
### Step 2: Create a StatefulSet

You can create a workload by using the console or a YAML file.

<span id=".5L2_55So5o6n5Yi25Y-w5Yib5bu65bel5L2c6LSf6L29"></span>
#### Configuring through the console


1. In the left navigation bar of the cluster management page, click **Workload** \> **StatefulSet**. On the StatefulSet page, click **Create StatefulSet**.

2. Enter the StatefulSet name, namespace, number of instances, and other information, and then click **Next: Container configuration** to configure the container.

3. Specify the basic information about the container.

4. Specify the storage information about the container based on the following figure. Click **Next: Advanced configuration** to go to the next step.

5. Configure the headless service, instance configuration, scheduling policy, and other information based on the following figure.

6. Click **Confirm**.


<span id=".5L2_55SoLXlhbWwt5paH5Lu25Yib5bu65bel5L2c6LSf6L29"></span>
#### Create a StatefulSet by using YAML

The following sample code shows how to create a workload by using a YAML file.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: headless-svc-web
  namespace: default
spec:
  clusterIP: None
  clusterIPs:
  - None
  ports:
  - name: headless-service-port-0
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: web
  sessionAffinity: None
  type: ClusterIP
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
  namespace: default
spec:
  podManagementPolicy: OrderedReady 
  replicas: 2
  selector:
    matchLabels:
      app: web
  serviceName: headless-svc-web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - image: cr-demo-cn-beijing.cr.volces.com/xxxx/hg-web-test:v2.0
        name: web
        ports:
        - containerPort: 80
          protocol: TCP
        volumeMounts:
        - mountPath: /test
          name: ssd
  volumeClaimTemplates:
  - apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      creationTimestamp: null
      name: ssd
      namespace: default
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 20Gi 
      storageClassName: ebs-ssd 
      volumeMode: Filesystem
```


<span id=".5q2l6aqk5LiJ77ya6aqM6K-B5oyB5LmF5YyW5a2Y5YKo5pyJ5pWI5oCn"></span>
## Validating results

<span id="CM4hHaMA"></span>
### Whether PVCs can scale out synchronously with pods


1. In the left navigation bar of the cluster management page, click **Workload** \> **StatefulSet**.

2. Click the name of the StatefulSet to go to the details page. In the instance list, you can see that web\-0 and web\-1 pods are running.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolumeClaim**. You can see two PVCs are generated: ssd\-web\-0 and ssd\-web\-1.

4. Click **Workload \> StatefulSet** in the left navigation bar. On the page that appears, find the target workload and click  **... \> Update number of instances** in the **Actions** column to change the number of instances from 2 to 3.

5. After the number of instances is updated, view the details of the workload. You can see that the number of pods has increased to 3.

6. On the **Storage \> PersistentVolumeClaim** page, you can see that PVCs have synchronously increased to 3. This indicates that the PVC can scale out synchronously with the pod.


<span id="khnldSFj"></span>
### Whether PVCs remain unchanged after pods are deleted 


1. On the **Workload \> StatefulSet** page, change the number of instances for the target StatefulSet from 3 to 0.

2. View the details of the workload. You can see that the number of pods has gradually decreased to 0.

3. On the **Storage \> PersistentVolumeClaim** page, you can see that all PVCs still exist after all pods are deleted.

4. On the **Workload \> StatefulSet** page, change the number of instances for the target StatefulSet from 0 to 3. You can see that the number of pods gradually increases to 3, and the pod names remain unchanged.

5. On the details page of a pod, view the storage information about the pod. You can see that the corresponding PVC has been remounted.


<span id="DtwjZ3hb"></span>
### Verify persistent storage


1. Run the following command in kubectl to view the files under the `/test` path.

   ```bash
   kubectl exec web-0 ls /test
   ```
   

   Expected output:

   ```bash
   lost+found
   ```
   

2. Run the following command to create a file named `test` under the `/test` path.

   ```bash
   kubectl exec web-0 touch /test/test
   ```
   

3. Run the following command to view the files under the `/test` path.

   ```bash
   kubectl exec web-0 ls /test
   ```
   

   Expected output:

   ```bash
   lost+found
   test
   ```
   

4. Run the following command to delete the pod named `web-0`.

   ```bash
   kubectl delete pod web-0
   ```
   

   Expected output:

   ```bash
   pod "web-0" deleted
   ```
   

5. Run the following command to view the files under the `/test` path.

   ```bash
   kubectl exec web-0 ls /test
   ```
   

   Expected output:

   ```bash
   lost+found
   test
   ```
   

6. The `test` file still exists after the pod is deleted, which indicates that the data in the cloud disk can be persistently saved.
