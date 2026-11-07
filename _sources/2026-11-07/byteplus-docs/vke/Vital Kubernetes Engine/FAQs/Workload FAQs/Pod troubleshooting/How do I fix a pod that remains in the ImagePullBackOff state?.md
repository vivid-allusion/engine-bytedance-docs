---
title: "How do I fix a pod that remains in the ImagePullBackOff state?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pod-in-the-ImagePullBackOff-state"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

The pod remains in the **ImagePullBackOff** state for an extended period.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

If the pod is in the **ImagePullBackOff** state, the pod has been successfully scheduled, but container image pulling failed. Possible reasons are as follows:


* Incorrect image address

* No imagePullSecret configured for the private image

* Invalid domain configuration for the private image

* Corrupted image file

* Image pull timeout


<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

<span id=".6ZWc5YOP5Zyw5Z2A5LiN5q2j56Gu"></span>
### Incorrect image address


1. Check whether the image address, name, and version are correctly configured. When the version tag is `latest`, confirm that an image with version tag `latest` exists in the image repository.

2. Run the following command to manually pull the image and confirm whether the image address is correct.

   ```bash
   docker pull <imange-name>
   ```
   


<span id=".56eB5pyJ6ZWc5YOP5pyq6YWN572uLWltYWdlcHVsbHNlY3JldA=="></span>
### No imagePullSecret configured for the private image

The pod pulls a private image. However, if no imagePullSecret is configured, or the configured Secret does not exist or is incorrect, authentication will fail, causing the pod to remain in the ImagePullBackOff state. The `401 Unauthorized` event is recorded for the pod.

Solution: Configure an imagePullSecret to enable password\-free image pulling for containers in the cluster. For details, see [Using a VKE add-on for password-free image pulling over the internal network](https://docs.byteplus.com/en/docs/cr/pull-images-over-the-internal-network-without-providing-credentials). 

<span id=".56eB5pyJ6ZWc5YOP5Z-f5ZCN6YWN572u6ZSZ6K-v"></span>
### Invalid domain configuration for the private image

The pod uses a private image and imagePullSecrets are configured, but the domain name in these imagePullSecrets is inconsistent with the domain name for the workload. This will cause the pod to remain in the ImagePullBackOff state.

Solution: see [How do I handle image pulling failures?](https://docs.byteplus.com/en/docs/cr/What-do-I-do-when-I-fail-to-pull-an-image)

<span id=".6ZWc5YOP5paH5Lu25o2f5Z2P"></span>
### Corrupted image file

If the image file is corrupted, it cannot be used normally even after it is downloaded. In this case, you need to push the image file again.

<span id=".6ZWc5YOP5ouJ5Y-W6LaF5pe2"></span>
### Image pull timeout

When a large number of pods are started simultaneously on a node, image downloads may be queued. If there are many large\-size images that require lengthy download times at the front of the queue, the pods positioned later in the queue will experience image pull timeouts. At this point, a `pull QPS exceeded` error is reported. An example of the error log is as follows.

```bash
1s          Normal    Created           pod/****-pod   Created container step-git-clone-0
1s          Normal    Started           pod/****-pod   Started container step-git-clone-0
1s          Normal    Pulling           pod/****-pod   Pulling image "cr-cn-****.volces.com/cp-system/exec-bash:v1.0.0"
1s          Normal    PullImageFailed   taskrun/****   build step "step-tos-cache-2-push" is pending with reason "pull QPS exceeded"
```


The cause of this phenomenon is that the kubelet parameter `serialize-image-pulls` is configured for **serial** download, or the number of concurrent downloads exceeds the threshold.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>pull QPS exceeded</code> error does not impact the normal download of pod images. When a pod times out in the queue, it will rejoin the download queue and retry pulling the image.</div>


Solution: To avoid Pod image pull timeouts and the `pull QPS exceeded` error, you can enable parallel downloads in kubelet and configure the number of concurrent downloads. For details, see [Configuring kubelet parameters](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more detailed configuration instructions, see the <a href="https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/">kubelet documentation</a>.</div>
