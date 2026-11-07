---
title: "How to resolve a Kubernetes image upgrade reporting image pull failure and returning a 401 error"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_resolve_a_Kubernetes_image_upgrade_reporting_image_pull_failure_and_returning_a_401_error"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

When upgrading the image of a target application in BytePlus Container Service using a private image stored in the BytePlus Beijing Region image repository, the system displays an image pull failure and returns a 401: Unauthorized error.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

When a container service cluster pulls a private image, it uses the repository domain name, username, and password stored in the credential store. The system reports that the image pull failed and returns a 401: Unauthorized error, indicating that authentication failed when attempting to pull a private image. The mirror repository domain name for the Beijing Region has been changed from `cr-cn-beijing.ivolces.com` to `cr-cn-beijing.volces.com`. Please confirm that you have updated the repository domain name.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Please check the Secret for the repository key type configured in your container service to ensure that the correct repository domain name, username, and password are set. For detailed instructions, see [Update confidential dictionary](https://docs.byteplus.com/en/docs/vke/Managing-Secrets#更新保密字典).

2. Rerun the pipeline.
