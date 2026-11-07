---
title: "Spaces"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-space-management"
---

BytePlus VOD uses spaces as the basic unit for resource isolation. Each space can be customized with stand\-alone business resources, templates, processes, and policies. For example, if you have multiple applications, you can create a unique space for each one. This article guides you on how to create and manage spaces within the BytePlus VOD console.

<span id="1d3efd63"></span>
## Prerequisites

Ensure that you have enabled the BytePlus VOD service.

<span id="7ce94a60"></span>
## Considerations


* A BytePlus account can create up to 20 spaces.

* After the space is created, the space name and region cannot be changed. The space name should be unique under a BytePlus account. We recommend that you use a name that clearly identifies your business.


<span id="ab3bca37"></span>
## Creating a space


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Create space**.

4. In the **Create space** dialog box, fill in the space information.

   
   |**Parameters** |**Description** |
   |---|---|
   |Project |Projects help you control access to BytePlus resources. You must affiliate the space to a project. To manage projects, visit the [Project management](https://console.byteplus.com/iam/projcetmanage/) page. |
   |Space name |The space name should be unique under the current account. We recommend that you use a name that clearly identifies your business. The length of the space name should be from 3 to 40 characters. Supported characters include: lowercase letters, numbers, and dash (\-). The space name must start and end with lowercase letters or numbers. |
   |||
   |||
   |Regions |Currently, you can only choose **Singapore**. |
   |Description |The space description can indicate the purpose of the space. For example, a space can be used for testing. The length of the space description should be less than 140 characters. |
   |Creator |The name of the space creator, which is the current account by default. |
   

5. Click **Create**.

6. (Optional) Click the **More** button in the upper right corner of the space card to see or edit space information, including the space region, create time, creator, and space description.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1c0b94b67d04d4f94012ad519a33c28~tplv-goo7wpa0wc-image.image) </span>


<span id="44250e2f"></span>
## Next steps

After creating a space, you can click **Enter space** to enter the space and perform other operations, such as uploading and processing media files, adding domain names. For details, see the following articles:


* [Media upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload)

* [Media processing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-processing)

* [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management)
