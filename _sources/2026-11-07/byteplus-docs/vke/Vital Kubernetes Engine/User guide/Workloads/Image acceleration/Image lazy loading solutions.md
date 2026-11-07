---
title: "Image lazy loading solutions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution"
---

This topic introduces the image lazy loading capability provided by VKE. This technique reduces the time required to read container image files and enables rapid startup of container applications.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently <strong>available by invitation</strong> only.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The standard container image format is defined by the [OCI Image Format Spec](https://github.com/opencontainers/image-spec). Container image layers are compressed TAR archive files. Before starting a container, the container runtime service or client downloads all layers of the entire container image to the local system. It then decompresses these layers sequentially to provide a Union File System for the container runtime. This process is highly time\-consuming, with latency directly proportional to the image size and layer size differences. However, in certain application scenarios, container applications do not need to read all container image files during the startup phase. For example, container applications may connect to external databases or download dependency files from external storage during startup. These scenarios require container readiness as quickly as possible.

To address this, VKE provides the image lazy loading feature. With lazy loading, containers can become ready within seconds, and startup speed is nearly unaffected by image size.

<span id=".6YCC55So5Zy65pmv"></span>
## Application scenarios

Image lazy loading is applicable to scenarios with the following characteristics:


* The image size is large, and the image content accessed after application startup has obvious local hotspots.

* The time required to pull the container image accounts for a large proportion of the overall container uptime.

* The container image changes frequently.


<span id=".5L2_55So6K-05piO"></span>
## Notes


* Unhit prefetch caches cause I/O delays that slow down your application. To avoid these delays, test if your target container application is compatible with lazy loading in a test environment. Only use it in production after confirming compatibility.

* For large\-scale scaling, we recommend using image lazy loading with P2P acceleration to reduce pressure on the image registry. For details, see [P2P image acceleration](https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution).

* After container startup, lazy loading still requires downloading image data from the registry. If the registry fails after image startup, the container cannot read image content correctly, which leads to unpredictable errors.

* The image lazy loading feature is only available for nodes with containerd version 1.4.13\-vke.3 or later. To view containerd versions, see [FAQ](https://docs.byteplus.com/en/docs/vke/What-container-runtimes-does-VKE-currently-support).

* The image lazy loading feature is currently not supported for VCI scenarios.


<span id=".5L2_55So5pa55rOV"></span>
## Procedure

VKE provides two solutions for creating lazy\-loaded images:


* [Solution 1](https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution#.5pa55qGI5LiA77ya57uT5ZCILWNyLeaPkOS-m-eahOmVnOWDj-i9rOWMluWKn-iDveS9v-eUqOmVnOWDj-aHkuWKoOi9vQ==): Convert the container image format using the rules provided by CR to generate a Nydus image (in lazy\-loading format), and then use this Nydus image in VKE workloads.

* [Solution 2](https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution#.5pa55qGI5LqM77ya6Ieq6KGM6L2s5o2i6ZWc5YOP5qC85byP5L2_55So6ZWc5YOP5oeS5Yqg6L29): Convert the container image format by yourself to generate a Nydus image (in lazy\-loading format), and then use this Nydus image in VKE workloads.


<span id=".5pa55qGI5LiA77ya57uT5ZCILWNyLeaPkOS-m-eahOmVnOWDj-i9rOWMluWKn-iDveS9v-eUqOmVnOWDj-aHkuWKoOi9vQ=="></span>
### Solution 1: Use image lazy loading with the image conversion feature provided by CR

The process for using image lazy loading with the image conversion feature of CR is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7adbf02a15e1128190a3cfb539ee39e.png) </span>


1. Create a lazy loading conversion rule on a standard CR instance. For detailed instructions, see [Creating rules for conversion to lazy-loaded images](https://docs.byteplus.com/en/docs/cr/create-image-lazy-loading-conversion-rules#.5pON5L2c5q2l6aqk).

2. Enable the image lazy loading feature on the node pool in VKE.

   You can use three methods to enable the image lazy loading feature for the node pool:

   * When creating a cluster, in the **Node pool configuration (optional)**  step, enable image lazy loading in the **Advanced settings** section. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * When creating a node pool, enable the image lazy loading in the **Advanced settings ** section of the **Node pool configuration** step. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   * For an existing node pool, you can enable image lazy loading by editing the node pool configuration. For detailed instructions, see [Editing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.57yW6L6R6IqC54K55rGg).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Enabling image lazy loading for an existing node pool only takes effect on new nodes created from scale\-out within the node pool. It does not apply to existing nodes in the pool. Therefore, in such scenarios, scale out the node pool. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool">Scaling node pools</a>.      </div>
      

3. Install the container image acceleration add\-on image\-accelerator on the cluster. For detailed instructions, see [image-accelerator](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW1hZ2UtYWNjZWxlcmF0b3It57uE5Lu2).

4. Push a compliant image to CR to have a Nydus image replica automatically generated. For instructions on pushing images, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To convert an image to a Nydus image, the tag of the original image must be less than or equal to 122 characters (to reserve 6 characters for the <code>-nydus</code> suffix). Otherwise, the conversion will fail.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Pushing an image with the same name to the same OCI artifact repository will overwrite the existing image by default. Please carefully confirm whether the name of the image to be pushed is the same as any existing image in the repository.   </div>
   

5. Use the image lazy loading feature in workloads. The following content uses a Deployment as an example. For detailed instructions, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   1. Use the generated Nydus image replica as the container image for the workload.

   2. Add a label with the key `vke.volcengine.com/image-accelerate-mode` and the value `lazyload` to the pod.

   3. View the pod instance state of the workload to check whether the pod has been scheduled to a node in the node pool with image lazy loading enabled.


<span id=".5pa55qGI5LqM77ya6Ieq6KGM6L2s5o2i6ZWc5YOP5qC85byP5L2_55So6ZWc5YOP5oeS5Yqg6L29"></span>
### Solution 2: Convert the image format yourself to use image lazy loading

The process for manually converting the image format to use image lazy loading is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_826ba93e9011cc96bc9edd8cd1176f97.png) </span>


1. Install the image conversion tool available in the GitHub community to your local system.

   ```bash
   VERSION=v2.1.6
   wget https://github.com/dragonflyoss/image-service/releases/download/${VERSION}/nydus-static-${VERSION}-linux-amd64.tgz
   tar -xf nydus-static-${VERSION}-linux-amd64.tgz
   cd nydus-static
   install nydus-image nydusify /usr/local/bin
   ```
   

2. Convert the image to a Nydus image.

   1. Use `docker login` to log in to the image center. The image center can be an open\-source image center, third\-party repository, or BytePlus CR instance.

   2. From the image center, get the address of the source image to be converted.

   3. Use the image conversion tool to convert the source image, generate the corresponding Nydus image, and push the Nydus image to the target image address.

      ```bash
      nydusify convert --source ${SOURCE_IMAGE} --target ${TARGET_IMAGE}    
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Replace <code>${SOURCE_IMAGE}</code> in the command with the source image address obtained in the previous step (for example, <code>doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0</code>). Replace <code>${TARGET_IMAGE}</code> with the target image address to which the Nydus image will be pushed.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Ensure that you have logged in to the image center corresponding to the target image address (<code>${TARGET_IMAGE}</code>) and have read and write access to its OCI artifact repository, namespace, and other related resources.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Pushing an image with the same name to the same OCI artifact repository will overwrite the existing image by default. Please carefully confirm whether the name of the image to be pushed is the same as any existing image in the image center.      </div>
      

3. Enable the image lazy loading feature on the node pool in VKE.

   You can use three methods to enable the image lazy loading feature for the node pool:

   * When creating a cluster, in the **Node pool configuration (optional)**  step, enable image lazy loading in the **Advanced settings** section. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * When creating a node pool, enable the image lazy loading in the **Advanced settings** section of the **Node pool configuration** step. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   * For an existing node pool, you can enable image lazy loading by editing the node pool configuration. For detailed instructions, see [Editing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.57yW6L6R6IqC54K55rGg).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Enabling image lazy loading for an existing node pool only applies to new nodes added by scaling out the pool. It does not take effect on existing nodes. Therefore, please scale out the node pool in such cases. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool">Scaling node pools</a>.      </div>
      

4. Install the container image acceleration add\-on image\-accelerator on the cluster. For detailed instructions, see [image-accelerator](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW1hZ2UtYWNjZWxlcmF0b3It57uE5Lu2).

5. Use the image lazy loading feature in workloads. The following content provides an example of how to view the monitoring information of a Deployment. For detailed instructions, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   1. Use the generated Nydus image replica as the container image for the workload.

   2. Add a label with the key `vke.volcengine.com/image-accelerate-mode` and the value `lazyload` to the pod.

   3. View the pod instance state of the workload to check whether the pod has been scheduled to a node in the node pool with image lazy loading enabled.


<span id=".6ZmE5b2V"></span>
## Appendix

<span id=".6ZWc5YOP5Yqg6YCf5pa55qGI6YCJ5oup5a-55q-U"></span>
### Comparison of image acceleration solutions

To accelerate pod startup, VKE provides different optimization solutions.


|Item |Image lazy loading |P2P acceleration |Custom node images and warm\-up (beta) |
|---|---|---|---|
|Solution explanation |Leverages access hotspots of image data to load required data on\-demand, improving container startup efficiency. |Uses the internal network bandwidth resources of worker nodes to distribute images between nodes, reducing pressure on the image registry. |Analyzes container images to offload infrequently changing content to node images, reducing container image size. Node images are warmed up to accelerate node readiness. |
|Application scenarios |Large container images, obvious data local hotspots, and frequent image changes. |Large container images and frequent changes. |Infrequent changes to base images. |
|Limits |* Scope of container image content accessed by container applications.<br><br>* Image repository reliability. |* Cloud disk cluster throughput.<br><br>* Pressure on cloud disks from workloads. |Node image cache warm\-up. |


In summary, the custom node image and warm\-up solution have additional steps for image splitting and node image warm\-up. However, after warm\-up, the overall image pulling time and performance are not affected by other factors. Therefore, in scenarios with frequent image changes, you can use the [P2P acceleration](https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution) or image lazy loading solution, or a combination of both.

<span id=".6ZWc5YOP5oeS5Yqg6L2955uR5o6n"></span>
### Monitoring of image lazy loading 

VKE provides Nydus monitoring capabilities, which allow you to monitor metrics related to image lazy loading, such as the number of Nydus Daemons and their memory usage. For details, see [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability).
