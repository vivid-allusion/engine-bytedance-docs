---
title: "Mount PersistentVolumeClaim to RayCluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Mount_PersistentVolumeClaim_to_RayCluster"
---

<span id="392785cf"></span>
## Feature overview

EMR on VKE supports mounting PersistentVolumeClaim to RayCluster.

<span id="f0e631fe"></span>
## prerequisites


1. An EMR on VKE cluster containing the Ray service has been created.

2. The corresponding storage volume must already be created in the VKE cluster. For detailed steps, see [Create a storage volume](https://www.volcengine.com/docs/6460/101643).


<span id="f5bb0704"></span>
## Create via console

Bind PersistentVolumeClaim when creating RayCluster.

<span id="c94f0d9d"></span>
### Add via form


1. Log in to the [EMR console](https://console.volcengine.com/emr).

2. On the **Service list** page, click **Ray** to enter the Ray service details page.

3. Click the **Add RayCluster** button and select **Add via form**.

4. In the group where PVC needs to be mounted, click the **Settings** button under the corresponding storage configuration.

5. On the pop\-up storage configuration page, click to open the **Storage configuration** option.

6. In the Add volume row, select the corresponding PersistentVolumeClaim and enter a custom volume name.

7. In the Mount volume row, select the volume name entered in the previous step, and configure the mount path and read/write permissions.

8. Click **OK** to complete the configuration.


<span id="4cd81ed1"></span>
### Add via YAML


1. Log in to the [EMR console](https://console.volcengine.com/emr).

2. On the **Service list** page, click the **Ray** service to enter the Ray service details page.

3. Click the **Add RayCluster** button and select **Add via YAML**.

4. Manually add the volumes and volumeMounts configuration in the YAML file.

5. Click **OK** to complete the configuration.


Example of YAML changes:

```YAML
apiVersion: ray.io/v1alpha1
kind: RayCluster
metadata:
  name: example-raycluster
spec:
  headGroupSpec:
    template:
      spec:
        containers:
        - name: ray-head
          volumeMounts:
          - mountPath: /mnt/data
            name: head-v
        volumes:
        - name: head-v
          persistentVolumeClaim:
            claimName: head-pvc
  workerGroupSpecs:
  - groupName: worker-group
    template:
      spec:
        containers:
        - volumeMounts:
          - mountPath: /mnt/data
            name: worker-v
        volumes:
        - name: worker-v
          persistentVolumeClaim:
            claimName: worker-pvc
```


<span id="a32c55a7"></span>
## Create via OpenAPI

Use **AddComponentInstance**, for example:

```JSON
{
    "ApplicationName": "Ray",
    "ComponentName": "RayCluster",
    "InstanceName": "rayclusterName",
    "ClusterId": "emr-xxx",
    "ApplicationConfigs": [
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "replicas",
            "ConfigItemValue": "1",
            "ComponentName": "RayCluster",
            "UnitType": "headgroup",
            "UnitInstanceName": "headgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "head_cpu",
            "ConfigItemValue": "1",
            "ComponentName": "RayCluster",
            "UnitType": "headgroup",
            "UnitInstanceName": "headgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "head_memory",
            "ConfigItemValue": "2Gi",
            "ComponentName": "RayCluster",
            "UnitType": "headgroup",
            "UnitInstanceName": "headgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "head_volumes",
            "ConfigItemValue": "[{\"name\":\"core-site-volume\",\"configMap\":{\"defaultMode\":420,\"name\":\"ray-cluster-core-site\"}},{\"name\":\"head\",\"persistentVolumeClaim\":{\"claimName\":\"testpvc\"}}]",
            "ComponentName": "RayCluster",
            "UnitType": "headgroup",
            "UnitInstanceName": "headgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "head_volumeMounts",
            "ConfigItemValue": "[{\"mountPath\":\"/opt/hadoop/etc/hadoop\",\"name\":\"core-site-volume\"},{\"name\":\"head\",\"mountPath\":\"/opt/head\",\"readOnly\":false}]",
            "ComponentName": "RayCluster",
            "UnitType": "headgroup",
            "UnitInstanceName": "headgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "replicas",
            "ConfigItemValue": "1",
            "ComponentName": "RayCluster",
            "UnitType": "workergroup",
            "UnitInstanceName": "workgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "worker_cpu",
            "ConfigItemValue": "1",
            "ComponentName": "RayCluster",
            "UnitType": "workergroup",
            "UnitInstanceName": "workgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "worker_gpu",
            "ConfigItemValue": "0",
            "ComponentName": "RayCluster",
            "UnitType": "workergroup",
            "UnitInstanceName": "workgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "worker_memory",
            "ConfigItemValue": "1Gi",
            "ComponentName": "RayCluster",
            "UnitType": "workergroup",
            "UnitInstanceName": "workgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "worker_volumes",
            "ConfigItemValue": "[{\"name\":\"core-site-volume\",\"configMap\":{\"defaultMode\":420,\"name\":\"ray-cluster-core-site\"}},{\"name\":\"worker\",\"persistentVolumeClaim\":{\"claimName\":\"testpvc\"}}]",
            "ComponentName": "RayCluster",
            "UnitType": "workergroup",
            "UnitInstanceName": "workgroup"
        },
        {
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "worker_volumeMounts",
            "ConfigItemValue": "[{\"mountPath\":\"/opt/hadoop/etc/hadoop\",\"name\":\"core-site-volume\"},{\"name\":\"worker\",\"mountPath\":\"/opt/worker\",\"readOnly\":false}]",
            "ComponentName": "RayCluster",
            "UnitType": "workergroup",
            "UnitInstanceName": "workgroup"
        },
        {
            "ComponentName": "RayCluster",
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "repository_url",
            "ConfigItemValue": "xxx"
        },
        {
            "ComponentName": "RayCluster",
            "ConfigFileName": "raycluster-values.yaml",
            "ConfigItemKey": "repository_tag",
            "ConfigItemValue": "xxx"
        }
    ]
}
```


<span id="ebfe1df0"></span>
## Manually specify when submitting RayJob


1. In the [Volcano Engine E-MapReduce console](https://console.volcengine.com/emr), click **Job Management \> Job List \> Create Job**.

2. On the **Create Job** page, select **Ray Job** as the job type and select the corresponding cluster.

3. Enable **Storage configuration** and select the corresponding storage volume.

* Add volume: Select an existing storage volume and name it.

* Mount volume: Mount the volume to the specified path in the pod and specify the corresponding read/write permissions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add and mount multiple volumes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cloud disks provided by the Volcano Storage team are non\-shared storage and can only be mounted by one Pod at a time. Only the ReadWriteOnce access mode is supported.   </div>
   

5. Click **Create** to complete the mounting.
