---
title: "Manage Functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-create-function"
---

This document describes how to create, publish, and delete functions.

<span id="create-a-function"></span>
## Create a function

Before editing code in Edge Functions, you need to create a function first.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each BytePlus account can create a maximum of 100 functions.</div>


<span id="steps"></span>
### Steps

Follow these steps to create a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Functions** page, click **Create function**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1c92cd1cd884f17756eeec88002f7e8e.jpeg) </span>

3. On the **Create function** page, configure the parameters according to the following instructions.

   
   |Parameter |Description |
   |---|---|
   |Name |Function name. The function name must be unique within each BytePlus account.<br><br>The rules for the name are as follows:<br><br><br>* Supports uppercase letters, lowercase letters, numbers, and hyphens (\-).<br><br>* Length should not exceed 128 characters. |
   |Description |Optional. Description of the function. Maximum 128 characters allowed. |
   |Project |The project to which the function belongs. |
   |How to create |The method of creating the function.<br><br><br>* No template: Start creating a function from a "helloworld" example.<br><br>* Create with a template: Select a sample code template to quickly create a function. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0be2841f477c574077cf69d29339d214.jpeg) </span>

4. Click **Save**. The function you created will be displayed on the **Functions** page.


<span id="publish-a-function"></span>
## Publish a function

After you publish a function, it can be deployed on edge nodes.

<span id="steps"></span>
### Steps

Follow these steps to publish a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page. Find the function you want to publish and click on the function name.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1c92cd1cd884f17756eeec88002f7e8e.jpeg) </span>

2. Click **Modify and deploy** in the **Code** tab.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_869cdf45d45bf711437ade4681dc70b9.jpeg) </span>

3. Click **Deploy** in the upper right corner of the page.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c5b1ba21b36ebce1d34cc53245e8d5ed.jpeg) </span>

4. In the pop\-up dialog box, fill in the **Description** information, select the release type, and click **OK** to complete the release.

   * Canary release: Publish the function to the canary nodes you specify. See [Canary Nodes](https://docs.byteplus.com/docs/byteplus-cdn/docs-canary-node).

   * Full release: Publish the function to all edge nodes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you use a domain trigger, you also need to add forwarding rules for the domain. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-domain-triggers">Domain Triggers</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Full release of a function generally takes 5 to 10 minutes. You must wait for the function to be fully released before you can associate a domain with it.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7af4479ac458616a4deff163cd2dbf27.jpeg) </span>


<span id="delete-a-function"></span>
## Delete a function

If you no longer need a function, you can delete it.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The function's code and configuration will all be deleted. Deleted functions cannot be recovered.</div>


<span id="prerequisites"></span>
### Prerequisites

The function is not associated with any domain. See [Domain Triggers](https://docs.byteplus.com/docs/byteplus-cdn/docs-domain-triggers).

<span id="steps"></span>
### Steps


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the function you want to delete, click **Delete** in the **Actions** column.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1c92cd1cd884f17756eeec88002f7e8e.jpeg) </span>

3. In the **Confirm Deletion** dialog box, check **Confirm delete**, then click the **Delete** button.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f73e0d28cebebf49279704207ac87702.jpeg) </span>
