---
title: "Preparations"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Preparations"
---

Before using Code Pipeline, you need to complete the preparations in this document.

<span id=".5rOo5YaM54Gr5bGx5byV5pOO6LSm5Y-3"></span>
## Perform enterprise authentication for an account

If your account has been verified as an enterprise account, please proceed to the next task. If you have not completed enterprise certification for your account, please refer to [Enterprise Certification](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id=".5byA6YCa54Gr5bGx5byV5pOO5oyB57ut5Lqk5LuY"></span>
## Enable BytePlus Code Pipeline

If you have enabled Code Pipeline, please skip to the next task. If you have not activated the product, log in to the [Code Pipeline Console](https://console.byteplus.com/cp) and follow the console instructions to activate it.

<span id=".6YWN572u5oyB57ut5Lqk5LuY5p2D6ZmQ"></span>
## Configure Code Pipeline permissions

The BytePlus account you register will be your primary account and, by default, has all permissions for the Code Pipeline product. To facilitate collaborative actions by multiple users in managing the resources under your account, you need to create IAM (Identity and Access Management, Access control) users (also known as sub\-users) and assign appropriate roles and permissions to IAM users. For detailed instructions, see [Configure permissions](https://docs.byteplus.com/en/docs/cp/Configure_IAM_user_permissions).

<span id=".77yI5Y-v6YCJ77yJ5byA6YCa54Gr5bGx5byV5pOO5a655Zmo5pyN5Yqh"></span>
## (Optional) Enable BytePlus Container Service

Code Pipeline, in combination with BytePlus Container Service and BytePlus Image Registry, provides a one\-stop experience for containerized continuous delivery. If you need to deploy clusters in the BytePlus Container Service, you must enable the container service and, as required, perform the following actions.


* [Create a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* [Create stateless workloads](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).


<span id=".77yI5Y-v6YCJ77yJ5byA6YCa54Gr5bGx5byV5pOO6ZWc5YOP5LuT5bqT"></span>
## (Optional) Enable the BytePlus image repository

If you need to push the built image to the BytePlus image repository, you must enable the image repository service. Ensure that you complete the following actions.

[Create a namespace](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

<span id=".77yI5Y-v6YCJ77yJ5a6M5oiQ6Leo5pyN5Yqh5o6I5p2D"></span>
## (Optional) Complete cross\-service authorization

Code Pipeline enables inter\-service calls through cross\-service authorization. If you need to properly connect to other required BytePlus services, such as container services or image repositories, you must complete [cross-service authorization](https://docs.byteplus.com/en/docs/cp/Cross-service_authorization).

<span id=".77yI5Y-v6YCJ77yJ5o6l5YWl6YOo572y6LWE5rqQ"></span>
## (Optional) Integrate deploy resource

The resource required for an application to run in a specific environment, such as a container cluster, virtual machine, or physical machine, is called a deployment resource. If you need to use application delivery features or deployment capabilities in the pipeline (such as Kubernetes image upgrade, Kubernetes rolling release, or kubectl release), you must first [Integrate the deploy resource](https://docs.byteplus.com/en/docs/cp/Integrate_custom_clusters).
