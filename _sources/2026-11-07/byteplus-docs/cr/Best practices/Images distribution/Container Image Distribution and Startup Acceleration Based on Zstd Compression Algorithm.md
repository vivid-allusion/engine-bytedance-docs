---
title: "Container Image Distribution and Startup Acceleration Based on Zstd Compression Algorithm"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Image_distribution_and_startup_acceleration_based_on_Zstd"
---

The speed of pulling and decompressing container images is one of the key factors affecting container startup time. Traditional container images typically use the gzip compression algorithm. However, zstd (Zstandard), as an efficient compression algorithm, achieves a better balance between compression ratio and speed, thereby optimizing the image transmission and startup process.

## Feature Introduction

[zstd](https://github.com/facebook/zstd) is a compression algorithm developed by Meta. Published [test results](https://engineering.fb.com/2016/08/31/core-data/smaller-and-faster-data-compression-with-zstandard/) show that zstd provides a higher compression ratio and faster decompression than gzip.

* **Faster Decompression Speed**: zstd's decompression speed is significantly faster than that of gzip (usually 5\-10 times faster), especially when handling large\-sized images. This makes it highly suitable for addressing the issue of excessively large AI model images.

* **Higher Compression Ratio**: At the same compression level, zstd can provide a higher compression ratio than gzip (for example, at the default compression level of \-3, zstd's compression ratio is close to gzip's level \-6, but with faster speed), thereby reducing the data volume during image transmission and lowering network latency.

* **Minimal Modification Complexity**: To use zstd, you only need to specify the compression format as zstd when packaging the image. The Vital Kubernetes Engine and Container Registry support this format by default when pushing and pulling images.

## Application scenarios

* Pulling large\-sized images, such as when starting AI services (e.g., VLLM, SGlang open\-source images, or proprietary large\-sized images).

* CI/CD processes that are sensitive to build and pull speeds.

## Prerequisites

* A Vital Kubernetes Engine (VKE) cluster has been created. For instructions on how to create a cluster, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* A Standard Edition instance has been created. For detailed operations, please refer to [Purchasing a Standard Edition Instance](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

      ```Bash
      
      ```

##

## Step 1: Build zstd\-Formatted Images and Push Them to the Container Registry

1. Build new zstd images.

> **tip**

> There are many tools for building container images, such as Docker Build, Buildkit, and Buildah. This document provides only two building methods. If you use other building tools, please refer to their corresponding documentation.

**Build zstd\-compressed container images using Docker and BuildKit**

   Buildkit is an independent container image building tool that can run on a Linux machine or container environment. We can easily interact with Buildkit through the Docker Buildx plugin (a Docker CLI plugin). Generally, Docker Desktop comes pre\-installed with this plugin; if using a Linux host, manual installation is required. After installation, you can use the build command to build images in the zstd compression format. The reference commands are as follows:

   1. Create a BuildKit build instance and switch to it.

      ```Bash
      # First create a Buildkit Container Image Builder
      $ docker buildx create \
        --name zstd-builder \
        --driver docker-container \
        --driver-opt image=moby/buildkit:v0.10.3
       
      # Switch the Buildx Context to the new Builder
      $ docker buildx use zstd-builder
      ```

      * \-\-name zstd\-builder: Customize the build instance name for easy subsequent reference.

      * \-\-driver docker\-container: Use a containerized BuildKit instance to avoid version conflicts with the local Docker engine.

      * \-\-driver\-opt image=moby/buildkit:v0.10.3: Specify the BuildKit version to ensure the availability of the zstd compression feature (supported by BuildKit v0.9+).

   2. Build an image using zstd compression and complete the image push.

      ```Bash
      $ docker buildx build \
        --file Dockerfile \
        --output type=image,name=$IMAGE_URI:$IMAGE_TAG,oci-mediatypes=true,compression=zstd,compression-level=3,force-compression=true,push=true .
      ```

      * \-\-file Dockerfile: Specify the path of the Dockerfile used for building.

      * \-\-output ...: Configure the output format and behavior:

         * type=image: Output as a container image.

         * name=$IMAGE_URI:$IMAGE_TAG: Specify the full URI and label of the image (e.g., myrepo/myimage:latest).

         * oci\-mediatypes=true: Use the media types of OCI standard (better compatibility).

         * compression=zstd: Enable zstd compression (replacing the default gzip).

         * compression\-level=3: Set the zstd compression level to 3 (balancing compression ratio and speed; the default is 3).

         * force\-compression=true: Force compression on all layers (including layers that may already be compressed).

         * push=true: Directly push to the remote registry after image building is completed.

2. Convert existing images.

   This document recommends converting existing images into the zstd compression format using Skopeo. Skopeo supports specifying the compression format (including zstd) through the \-\-dest\-compress\-format parameter. Here are the specific steps:

   1. Check the Skopeo version.

      > **warning**

      > Version 1.4 or above is required, which supports the zstd feature.

      ```Bash
      skopeo --version    
      ```

   2. (Optional) If the version is lower than 1.4, please install version 1.4 or above.

      ```YAML
      # Ubuntu/Debian
      sudo apt-get install skopeo
      # CentOS/RHEL
      sudo dnf install skopeo
      # macOS
      brew install skopeo
      ```

   3. Convert the image to the **zstd** compression format.

      Use skopeo copy and specify \-\-dest\-compress\-format=zstd

      ```Bash
      skopeo copy \
          --dest-compress-format=zstd \
          docker://docker.io/library/nginx:latest \
          oci:/path/to/output/nginx-zstd:oci
      ```

      * \-\-dest\-compress\-format=zstd: Specify that the target uses zstd compression.

      * docker://: The source image address.

      * oci:/path/to/output/nginx\-zstd:oci: Output as the OCI format and store it at the specified path.

   4. Verify the compression format. The mediaType in Layers, which should be application/vnd.oci.image.layer.v1.tar+zstd

      ```YAML
      skopeo inspect oci:/path/to/output/nginx-zstd:oci
      ```

   5. Push or use the image. Push it to the Container Registry (or other registries that support zstd compression format).

      ```Bash
      skopeo copy \
          oci:/path/to/output/nginx-zstd:oci \
          docker://instance-cn-beijing.cr.volces.com/nginx:zstd
      ```

## Step 2: Distribute zstd\-Format Images via P2P

1. Enable P2P distribution.

   > **tip**

   > This document introduces the main procedure. For detailed instructions on enabling P2P, please refer to the [P2P Acceleration Overview](https://docs.byteplus.com/en/docs/cr/p2p-acceleration-overview).

   1. Log in to the [CR console](https://console.byteplus.com/cr). On the **Distribution Acceleration** \> **P2P Acceleration** page of the target instance, enable the P2P acceleration feature.

      |**Parameter** |**Description** |
      |---|---|
      |VPC Range |Select the Virtual Private Cloud (VPC) for the P2P acceleration feature. VKE cluster nodes within this VPC can utilize the P2P acceleration feature of the Standard Edition instance. |

   2. Log in to the [VKE console](https://console.byteplus.com/vke). On the **Operations & Maintenance Management** \> **Add\-on Management** page of the target cluster, install the **p2p\-accelerator** add\-on.

2. Distribute zstd images.

   * For new services: Create a stateless workload that pulls zstd\-formatted images, and pull these images using the P2P method. For operating instructions, please refer to [Creating Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * For existing services: Redeploy the workload with a single click in the Vital Kubernetes Engine console to make the distribution of zstd images take effect.

## Test result

End\-to\-end tests were conducted on nodes with high\-specification (large bandwidth) local disks to measure the time from pulling an image to starting it within the container's intranet. The test results are as follows: When building the same image, the zstd format offers better compression and shorter image distribution times.

> **tip**

> In actual use, the specific end\-to\-end pull time may vary depending on factors such as node specifications, disk, and other conditions.

|**Number of nodes** |Size of Image Built |**Compression Format** |**End\-to\-End Pull Time** |**Conclusion** |
|---|---|---|---|---|
|10 |10.8GiB |gzip |1m36s~1m39s |When building the same image, the zstd format provides better compression and shorter image distribution times. |
|10 |9.36GiB |zstd |45s~48s ||
|10 |27.7GiB |gzip |4m19s~4m23s |When building the same image, the zstd format provides better compression and shorter image distribution times. |
|10 |24.93GiB |zstd |2m39s~2m46s ||
