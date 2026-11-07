---
title: "Managing VCI image caches by using CRD"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_CRD_to_manage_VCI_image_cache"
---

This topic describes how to create and manage VCI image caches by using CustomResourceDefinition (CRD) resources in Kubernetes.

## Prerequisites

* A cluster for VCI applications has been created. For detailed operations, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The cluster where your VCI application resides has been connected using kubectl. For details, see [Connecting to clusters via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The container image required to create the VCI has been prepared. You can use images from BytePlus CR as well as images from third\-party container registries. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

## Create a VCI image cache based on ImageCache

1. Create a custom resource ImageCache that will be used to create the VCI image cache. The following `imagecache-test.yaml` file serves as an example:

   ```YAML
   apiVersion: vci.volcengine.com/v1beta1
   kind: ImageCache
   metadata:
     name: imagecache-test  # Specify the name of the ImageCache. The name must be unique within the cluster.
   spec:
     images:                  # List of container images required to create the image cache.
     - cr-cn-beijing.volces.com/vke/centos:v1
     - cr-cn-beijing.volces.com/vke/busybox:v1
     imagePullSecrets:        # List of CR access credential Secrets. If not configured, a temporary key will be obtained.
     - default:secret1
     subnetIds:               # List of IDs of subnets to which the image cache belongs.
     - subnet-3rf6vwb******
     - subnet-7s89a78******
     securityGroupIds:        # List of IDs of security groups to which the image cache belongs.
     - sg-2byy13cns******
     - sg-ds89xas98******
     retentionDays: 7         # Image cache retention duration. Unit: days. An expired image cache will be cleared.
     volume:
       imageCacheSize: 40   # Size of the image cache. Unit: GiB.
       prewarmZoneIds:  # The warm-up policy configurations of the EBS snapshots that correspond to the image cache. Specify the availability zone for the snapshot to be warmed up.
       - cn-beijing-b
       - cn-beijing-c
       prewarmRetentionDays: 90 # The warm-up retention duration for the EBS snapshots that correspond to the image cache. Unit: day(s). Value range: 1–180.
   ```

2. Run the following command to create the ImageCache.

   ```Bash
   kubectl create -f imagecache-test.yaml
   ```

## Associating an existing VCI image cache by using ImageCache

1. Create a custom resource ImageCache and associate it with an existing VCI image cache. The following `imagecache-exist.yaml` file serves as an example:

   ```YAML
   apiVersion: vci.volcengine.com/v1beta1
   kind: ImageCache
   metadata:
     name: imagecache-exist # Specify the name of the ImageCache. The name must be unique within the cluster.
   spec: 
     appointedImageCacheId: imc-****** # The ID of the existing image cache.
     securityGroupIds: # List of security group IDs for the network of the image cache.
     - sg-2byy13cns******
     subnetIds:        # List of IDs of subnets to which the image cache belongs.
     - subnet-3rf6vwb******
     - subnet-7s89a78******
   ```

2. Run the following command to create the ImageCache.

   ```Bash
   kubectl create -f imagecache-exist.yaml
   ```

## Querying ImageCache status and latest details

After a VCI image cache is created, the ImageCache Controller will obtain the latest information of the image cache and synchronize it to the description of the ImageCache. You can run the `get ImageCache` command to get the latest status and information of the image cache.

> **tip**

* > The status of the image cache after creation will be written back to the `status` field of the corresponding ImageCache custom resource.

* > If the image cache information is updated via the [UpdateImageCache](https://docs.byteplus.com/en/docs/vke/UpdateImageCache) API, the information of the corresponding ImageCache resource will also be refreshed.

* > When the image cache is deleted or cleaned up, the status of the custom resource object is updated. The custom resource object is not deleted.

The following content provides an example of the custom resource ImageCache.

```YAML
apiVersion: vci.volcengine.com/v1beta1
kind: ImageCache
metadata:
  name: imagecache-test  # Name of the ImageCache.
spec:
  images:                  # List of container images required to create the image cache.
  - cr-cn-beijing.volces.com/vke/centos:v1
  - cr-cn-beijing.volces.com/vke/busybox:v1
  imagePullSecrets:        # List of CR access credential secrets.
  - default:secret1
  subnetIds:               # List of IDs of subnets to which the image cache belongs.
  - subnet-3rf6vwb******
  - subnet-7s89a78******
  securityGroupIds:        # List of IDs of security groups for the network of the image cache.
  - sg-2byy13cns******
  - sg-ds89xas98******
  retentionDays: 7         # Image cache retention duration. Unit: days. An expired image cache will be cleared.
  volume:
    imageCacheSize: 40   # Size of the image cache. Unit: GiB.
    prewarmZoneIds:  # EBS snapshot warm-up policy configuration for the image cache (the availability zone of the snapshot).
    - cn-beijing-b
    - cn-beijing-c
    prewarmRetentionDays: 90 # The warm-up retention duration for the EBS snapshots that correspond to the image cache. Unit: days.
status:
  images:
    previous: # Image information configured in .spec last time, used for comparison with the current .spec.
    - cr-cn-beijing.volces.com/vke/centos:v1
    - cr-cn-beijing.volces.com/vke/busybox:v1
    latest:  # Latest image information synchronized based on EventRuleRecords.
    - cr-cn-shanghai.volces.com/vke/centos:v2
    - cr-cn-shanghai.volces.com/busybox:v2
  imageCacheName: imagecache-test-******
  imageCacheId: *********  # Image cache ID.
  creationTime: 2024-04-16T20:33:54Z    # Creation time of the image cache.
  updateTime: 2024-04-16T20:33:54Z      # Time when the image cache was last updated.
  expireDateTime: 2024-07-16T20:33:54Z  # The time when the image cache expires.
  lastMatchedTime: 2024-04-16T21:23:54Z # Time when the image cache was last matched.
  phase: Ready                          # Image cache status information.
  conditions:
  - lastTransitionTime: "2024-04-16T20:33:54Z"
    message: instance imc-3vknvu66783****** has been ready
    reason: ImageCacheHasBeenReady
    status: "True"
    type: ImageCacheReady
  - lastTransitionTime: "2024-04-16T20:33:54Z"
    message: "instance {imc-******} is in progress"
    reason: CreateImageCacheRequestSuccess
    status: "True"
    type: CreationInProgress
```

## Deleting VCI image caches via ImageCache

When you delete the ImageCache resource using the `delete` command, the ImageCache Controller will also delete the corresponding VCI image cache.

The following example command deletes a resource ImageCache named `imagecache-test`. After the command is executed, the VCI image cache corresponding to `imagecache-test` will be deleted.

```Bash
kubectl delete imc imagecache-test
```

## Updating VCI image caches via ImageCache

When you update an ImageCache resource, the ImageCache Controller will also update the corresponding VCI image cache.

> **tip**

* > When the status of the image cache is `Ready`, you must modify the `images` field (other fields can also be modified) to trigger the image cache update.

* > When the status of the image cache is `Failed`, modifying any updatable field in the YAML below will trigger an image cache update.

For a list of fields that support updates, see the comments in the YAML file below (except for fields with the comment **It cannot be updated**, all other fields with comments support updates).

```YAML
apiVersion: vci.volcengine.com/v1beta1
kind: ImageCache
metadata:
  name: imagecache-test  # Name of the ImageCache. It cannot be updated.
spec:
  images:                  # List of container images required to create the image cache.
  - cr-cn-beijing.volces.com/vke/centos:v1
  - cr-cn-beijing.volces.com/vke/busybox:v1
  imagePullSecrets:        # List of container registry access credentials. If no credentials are provided, temporary credentials will be obtained.
  - default:secret1
  subnetIds:               # List of IDs of subnets to which the image cache belongs.
  - subnet-3rf6vwbgkg****
  - subnet-7s89a78xaa****
  securityGroupIds:        # List of IDs of security groups for the network of the image cache.
  - sg-2byy13cnsczy****
  - sg-ds89xas98sa9****
  retentionDays: 7         # Image cache retention duration. Unit: days. It cannot be updated.
  volume:
    imageCacheSize: 40   # Size of the image cache. Unit: GiB.
    prewarmZoneIds:  # EBS snapshot warm-up policy configuration for the image cache. Specify the availability zone for the snapshot to be warmed up.
    - cn-beijing-b
    - cn-beijing-c
    prewarmRetentionDays: 90 # The warm-up retention duration for the EBS snapshots that correspond to the image cache. Unit: day(s). Value range: 1–180.
```

## Automatically updating VCI image caches based on event notifications

When creating an ImageCache corresponding to a VCI image cache, you can configure CR event notification rules to enable automatic updates of the VCI image cache based on event notifications.

1. Create an ImageCache corresponding to the VCI image cache and configure CR event notification rules. The following `imagecache-test.yaml` file serves as an example:

   ```YAML
   apiVersion: vci.volcengine.com/v1beta1
   kind: ImageCache
   metadata:
     name: imagecache-test  # Specify the name of the ImageCache. The name must be unique within the cluster.
   spec:
     eventRule: # Create CR event notification rules.
       strategy: update  # Strategy in case of a match. Values include update and new, indicating an image cache update and creation, respectively.
       registry: "helm-cr"  # CR instance name. Only Standard Edition instances are supported.
       namespaces:  # List of namespaces within the CR instance.
       - vke
       images:  # List of images within the namespace.
       - centos 
       - busybox
       tag: ".*"  # Rule scope. Regular expressions are supported.
       enabled: true  # Whether to enable eventRule. Values: true (enabled) and false (disabled).
     images:  # List of container images required to create the image cache.
     - cr-cn-beijing.volces.com/vke/centos:v1
     - cr-cn-beijing.volces.com/vke/busybox:v1
     imagePullSecrets:  # List of container registry access credentials. If no credentials are provided, temporary credentials will be obtained.
     - default:secret1
     subnetIds:  # List of IDs of subnets to which the image cache belongs.
     - subnet-3rf6vwb******
     - subnet-7s89a78******
     securityGroupIds:  # List of IDs of security groups for the network of the image cache.
     - sg-2byy13cns******
     - sg-ds89xas98******
     retentionDays: 7  # Image cache retention duration. Unit: days. An expired image cache will be cleared.
     volume:
       imageCacheSize: 40  # Size of the image cache. Unit: GiB.
       prewarmZoneIds:  # EBS snapshot warm-up policy configuration for the image cache. Specify the availability zone for the snapshot to be warmed up.
       - cn-beijing-b
       - cn-beijing-c
       prewarmRetentionDays: 90  # The warm-up retention duration for the EBS snapshots that correspond to the image cache. Unit: day(s). Value range: 1–180.
   ```

2. Run the following command to create the ImageCache.

   ```Bash
   kubectl create -f imagecache-test.yaml
   ```

   The following sample code provides an example of the `status` field returned when you query the ImageCache containing CR event notification rules. For information about how to query the information, see [Querying ImageCache status and latest details](https://docs.byteplus.com/en/docs/vke/Using_CRD_to_manage_VCI_image_cache#.5p-l6K-iLWltYWdlY2FjaGUt55qE54q25oCB5ZKM5pyA5paw5L-h5oGv).

   ```YAML
   status:
     notifications:  # Record EventRuleRecords messages.
     - image: "cr-cn-shanghai.volces.com/vke/centos:v3"
       receviedTimestamp: 2024-05-27T10:33:30Z
       processedTimestamp: 2024-05-27T10:34:30Z
       id: "xx-4"
     - image: "cr-cn-shanghai.volces.com/vke/busybox:v3"
       receviedTimestamp: 2024-05-27T10:33:30Z
       processedTimestamp: 2024-05-27T10:34:30Z
       id: "xx-1"
     eventRuleStatus:
       ruleName: ******  # The name of the CR event notification rule.
       ruleId: "******"  # The ID of the event notification rule.
       updateTime: 2024-05-27T09:23:56Z  # Time of last update on the event notification rule.
       eventRuleHash: "******"
     images:
       previous:  # Image information configured in .spec last time, used for comparison with the current .spec.
       - cr-cn-shanghai.volces.com/vke/centos:v1
       - cr-cn-guilin-boe.cr.volces.com/busybox:v1
       latest:  # Latest image information synchronized based on EventRuleRecords.
       - cr-cn-shanghai.volces.com/vke/centos:v2
       - cr-cn-guilin-boe.cr.volces.com/busybox:v2
     imageCacheName: *********  # Image cache name.
     imageCacheId: *********  # Image cache ID.
     creationTime: 2024-05-27T10:33:30Z     # Creation time of the image cache.
     updateTime: 2024-05-27T10:33:30Z       # Time when the image cache was last updated.
     expireDateTime: 2024-05-27T10:33:30Z   # The time when the image cache expires.
     lastMatchedTime: 2024-05-27T09:33:30Z  # Time when the image cache was last matched.
     phase: Failed  # Image cache status information.
     conditions:
     - lastTransitionTime: "2024-04-16T20:33:54Z"
       message: instance imc-3vknvu667****** has been ready
       reason: ImageCacheHasBeenReady
       status: "True"
       type: ImageCacheReady
     - lastTransitionTime: "2024-04-16T20:33:54Z"
       message: "instance {imc-******} is in progress"
       reason: CreateImageCacheRequestSuccess
       status: "True"
       type: CreationInProgress
   ```
