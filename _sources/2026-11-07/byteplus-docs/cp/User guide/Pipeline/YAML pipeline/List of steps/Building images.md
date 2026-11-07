---
title: "Building images"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Building_images"
---

The image step is used to build container images and push them to the specified container registry.

<span id="V2veLII7"></span>
## Building images and pushing to the platform container registry (CR)

Use BuildKit to efficiently build Docker images and automatically push them to the container registry (CR) provided by the platform.


* **Addon**: buildkit\-cr@4.0.0

* **Parameter**:

   
   |**Parameter** |**Type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |region |string |Yes |\- |Region where the container registry is located. |
   |registryInstance |string |Yes |\- |Container Registry instance. |
   |namespace |string |Yes |\- |Namespace of the container registry. |
   |repo |string |Yes |\- |Repository name. |
   |tag |string |Yes |\- |Image tag. |
   |dockerfiles |object |Yes |\- |Source of the Dockerfile. Specify the file path using default.path, or inline content using default.content. |
   |contextPath |string |Yes |. |Relative path of the Docker build context. |
   |compression |enum |No |gzip |Image compression algorithm, optional gzip, zstd. |
   |useCache |boolean |No |\- |Whether to use cache to accelerate image building.<br><br><br>* `true`: Use cache.<br><br>* `false`: Default value. Do not use cache. |
   |disableSSLVerify |boolean |No |\- |Whether to disable SSL certificate verification.<br><br><br>* `true`: Disable.<br><br>* `false`: Default value. Do not disable. |
   |buildParams |string |No |\- |Support specifying docker build parameters such as \-\-build\-arg, \-\-target, and so on. |
   

* **Example**

   ```YAML
   tasks:
     - task: build-image-and-push-to-registry
       displayName: Build and Push to CR
       steps:
         - step: buildkit-cr
           displayName: Build and Push to CR
           component: buildkit-cr@4.0.0
           inputs:
             region: cn-beijing
             registryInstance: my-registry-instance
             namespace: my-namespace
             repo: my-repo
             tag: v1.0.0
             contextPath: .
             dockerfiles:
               default:
                 path: ./Dockerfile
   ```
   


<span id="3XIHQycH"></span>
## Building images and pushing to a custom repository

Build Docker images and push them to user\-defined, non\-platform\-managed container registries (such as Docker Hub, Harbor, and so on).


* **Addon**: buildkit\-custom@3.0.0

* **Parameter**:

   
   |**Parameter** |**Type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |customImageAddress.protocol |enum |Yes |https |Repository URL protocol, optional http, https. |
   |customImageAddress.address |string |Yes |\- |Complete image address, in the format host/repo:tag. |
   |loginCredential |list |No |\- |Credentials for accessing the custom repository, use service connection. |
   |dockerfiles |object |Yes |\- |Dockerfile source, specified by default.path or default.content. |
   |contextPath |string |Yes |\- |Build context path. |
   |compression |enum |No |gzip |Compression algorithm, optional `gzip`, `zstd`. |
   |useCache |boolean |No |\- |Whether to use cache to accelerate image building.<br><br><br>* `true`: Use cache.<br><br>* `false`: Default value. Do not use cache. |
   |disableSSLVerify |boolean |No |\- |Whether to disable SSL certificate verification.<br><br><br>* `true`: Disable.<br><br>* false: Default value. Do not disable. |
   |buildParams |string |No |\- |Support specifying docker build parameters such as \-\-build\-arg, \-\-target, and so on. |
   

* Example:

   ```YAML
   tasks:
     - task: build-image-and-push-to-custom-server
       displayName: Build and Push to Custom Registry
       steps:
         - step: buildkit-custom
           displayName: Build and Push to Custom Registry
           component: buildkit-custom@3.0.0
           inputs:
             customImageAddress:
               protocol: https
               address: registry.example.com/my-org/my-app:v1.0.0
             contextPath: .
             dockerfiles:
               default:
                 path: ./Dockerfile
   ```
