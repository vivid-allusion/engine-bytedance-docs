---
title: "Changing cloud disk types"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Changing_cloud_disk_types"
---

VKE supports multiple cloud disk types as storage volumes to meet storage performance and cost requirements in different scenarios. When you use cloud disk volumes, you can change cloud disk types as needed. This topic describes the considerations and procedure for changing cloud disk types.

<span id="7aQ8IwKZ"></span>
## Background

In a VKE cluster, cloud disks are the core storage medium for stateful applications, such as databases and message queues. These applications are highly sensitive to performance metrics such as disk IOPS and throughput. In the past, the performance specifications of a cloud disk were fixed when the disk was created and could not be changed directly. When business growth and increased traffic resulted in insufficient storage performance, you usually had to create a high\-specification cloud disk and migrate data to it. This process causes downtime and involves data migration risks and costs. For periodic traffic spikes, such as major promotions or month\-end settlements, provisioning high\-performance cloud disks for the long term wastes resources during off\-peak hours.

To resolve these issues, VKE provides a solution for changing cloud disk types based on VolumeAttributesClass (VAC). This solution decouples configurations such as cloud disk types and performance specifications from PersistentVolumes (PVs) and abstracts them into an independently adjustable configuration template. You can directly modify parameters such as the type, IOPS, and throughput of a running cloud disk without rebuilding the PV or interrupting services. This solution provides the following core benefits:


* **Online configuration change without service interruption**: When you adjust cloud disk types and performance parameters, you do not need to unmount volumes or restart Pods. Applications can continue to read and write data.

* **Configuration and data decoupling**: Cloud disk types and performance parameters are defined in a VAC. One VAC can be reused by multiple PersistentVolumeClaims (PVCs). To adjust specifications, you only need to modify one configuration, which helps with unified governance.

* **Adapt performance to business cycles**: Temporarily increase performance during peak hours and restore the standard level afterward. This allows storage costs to scale with actual demand and avoids long\-term spending on peak capacity.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about VAC resources, see the <a href="https://kubernetes.io/docs/concepts/storage/volume-attributes-classes/">official documentation</a>.</div>


<span id="n3CoVm2Q"></span>
## Limits


* Only scenarios that use dynamically provisioned cloud disk PVs are supported.

* Currently, only changes between ESSD_PL0 and ESSD_FlexPL specifications are supported. Changes to other cloud disk types are not supported.


<span id="yZ8k1zOC"></span>
## Prerequisites


