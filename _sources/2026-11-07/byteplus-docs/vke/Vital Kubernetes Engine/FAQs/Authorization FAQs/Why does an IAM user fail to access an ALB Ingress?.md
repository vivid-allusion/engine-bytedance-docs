---
title: "Why does an IAM user fail to access an ALB Ingress?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cannot-access-ALB-Ingresses-with-an-IAM-user"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

An IAM user that is granted access to ALB Ingress resources by the BytePlus root user encounters a **403** error when accessing ALB Ingress resources.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Cause


1. Accessing ALB Ingress resources requires [ALBInstance](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl) access. ALBInstance is a cluster\-level resource, and the corresponding resource\-level access must be enabled.

2. When the IAM user is granted access to ALB Ingress resources by using the console, if a specific namespace is specified, the IAM user can only access resources in the namespace.


<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

Enable access to ALBInstance resources (cluster\-level resources). For detailed steps, see [How do I grant cluster-level resource permissions to IAM users?](https://docs.byteplus.com/en/docs/vke/How-do-I-grant-an-IAM-user-permissions-on-cluster-level-resources)
