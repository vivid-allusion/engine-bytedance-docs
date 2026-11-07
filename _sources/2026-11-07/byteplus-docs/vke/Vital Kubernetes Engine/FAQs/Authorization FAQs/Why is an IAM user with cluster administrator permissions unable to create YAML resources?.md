---
title: "Why is an IAM user with cluster administrator permissions unable to create YAML resources?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-do-I-fail-to-create-YAML-resources-by-using-a-RAM-user-with-cluster-admin-permissions"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

The IAM user has been granted **cluster administrator** permissions via RBAC, but the user is unable to create YAML resources. The system displays the `AccessDenied,Code:403` error, with the error details shown below.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The IAM user has not been assigned an IAM policy that allows managing VKE resources.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

VKE provides two types of IAM policies for authorization: **system preset policy** and **custom policy**. You need to authorize the IAM user to manage VKE resources as needed.

For information about IAM policies, see [Authorization overview](https://docs.byteplus.com/en/docs/vke/Authorization-overview). For information about how to grant permissions, see [Granting permissions to IAM users](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions).
