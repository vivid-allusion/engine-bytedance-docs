---
title: "IRSA overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/IRSA-overview"
---

Vital Kubernetes Engine (VKE) integrates with Identity and Access Management (IAM) to provide the IAM roles for service accounts (IRSA) mechanism, which achieves fine\-grained pod\-level permission isolation based on VKE.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Typically, applications within a VKE cluster access other BytePlus cloud resources by using the following methods:


* Access the OpenAPIs of cloud resources by using the Security Token Service (STS) tokens of IAM roles, which are obtained through the metadata of the instances with which the IAM roles are associated. For details about instance metadata, see [ECS instance metadata ](https://docs.byteplus.com/en/docs/ecs/Instance-metadata-overview)and [VCI instance metadata ](https://docs.byteplus.com/en/docs/vke/Instance-metadata-overview).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">VKE clusters are built based on Elastic Compute Service (ECS) and Vital Container Instance (VCI). The metadata of ECS and VCI instances contains the basic information of the instances on the BytePlus cloud platform.   </div>
   

* Access cloud resources by using the long\-term access key of a BytePlus IAM user or a role.


Both access methods may bring high security risks and make it difficult to isolate permissions based on different applications in a cluster. Therefore, the IRSA solution is provided by VKE to help you associate IAM roles with applications at the pod level in a cluster.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

IRSA is a security mechanism that allows applications in a VKE cluster to use BytePlus IAM roles through Kubernetes service accounts. The IRSA mechanism associates a specific IAM role with a service account. This enables pods running in a VKE cluster to obtain the permissions granted to the role through the service account. In this way, the pods can access corresponding cloud service resources.

The following figure shows the workflow of the IRSA feature.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_218069a7d746c82705d626b245c0b36d.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17b0f1bca8c28f6600b20b240c3d9b9a.png) </span>


1. A client launches a pod using service account token projection. For details, see [Configure Service Accounts for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/).

2. The cluster API server issues an OIDC token for the pod, which is generated based on the OIDC identity, and then the kubelet mounts the token for the pod and refreshes it regularly.

3. The program running in the pod accesses the AssumeRoleWithOIDC API of STS by using the mounted OIDC token file to obtain a temporary credential for the specified IAM role.

4. The program running in the pod uses temporary credentials to access the OpenAPIs of other cloud resources on BytePlus.


<span id=".5Yqf6IO95LyY5Yq_"></span>
## Feature advantages

Key advantages of the IRSA mechanism:


* **Principle of least privilege**: Assign a specific IAM role to each service account. This enables fine\-grained permission management for services. It ensures services only access necessary resources, enhancing business security and conforming to the principle of least privilege.

* **Security**: IRSA minimizes the requirements for hard\-coding access credentials in application code or container images, which reduces potential security risks.

* **Easy management ** : Kubernetes service accounts enable simplified, centralized, and unified permission management for cloud resource access.