* You have created a managed cluster and the cluster version is v1.32 or later. If the version does not meet the requirement, upgrade the cluster. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster?lang=en).

   * If the cluster version is v1.32, [submit a ticket](https://console.byteplus.com/workorder/create?step=1&SubProductID=P00000210) to request `feature-gates=VolumeAttributesClass=true` for the cluster.

   * If the cluster version is v1.34 or later, no additional prerequisites are required.

* You have installed the csi\-ebs add\-on and upgraded it to v1.5.0 or later. For details, see [csi-ebs](https://docs.byteplus.com/en/docs/vke/csi-ebs-add-on?lang=en).

* You have created an SC and a PVC and mounted a dynamic cloud disk (EBS) PV. For details, see [Using dynamic PVs of the EBS type](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes?lang=en).


<span id="kBgfIsa8"></span>
## Procedure

<span id="zlcSH7uo"></span>
### Step 1: Enable the cloud disk configuration change feature


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Hover over the csi\-ebs add\-on card, click **Configuration**, and enable the VAC feature. For more information about add\-on parameters, see [csi-ebs](https://docs.byteplus.com/en/docs/vke/csi-ebs-add-on?lang=en).

5. Click **Confirm** to finish configuration.


<span id="mTnDaztz"></span>
### Step 2: Configure a VAC

VACs are configuration templates for different storage types in the cluster. In a VAC configuration, `driverName` and `parameters` cannot be modified after the VAC is created. We recommend creating a separate VAC for each target cloud disk specification and switching configuration templates by updating the PVC.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When you configure a VAC, we recommend including the version and key specification information in the name for easier recognition and use. An example is <code>ebs-flexpl-iops10k-burst-v1</code>.</div>


* <div data-tips="true" data-tips-type="warning">Do not reuse names that are already used. This helps avoid deleting and re\-creating VACs with the same name.</div>


1. Create a YAML file for the VAC. The following `vac-ebs-demo.yaml` file serves as an example:

   ```YAML
   apiVersion: storage.k8s.io/v1
   kind: VolumeAttributesClass
   metadata:
     name: ebs-flexpl-iops10k-burst-v1 # VAC name
   driverName: ebs.csi.volcengine.com # Required. The driver required for storage mount.
   parameters:
     type: ESSD_FlexPL # Required. The EBS volume type and performance level. For ESSD, performance levels ESSD_PL0 and ESSD_FlexPL are supported.
     extraPerformanceTypeId: IOPS # Optional. The extra performance type. Valid values: IOPS, Balance, and Throughput. This field takes effect only when the type is ESSD_FlexPL and the EBS capacity is greater than or equal to 500 GB.
     extraPerformanceIOPS: "10000" # Optional. IOPS in the extra performance configurations. This parameter takes effect only if the extra performance type is IOPS or Balance. The value range is 1 to 50000.
     burstEnabled: "true" # Optional. Whether to enable performance bursting. This field takes effect only if the type is set to ESSD_FlexPL. Valid values: true and false. Default value: false.
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |driverName |The driver required for PV mount. In this topic, you need to set the value to ebs.csi.volcengine.com, which indicates the csi\-ebs add\-on. |
   |type |The volume type. Only ESSD_PL0 and ESSD_FlexPL specifications are supported. |
   |extraPerformanceTypeId |The extra performance type. You can increase volume performance without increasing volume capacity.<br><br>IOPS, Balance, and Throughput are supported. This parameter is required only if the volume type is ESSD_FlexPL and the volume capacity is greater than or equal to 500 GB. For different types of extra performance, see [ESSD FlexPL volumes](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume). |
   |extraPerformanceIOPS |IOPS in the extra performance configurations. This parameter takes effect only if the extra performance type is IOPS or Balance. The value is an integer. Unit: operations per second. The value range is from 1 to 50000. |
   |extraPerformanceThroughputMB |The throughput of the extra performance configurations. This parameter takes effect only if the extra performance type is Throughput. The value is an integer. Unit: MB/s. Valid values: 0 to 650. |
   |burstEnabled |Whether to enable performance bursting for a cloud disk. This allows the cloud disk to deliver I/O performance that exceeds its baseline performance for a short period to handle peak business workloads or bursty traffic. This field takes effect only if the cloud disk type is ESSD_FlexPL. Valid values:<br><br><br>* **true**: Enable performance bursting for the cloud disk.<br><br>* **false**: Disable performance bursting for the cloud disk. This value is used by default.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After you enable the performance bursting feature for ESSD FlexPL cloud disks, you will be charged based on the burst performance usage.</div><br> |
   

2. Run the following command to create the VAC.

   ```Bash
   kubectl apply -f vac-ebs-demo.yaml
   ```
   


<span id="Ke9qLjHG"></span>
### Step 3: Change the PVC configuration


1. Add or modify the VAC configuration in the PVC to specify the required cloud disk type. The following `pvc-ebs-dynamic.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-ebs
     namespace: default
   spec:
     accessModes: 
     - ReadWriteOnce
     volumeAttributesClassName: ebs-flexpl-iops10k-burst-v1 # Add or modify this VAC configuration field to change the cloud disk type and performance parameters.
     resources:
       requests:
         storage: 50Gi
     storageClassName: storage-class-ebs
     volumeMode: Filesystem
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |volumeAttributesClassName |Add or modify this VAC configuration field to specify the cloud disk type, performance parameters, and other settings.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For other parameters in the PVC, see <a href="https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes?lang=en">Using dynamic EBS PVs</a>.</div><br> |
   

2. Run the following command to change the PVC configuration.

   ```Bash
   kubectl apply -f pvc-ebs-dynamic.yaml
   ```
   


<span id="hKGAMgkl"></span>
## Validate results

After the configuration is complete, the system automatically changes the type or parameters of the cloud disk PV. You can also log in to the [EBS console](https://console.byteplus.com/ebs) to view the volume details after the change and confirm whether the change meets your requirements.
