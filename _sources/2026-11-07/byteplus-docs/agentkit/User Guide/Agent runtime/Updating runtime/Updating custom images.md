---
title: "Updating custom images"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_custom_images"
---

This topic describes how to update the version of a custom image.

<span id="3CZa8DiS"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. In non\-preview mode, you do not need to specify a version and can update directly.

* **Effective conditions**: After you update the image, the new configuration takes effect only after **republishing**, and a new version is generated simultaneously. Once published, the latest version is automatically used for subsequent agent runtime calls. [Viewing release records](https://docs.byteplus.com/en/docs/agentkit/Viewing_release_history)


<span id="qpeZioUi"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section of the **Configuration information** tab, locate **Image address** and click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span> icon next to it****.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

5. In the "Edit image" panel, choose either of the following methods to configure the image:

   * Click "Select from Container Registry" and select the target image.

   * Click "Enter a BytePlus image address" and enter the target image address.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you use an image from another account, make sure that the instance where the image is located has<a href="https://docs.byteplus.com/en/docs/cr/Enabling_public_network_access"> public network access enabled</a>. Otherwise, the image pull may fail, and the runtime deployment cannot be completed.   </div>
   

6. Click "Confirm" to save the draft configuration.

7. Publish the agent runtime to apply the new configuration:

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or[ publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Release" in the upper\-right corner of the page. The new configuration takes effect only after republishing.
