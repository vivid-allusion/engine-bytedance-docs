---
title: "How do I fix image pull failures?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/What-do-I-do-when-I-fail-to-pull-an-image"
---

This topic describes some scenarios that may cause image pull failures. It also provides the corresponding solutions.

> **tip**

> If none of the following methods resolve your issue, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000208). Provide the operation logs and detailed error messages. This helps support engineers resolve the issue as soon as possible.

## Incorrect image address or missing permission for the image

### Issue description

When you execute the `docker pull` command, the **Error response from daemon: unauthorized** error message is returned.

### Cause

The image address is incorrect, or you do not have permission for the image.

### Solution

* If the error occurs when you pull a public image:

   Check whether the image address is correct. Then upload the image again.

* If the error occurs when you pull a private image:

   * Your account may not have permission to access the CR instance or namespace where the private image is stored. Contact the root user to grant the required permissions. After the permissions are granted, try again.

   * Check whether the image address is correct. Then upload the image again.

## Invalid domain configuration for the private image

### Issue description

When a VKE workload pulls a private image, the error `imagepullbackoff` appears.

### Cause

In VKE, a workload using a private image is configured with imagePullSecrets, but the domain name in imagePullSecrets does not match the domain name in the workload.

### Solution

Set the CR instance domain name in the Secret to match the domain name in the workload. The procedure is as follows.

1. View the domain name in the workload.

2. View the Secret used by the workload.

3. Set the CR instance domain name in the Secret to match the domain name in the workload. For details, see [Managing Secrets](https://docs.byteplus.com/en/docs/vke/Managing-Secrets).
