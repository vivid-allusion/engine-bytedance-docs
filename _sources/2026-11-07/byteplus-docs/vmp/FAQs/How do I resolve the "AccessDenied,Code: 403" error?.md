---
title: "How do I resolve the \"AccessDenied,Code: 403\" error?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/What-can-I-do-if-the-system-prompts-AccessDenied-Code403"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue Description

Create an IAM user with the BytePlus root user, then log in to the VMP configuration interface with the IAM user. The system prompts an **Insufficient Permission** message. The error message is `AccessDenied, Code: 403`.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause Analysis

The IAM user used to log in has not been authorized for VMP and does not have operation permission for related resources. For detailed introduction on authorization, please refer to [Permission Overview](https://docs.byteplus.com/en/docs/vmp/Permission-overview).

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Log in to the [IAM Console](https://console.byteplus.com/iam).

2. In the left navigation bar, select **Identity Management**\> **Users**.

3. In the **user list**, find the target username, and click **Add Permission** under the corresponding **Operation** column.

4. On the **User Details** page, select **Permission** \> **Global Permissions** tab, and click **Add Permission**.

5. Enter VMP in the search box of the **Add Permission** panel to search for system preset policies related to the VMP service.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97222100253041b618881cc773054cdb.png) </span>

6. According to actual needs, select the `VMPFullAccess` policy or the `VMPReadOnlyAccess` policy, click **Confirm**, and authorize the IAM user.
