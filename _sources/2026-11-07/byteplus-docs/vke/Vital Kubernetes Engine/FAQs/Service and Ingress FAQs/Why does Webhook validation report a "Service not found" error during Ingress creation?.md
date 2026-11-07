---
title: "Why does Webhook validation report a \"Service not found\" error during Ingress creation?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-does-a-Webhook-verification-error-Service-not-found-occur-when-I-create-an-Ingress"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

During Ingress creation, the page displays an error indicating that the Webhook of the ingress\-nginx cannot find the corresponding Service.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The cluster where the Ingress (Nginx Ingress, CLB Ingress, or ALB Ingress) is to be created contains an ingress\-nginx application deployed via **Application center** \> **Application template**. This issue occurs when resources associated with this application, such as the workload (Deployment or DaemonSet) and Service, are deleted, but the corresponding Webhook resource is not removed.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

Follow the steps below to delete the target ingress\-nginx application and its residual resources.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center** \> **Helm**.

3. On the **Helm** page, find the ingress\-nginx application by the project, cluster, and namespace where the application is located, and in the **Actions ** column, click `...` \> **Delete**.

4. In the pop\-up box, select **Synchronous deletion of CRD resources** and click **Confirm** to delete the application.

5. Recreate the Ingress in the cluster. For details, see [Ingress](https://docs.byteplus.com/en/docs/vke/Ingresses).
