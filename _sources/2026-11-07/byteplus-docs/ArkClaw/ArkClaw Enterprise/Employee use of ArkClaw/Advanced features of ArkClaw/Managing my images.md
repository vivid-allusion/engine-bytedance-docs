---
title: "Managing my images"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_my_images"
---

An image is a "custom instance blueprint" for ArkClaw Enterprise. In the "My images" panel, you can view custom images created by your administrator. You can also build reusable custom images based on BytePlus's official public images by presetting the professional soul, platform specifications, built\-in plugins, built\-in skills, and initialization startup commands. When you [create a Claw instance](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_), you can select an image that you are authorized to use to inherit its capabilities and avoid repetitive configurations.

<span id="3YTAvGnt"></span>
## Operation instructions


* **Configuration instructions**

   * Each employee can create up to 10 custom images by default. To increase the quota, contact your enterprise administrator.

   * The difference between images and [Claw templates](https://docs.byteplus.com/en/docs/ArkClaw/Managing_templates) is that images contain complete runtime configuration and support **YAML** build, while Claw templates are only used as deployment scripts.

   * Images created by enterprise employees are only available for their own use. To share an image with other enterprise employees, contact the enterprise administrator to configure the [deployment scope of the image](https://docs.byteplus.com/en/docs/ArkClaw/Image_management#GYxrLDxS).

* **Description**

   * **Creating a custom image ** allows an employee to build a custom image from scratch. Through form\-based configuration or YAML orchestration, the employee can preset base images, plugins, skills, personas, and configurations as an optional template for creating Claw instances.

   * **Copying custom images ** allows enterprise employees to quickly generate a new image based on an existing custom image. The source image's configuration is automatically copied during the copying process. You can modify it as needed without starting from scratch. The new image created by copying is completely independent from the source image. Future changes, releases, or deletions on either side do not affect the other.

   * **Markdown (MD) configuration files** are used to manage system settings, personas, identity info, and user configurations for images. When creating a custom image or creating one by copying, you can view and modify specified Markdown configuration files. This helps the image better fit internal use cases and management policies.

   * **The "My images" section only displays ** images created by employees themselves. Images distributed by enterprise administrators (the image\-based templates from preset Claw templates on the Claw creation page) can only be used for Claw creation.


<span id="gal5D04P"></span>
## View my images


1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target ArkClaw page and click the details icon in the upper\-right corner.

3. Click the "My images" button.

4. In the "My images" pane, you can view all available images.

5. Click the “Details” button on the target card to view the details of this image. The details include the image version, soul settings, built\-in plugins and skills, and more.

6. (Optional) Click “Use image to create Claw” on the target card to navigate to the creation page and [create a Claw instance](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_) based on this image.


<span id="3mReFN7p"></span>
## Create a custom image

<span id="tWAwTD4m"></span>
### Scenarios

When the preset Claw templates cannot meet your requirements, such as when you need to provide a standardized Claw environment for a specific role, business line, or team, you can create a reusable custom image based on a public image. By using ** form\-based configuration ** or **YAML orchestration**, you package the base image, plugins, skills, environment variables, personas, and configuration files into this image.

<span id="zxsxLMjJ"></span>
### Procedure


1. In the "My images" pane, click the “Create” button.

2. Refer to the following tables and choose a method to configure the image.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The form and YAML configuration methods are mapped to each other and can be switched at any time. Changes to either method are automatically synchronized to the other.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The YAML configuration method is suitable for technical users familiar with the Image Builder process. It allows you to quickly build custom images by orchestrating components, scripts, and test steps using declarative YAML.   </div>
   

   
   <Tabs>
   <Tab zoneid="kLLNsqZV2Q" title="Form">
   <TabTitle>Form</TabTitle>
   
   
   |**Parameter​**  |**Description** |
   |---|---|
   |Configuration method |Select the configuration method of the custom image. In this case, select **Form**. |
   |Term |Enter the custom image name. |
   |Description |Enter the description of the image. We recommend that you describe the applicable scenarios and scope of the image for easier identification, management, and use. |
   |Image version |Displays the latest public image version (for display only). You can click to view version baseline details. |
   |Markdown configuration |Supplement or replace Markdown configuration content for the custom image. You can select different methods to manage the Markdown content of the current image based on your configuration requirements.<br><br><br>* **MD configuration insructions**<br><br>   * **Append content**: Adds enterprise‑customized content to the base image's existing MD configuration. If nothing needs to be added, no modification is required, and the base image's original settings remain unchanged. This applies when you want to supplement enterprise‑specific role settings, rules, or preferences while inheriting the base image's capability baseline.<br><br>   * **Overwrite all**: Loads the base image's MD configuration into the editor. You can modify it directly, or delete everything and rewrite it from scratch. After saving, the final content in the editor takes effect. The base image's original configuration is no longer retained. This applies to scenarios where comprehensive customization of the MD configuration is required.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Before choosing this method, <strong>ensure the custom content covers key rules from the original configuration</strong>. Otherwise, style consistency and proactive problem‑solving capability may decline, and rules such as prompt injection protection, privacy protection, and sensitive operation confirmation may also fail.      </div><br>      <br><br>* **MD content description**<br><br>   * **Professional soul (SOUL.md)** : Configures Claw's core role settings, including professional positioning, working methods, behavioral principles, and long‑term stable system rules. This file determines Claw's overall role style and basic behavioral boundaries. Enterprise administrators can use it to preset a unified soul configuration for the image.<br><br>   * **Platform guidelines (AGENT.md)** : It is a system‑level specification preset by the platform. It includes security rules such as prompt injection protection, privacy protection, and sensitive operation confirmation. |
   |Built\-in plugin |This parameter is required only when the "Configuration method" is "Form".<br><br>The plugins of the current public image are displayed by default. You can select or unselect the relevant plugins based on your business requirements. If the plugins of the public image cannot meet your requirements, click "Custom plugins‌" at the bottom of the drop\-down list to add custom plugins.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Custom plugins can be specified using one of the two source types: NPX or a download address.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>NPX</strong>: The NPM package name and plugin name that can be pulled via NPX must be provided.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Download address</strong>: A publicly accessible resource download URL must be provided (TOS and other object storage URLs are supported). The plugin name is also required.</div><br> |
   |Built\-in skills |This parameter is required only when the "Configuration method" is "Form". Select the skills pre\-installed in the image. You can add enterprise\-specific skills, preset skills, and public skills.<br><br><br>* **Skill type**<br><br>   * **Enterprise\-specific skills**: Skills uploaded by enterprise administrators.<br><br>   * **Public skills**: Public skills in Skill Center \> SkillHub.<br><br>   * **Preset skills**: Basic skills preset by the platform.<br><br>* **Procedure**:<br><br>   1. In the Built\-in skills section, click "Manage skills".<br><br>   2. On the skill details page that appears, select "Enterprise\-specific", "Public skills", or "Preset skills", and enable the target skill under the corresponding tab. |
   |Custom initialization script |This parameter is required only when the "Configuration method" is "Form". Configure the `Linux Shell` command to be automatically executed when the image starts. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="LckPYuSnqu" title="YAML">
   <TabTitle>YAML</TabTitle>
   
   
   |**Parameter​**  |**Description** |
   |---|---|
   |Configuration method |Select the configuration method of the custom image. In this case, select **YAML**. |
   |Image version |Displays the latest public image version (for display only). You can click to view version baseline details. |
   |Base image |Supports importing a JSON file based on an existing image for continuous iteration. |
   |YAML |Configure the professional soul (SOUL.md), built\-in plugins, built\-in skills, and platform specification (AGENT.md) of the current image.<br><br>**Configuration example**:<br><br>```Python```<br>```name: DocTest #Required. The name of the image (4-64 characters).```<br>```description: "YAML Image Creation Test" #Optional. The description of the image (0-200 characters).```<br>```# Optional. The list of plugin configurations.```<br>```plugins:```<br>```    - id: agent-identity-plugin```<br>```      name: agent-identity-plugin```<br>```      display-name: agent-identity-plugin```<br>```      source: ""```<br>```      blacklist: false```<br>```      type: built-in```<br>```      description: ""```<br>```      version: 0.8.3```<br>```    - id: dingtalk-connector```<br>```      name: dingtalk-connector```<br>```      display-name: DingTalk Channel```<br>```      source: ""```<br>```      blacklist: false```<br>```      type: built-in```<br>```      description: Official OpenClaw DingTalk channel plugin```<br>```      version: 0.8.20      ```<br>```# Optional. The list of skill configurations.```<br>```skills:```<br>```    - name: byted-seedance-video-generate```<br>```      display-name: "U0001F4E6 byted-seedance-video-generate"```<br>```      description: Generate videos```<br>```      blacklist: false```<br>```      slug: ""```<br>```      type: built-in```<br>```    - name: byted-seedream-image-generate```<br>```      display-name: "U0001F4E6 byted-seedream-image-generate"```<br>```      description: Generate high-quality```<br>```      blacklist: false```<br>```      slug: ""```<br>```      type: built-in```<br>```# Optional. The soul configuration. The value is Base64-encoded and can be up to 5 KB in size.```<br>```soul-md:" c291bC1tZGFyayBLomNvZGVkIGNVbn****"```<br>```# Optional. The agent configuration. The value is Base64-encoded and can be up to 5 KB in size.```<br>```agent-md: "YwdlbnQgbWQgYmFzZTYOIGVuY29kZWQgY29udG****"```<br>```# Optional. The startup script for the instance. The value is Base64-encoded and can be up to 12 KB in size.```<br>```build-script: "aW5pdCBzY3JpcHQgYmFzZTYOIGVuY****"```<br><br><br> |
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. After configuration, click the "Create" button to complete image creation.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After an image is created, if the skills added within the image are updated, the changes only take effect for Claw instances subsequently created from that image. Existing Claw instances are not affected.   </div>
   

<span id="GjKr8eeB"></span>
## Copying custom images

<span id="fl5cK2zK"></span>
### Scenarios

Creating by copying applies to scenarios where you want to reuse an existing custom image configuration rather than modifying the original image directly. For example, creating a similar image for another department based on a standard image, by fine\-tuning plugins or configs to create a new independent version for canary testing, or exploring new configurations while keeping the original stable.

Creating by copying is not an update to the original image, nor a version branch. **The copied image is a new and independent custom image**. The original image and the copied one are independent of each other. Future editing, publishing, or deleting either one does not affect the other.

<span id="90gnRacC"></span>
### Prerequisites

An existing copyable custom image is required, meaning the [Create custom image](https://docs.byteplus.com/en/docs/394/108408#3mReFN7p) operation has been completed.

<span id="O1URiwCV"></span>
### Procedure


1. In the "My images" pane, click the "Details" button on the target agent image card.

2. Select **YAML view**, and in the **YAML information** module, click the "Copy and create" button.

3. In the image creation dialog box that pops up, refer to [Creating custom images](https://docs.byteplus.com/en/docs/394/108408#3mReFN7p) to modify the image configuration, and click "Confirm" to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system copies both the <strong>form configuration</strong> and the <strong>YAML configuration</strong> from the source image. You can select either method to configure the custom image.   </div>
   

<span id="5eCdLPgk"></span>
## Edit a custom image

<span id="SULxoD0H"></span>
### Scenarios

When you need to adjust the name, description, or permission scope of an existing custom image, you can edit the custom image. After an image is created, its core configuration (e.g., soul for role, plugins, and skills) is fixed. The edit operation only supports modifying the name and description. To change the core configuration, create a new custom image.

<span id="NvQVytbV"></span>
### Prerequisites

An existing custom image to be edited is required, meaning the [Create custom image](https://docs.byteplus.com/en/docs/394/108408#3mReFN7p) operation has been completed.

<span id="CPyHsIL5"></span>
### Procedure


1. In the "My images" pane, locate the target image and click "Edit".

2. In the Edit dialog box, modify the image name and description.

3. After modification, click the "Confirm" button to complete the edit.


<span id="doMGdCwp"></span>
## Delete a custom image

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deletion, this image can no longer be used for<a href="https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_"> creating Claw instances </a>and cannot be restored. Claw instances created based on this image no longer support <strong>restoring factory settings</strong>. Proceed with caution.</div>



1. In the "My images" pane, locate the target image and click "Delete".

2. In the confirmation pop\-up window, confirm the information and click the "Delete" button to complete the deletion.
