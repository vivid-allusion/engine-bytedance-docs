---
title: "Image commit"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Image_commit"
---

This topic mainly describes the image commit feature in VCI Agent Sandbox and its usage instructions.

<span id="KKmebCi9"></span>
## Feature introduction

VCI Agent Sandbox provides the image commit capability for the container root file system (container rootfs). It allows images to be pushed to an image registry after being committed. This is suitable for periodically archiving data generated during runtime.

<span id="p96oQEb5"></span>
## Usage instructions


* VCI does not automatically clean up historical images pushed to image registries. Therefore, you need to pay attention to the image registry capacity usage.

* According to the OCI image specification, a single image can have up to 128 layers. After multiple images are committed, this limit may be triggered, which causes commit failures. We recommend that you commit images only at critical time points or periodically merge layers by rebuilding images.


<span id="NrLABySo"></span>
## Procedure


1. Before performing an image commit, prepare an image registry and obtain the username and password of the registry. You can use BytePlus CR to create an image registry. For details, see [Getting started with CR](https://docs.byteplus.com/en/docs/cr/getting-started).

2. Configure the image registry username and password in the Secret object. For details, see [Creating Secrets](https://docs.byteplus.com/en/docs/vke/Creating-a-Secret).

3. Automatically create an image commit and generate an image cache by using the ContainerImageCommit CRD.

   ```YAML
   apiVersion: extensions.agents.x-k8s.io/v1alpha1
   kind: ContainerImageCommit
   metadata:
     namespace: default
     name: test-commit
   spec:
     target:
       sandboxRef:
         apiVersion: agents.x-k8s.io/v1alpha1
         kind: Sandbox
         namespace: default
         name: test-sandbox-example
       containerName: test-server # The name of the container for which the image commit is performed.
     image:  # The parameters used during the image commit.
       name: sandbox-0202:v0.1.1   # The image address and tag.
       author: bob
       changes:   # Only ENTRYPOINT and CMD are supported.
       - "ENTRYPOINT ["nginx"]"  # The executable file to execute when the container starts.
       - "CMD ["-g", "daemon off;"]"  # The default parameters passed to ENTRYPOINT when the container starts.
       message: "generate commit v0.1.1"
     imageCacheConfig:
       enable: true # After the image is uploaded, the image cache is automatically created.
       subnetIds: # The subnet IDs used for creating the image cache. You can specify Pod subnets in the cluster.
       - subnet-xxx
       - subnet-yyy
       securityGroupIds:  # The security groups used for creating the image cache. You can specify Pod security groups in the cluster.
       - sg-xxx
       retentionDays: 10 # Optional. The retention duration of the image cache. Unit: days.
       imageCacheSize: 50 # Optional. The size of the image cache. Unit: GiB.
     authConfig: # The authentication information used for pushing the image.
       secretRef:
         name: test-registry-auth # The name of the Secret that contains the configured image registry username and password.
         namespace: default  # The namespace where the Secret is stored. If you do not specify this parameter, the namespace of ContainerImageCommit is used by default.
       skipTlsVerify: true # Specify whether to skip TLS verification. Valid values: true (skip) and false (do not skip).
       plainHttp: true   # Specify whether to use HTTP. Valid values: true (use) and false (do not use).
     pause: false # Specify whether to suspend the container when the image is being packaged. Valid values: true (suspend container) and false (do not suspend container).
     timeout: "60m"  # Optional. The timeout period of ContainerImageCommit. The status will not update after the timeout period. The value is in the format of number+unit. For example, "60m" indicates 60 minutes and "120s" indicates 120 seconds.
     retentionDays: 15 # Optional. The retention period of the Commit Custom Resource. This does not impact the generated image and image cache. Unit: days.
   ```
   

   If the `status.phase` of the CRD changes to **Completed**, it indicates that the image is packaged and pushed. The sample code is as follows.

   ```YAML
   status:
     phase: Completed # The image is packaged and pushed.
     taskId: fake-id
     tryCount: 1
   ```
