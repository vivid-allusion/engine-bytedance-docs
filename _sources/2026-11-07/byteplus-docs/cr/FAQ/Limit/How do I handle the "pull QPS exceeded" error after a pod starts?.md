---
title: "How do I handle the \"pull QPS exceeded\" error after a pod starts?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How_to_handle_the_pull_QPS_exceeded_error_after_Pod_startup"
---

## Issue description

After a pod starts, images fail to be pulled with the error `pull QPS exceeded`. A sample log is shown below.

```Plain Text
1s          Normal    Created           pod/****-pod   Created container step-git-clone-0
1s          Normal    Started           pod/****-pod   Started container step-git-clone-0
1s          Normal    Pulling           pod/****-pod   Pulling image "cr-cn-****.volces.com/cp-system/exec-bash:v1.0.0"
1s          Normal    PullImageFailed   taskrun/****   build step "step-tos-cache-2-push" is pending with reason "pull QPS exceeded"
```

## Solution

This issue is caused by limits in the Kubelet add\-on itself, not by CR. If this issue occurs, increase the values of `registryBurst` and `registryPullQPS` in Kubelet. The final parameter values depend on your specific workload scenario. Tune them based on your actual business needs.
