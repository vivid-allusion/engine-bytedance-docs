---
title: "Edit image tag description"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Edit_image_tag_description"
---

CR supports adding Description for image tags (Tag). This article describes how to edit the Description of an image tag.

<span id="mgrZgdbQ"></span>
## Background

In actual use, there are often a large number of tags under the same CR (for example, v1.0.0, latest, release\-2026, and so on). It is difficult to quickly determine the purpose and status of each version based only on the tag name. After adding Description for an image tag, you can directly view the purpose description of each version in the **Description** column of the image list, without having to pull each image for confirmation. This is applicable to the following scenarios:


* **Environment distinction**: Mark the environment to which the version belongs, such as production environment, test environment, or pre\-release environment.

* **Status marking**: Mark the release status of the version, such as stable, pending verification, or pending offline.

* **Change traceability**: Record the requirements, owner, or change description corresponding to the version, facilitating team collaboration and traceability.


<span id="QdqE6skE"></span>
## Considerations


* The maximum length of a single Description is **255 characters.** 

* When marking multiple attributes in the Description, use an English comma (,) to separate them, for example, prod,stable.


<span id="hq7oRKCh"></span>
## Prerequisites


* Instance has been created. For actions, see [Create standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* Namespace has been created. For actions, see [Create namespace ](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

* The image has been pushed to the CR instance. For details, see [Push and pull artifacts ](https://docs.byteplus.com/en/docs/cr/push-and-pull-images?lang=en).


<span id="MQPNxRgS"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. Log in to the OCI artifact overview page.

   1. In the left navigation bar of the instance page, click **OCI artifact repository**.

   2. On the **OCI artifact repository** page, click the name of the target OCI artifact repository.

3. In the **image list**, find the target image tag, and click **edit** in the **description** column.

4. Enter description content in the edit box, click **confirm**, and complete the operation.
