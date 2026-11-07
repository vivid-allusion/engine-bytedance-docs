---
title: "Overview of image"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Image-overview"
---

<span id=".6ZWc5YOP5qaC6L-w"></span>
## Overview

An image is a special file that contains the basic operating system and application data required for an ECS instance. When creating an instance, you are required to select an image.

<span id=".6ZWc5YOP57G75Z6L"></span>
## Types

ECS images include public images, custom images, shared images based on different sources.


* **Public Image:**  An image provided by the BytePlus platform with legitimate copyrights. Therefore, this kind of image offers high security and stability. Currently, public images include the mainstream Windows Server and Linux images, and are available for all users to view or use. For information about image types and versions, refer to the [Image release notes](https://docs.byteplus.com/en/docs/ecs/Image-release-notes).

* **Custom Image:**  A custom image is an image that you create yourself from an instance or snapshot, or upload from your local device. It is your private image. In addition to the operating system, you can pre\-install public applications or private applications in the image based on your business requirements. Custom images are applicable to scenarios where you need to redeploy systems with complex initialization or deploy servers with the same configuration multiple times.

* **Shared Image:**  An image shared by other BytePlus accounts. By using shared images, you can quickly deploy the same software environment as that on ECS instances created by other accounts. You can also share custom images that you create or upload with other BytePlus accounts. For more information, refer to the [Sharing or unsharing custom images](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image).


<span id=".6ZWc5YOP6LS555So"></span>
## Fee

Fees may be incurred when you use images. For details, refer to the [Billing of image](https://docs.byteplus.com/en/docs/ecs/Imagebilling).

<span id="5GPQCowk"></span>
## Limits

Custom image: Each region supports a maximum of 50 custom images.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you want to increase your custom image quota, go to <a href="https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs">Quota Center</a> and submit an application.</div>
