---
title: "Image lazy loading overview"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Image_lazy_loading_overview"
---

CR Support image lazy loading capability. By converting container images to Nydus format, image data layers are loaded on demand, significantly shortening container start time.

<span id="ADNSCEoX"></span>
## Feature introduction

In the traditional container start process, the container runtime must download the complete container image to the local node before starting the container. When the image size is large (several GB or even tens of GB), the image download time will significantly extend the pod's end\-to\-end start time.

Image lazy loading changes this process: before starting the container, there is no need to download the full image. During runtime, only the required data blocks are loaded on demand. This method can reduce the impact of image pull on start time from minutes to seconds.

In the repository, you only need to configure the image lazy loading conversion rule. The target image pushed to the repository will automatically generate a Nydus format accelerated replica. After installing the image\-accelerator addon on the container service cluster node, workloads can directly use the Nydus image for on\-demand loading, effectively shortening container start time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For each image that matches a conversion rule, the system automatically generates a lazy\-loaded image. This image is stored in the same OCI artifact repository as the source image, with the <code>nydus</code> suffix.</div>


<span id="YJ0OGOfB"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63aa1ce0d3edc7b453aa0af4836e474e.png) </span>

<span id="tTOUksiI"></span>
## Application scenario


|**Scenario** |**Description** |
|---|---|
|Large image startup acceleration |For AI inference, big data processing, and other workloads with image sizes exceeding 1 GB, the start time can be reduced from minutes to seconds. |
|Autoscaling scenario |During cluster autoscaling, new nodes have no local image cache. Image lazy loading avoids full download and significantly accelerates pod readiness. |
|Frequent CI/CD releases |Each time the image tag is updated during release, nodes without cache need to pull again. Image lazy loading only loads changed data blocks, reducing bandwidth consumption. |


<span id="iorc7TxW"></span>
## Usage process

You can use CR and VKE to implement image lazy loading and rapidly start container images. The overall implementation process is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35f5c99072e3229149fc2b00cf9181a0.png) </span>

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To convert an image to the Nydus format, the tag of the original image must be less than or equal to 122 characters (leaving 6 characters for the <code>-nydus</code> suffix). Otherwise, the conversion will fail.</div>


* <div data-tips="true" data-tips-type="warning">Pushing an image with the same name to the same OCI artifact repository will overwrite the existing image by default.</div>


1. Create an image lazy loading conversion rule in CR, which is described in this section.

2. Enable the image loading feature on the nodes of the target VKE cluster. For details, see [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools) and **Image lazy loading**.

3. Install the acceleration add\-on in the target VKE cluster. For details, see the ** image\-accelerator add\-on ** section in [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

4. Push a compliant image to CR to have a Nydus image replica automatically generated. For instructions on pushing images, see the push section in [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

5. Pull the Nydus image in the workload to start the container, and add the label `vke.volcengine.com/image-accelerate-mode: lazyload` to the Pod. For details, see [Updating Deployment](https://docs.byteplus.com/en/docs/vke/Managing-Deployments#.5pu05paw5peg54q25oCB6LSf6L29).
