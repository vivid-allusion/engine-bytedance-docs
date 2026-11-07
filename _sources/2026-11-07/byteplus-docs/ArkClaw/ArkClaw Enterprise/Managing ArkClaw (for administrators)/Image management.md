---
title: "Image management"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Image_management"
---

A custom image is the "custom instance blueprint" of ArkClaw Enterprise. It encapsulates base images, plugins, skills, personas, and configuration files into reusable templates. Enterprise administrators can create, copy, edit, and manage custom images. Employees can create or update Claw instances based on visible custom images.

<span id="FMMB6oeO"></span>
## Operation instructions


* **Configuration instructions**

   * By default, an ArkClaw space allows the creation of **200** custom images, and each employee Claw can create 10 custom images. To request a quota increase, contact your account manager.

   * The difference between an image and a [template](https://docs.byteplus.com/en/docs/ArkClaw/Managing_templates) is that an image includes complete runtime configuration and can be built via **YAML**, while a template is only used as a deployment script.

   * The visibility scope of a custom image is determined by the "Permission scope" parameter specified by administrators during image creation. The default value of this parameter is "Allow all", which means that the image is visible and available to all enterprise employees. Administrators can adjust the visibility scope at any time via "Manage assignees". Enterprise employees can modify information about a custom image, such as the name and description, in a Claw instance.

* **Description**

   * **Create custom images** allows administrators to build one from scratch. Administrators can preset base images, plugins, skills, personas, and configurations via a form or YAML, as optional templates for employees.

   * **Copy custom image** allows administrators to quickly generate a new image based on an existing custom image. The source image's configuration is automatically copied during the copying process. You can modify it as needed without starting from scratch. The new image created by copying is completely independent from the source image. Future changes, releases, or deletions on either side do not affect the other.

   * **Markdown (MD) configuration files** are used to manage system settings, personas, identity info, and user configurations for images. When creating a custom image or creating one by copying, you can view and modify specified MD configuration files. This makes the image better fit internal use cases and management policies.


<span id="ecMeMTQj"></span>
## Create a custom image

<span id="VExt5Azw"></span>
### Scenarios

When an enterprise needs to provide uniform initial configurations for employee Claw instances, a custom image is an appropriate option. Custom images can be built based on preset base images, plugins, skills, environment variables, personas, and configuration files. They are suitable for providing standardized Claw environments for different departments, roles, or business lines, turning commonly used plugins, skills, and configurations into reusable templates, and centrally managing the range of images that employees can select when creating Claw instances.

<span id="McLY46vi"></span>
### Prerequisites

User/department import has been completed. To distribute images based on department, you need to configure the department structure in advance. For detailed operations, see [Managing user groups](https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information?lang=zh#y6R20v3x) and [Managing departments](https://docs.byteplus.com/en/docs/ArkClaw/Managing_departments?lang=zh).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature is currently in Beta and is only visible and usable after activation. If needed, contact your account manager to request access.</div>


<span id="aSqV62ZJ"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Image Management".

3. Click the "Create image" button. See the table below and select a method to configure the image information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The form configuration method is suitable for non\-technical users. The YAML configuration method is suitable for technical users familiar with the Image Builder process and lets you quickly build custom images by orchestrating components, scripts, and test steps in declarative YAML.   </div>
   

   
   <Tabs>
   <Tab zoneid="FyVA3mRIzT" title="Form">
   <TabTitle>Form</TabTitle>
   
   
   |**Parameter​**  |**Description** |
   |---|---|
   |Configuration method |Select the configuration method of the custom image. In this case, select **Form**. |
   |Term |Enter the custom image name. |
   |Description |Enter the description of the image. We recommend that you describe the applicable scenarios and scope of the image for easier identification, management, and use. |
   |Image version |Displays the latest public image version (for display only). You can click to view version baseline details.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Enterprise administrators can view the latest public image version and update to the latest version under O&M \> Batch O&M \> Version management in the ArkClaw console.</div><br> |
   |Permission scope |Configure the permission scope of this image. The default is "Allow all".<br><br><br>* **Allow all**: The image is visible to and usable by all employees.<br><br>* **Controlled access**: This image is available to specified departments, user groups, or users. Only employees with permission can view and use it.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The image is invisible to and unusable by any employees. |
   |Markdown configuration |Supplement or replace Markdown configuration content for the custom image. You can select different methods to manage the Markdown content of the current image based on your configuration requirements.<br><br><br>* **MD configuration instructions**<br><br>   * **Append content**: Adds enterprise‑customized content to the base image's existing MD configuration. If nothing needs to be added, no modification is required, and the base image's original settings remain unchanged. This applies when you want to supplement enterprise‑specific role settings, rules, or preferences while inheriting the base image's capability baseline.<br><br>   * **Overwrite all**: Loads the base image's MD configuration into the editor. You can modify it directly, or delete everything and rewrite it from scratch. After saving, the final content in the editor takes effect. The base image's original configuration is no longer retained. This applies to scenarios where comprehensive customization of the MD configuration is required.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Before choosing this method, <strong>ensure the custom content covers key rules from the original configuration</strong>. Otherwise, style consistency and proactive problem‑solving capability may decline, and rules such as prompt injection protection, privacy protection, and sensitive operation confirmation may also fail.      </div><br>      <br><br>* **MD content description**<br><br>   * **Professional soul (SOUL.md)** : Configures Claw's core role settings, including professional positioning, working methods, behavioral principles, and long‑term stable system rules. This file determines Claw's overall role style and basic behavioral boundaries. Enterprise administrators can use it to preset a unified soul configuration for the image.<br><br>   * **Platform guidelines (AGENT.md)** : It is a system‑level specification preset by the platform. It includes security rules such as prompt injection protection, privacy protection, and sensitive operation confirmation.<br><br>   * **User information (USER.md)** : Presets personalized information on the user side, including work scenarios, communication preferences, and long‑term usage habits. The appended content is written to the image's user profile. It affects Claw's interaction style and output style toward the user.<br><br>   * **Identity information (IDENTITY.md)** : Defines Claw's identity positioning, including target roles, organizational affiliation, suitable and unsuitable scenarios, and behavioral decision boundaries. The appended content is written to the image's identity configuration. It affects Claw's self‑perception and scenario adaptation capability. |
   |Built\-in plugin |The plugins of the current public image are displayed by default. You can select or unselect the relevant plugins based on your business requirements. If the plugins of the public image cannot meet your requirements, click "Custom plugins‌" at the bottom of the drop\-down list to add custom plugins.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Custom plugins can be specified using one of the two source types: NPX or a download address.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>NPX</strong>: The NPM package name and plugin name that can be pulled via NPX must be provided.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Download address</strong>: A publicly accessible resource download URL must be provided (TOS and other object storage URLs are supported). The plugin name is also required.</div><br> |
   |Built\-in skills |Select the skills pre\-installed in the image. You can add enterprise\-specific skills, preset skills, and public skills.<br><br><br>* **Skill type**<br><br>   * **Enterprise\-specific skills**: Enterprise\-uploaded specific skills. To use enterprise\-specific skills, create a space and upload them to it first. For detailed instructions, see [Managing skills](https://docs.byteplus.com/en/docs/ArkClaw/Managing_skills).<br><br>   * **Public skills**: Public skills in Skill Center \> SkillHub.<br><br>   * **Preset skills**: Basic skills preset by the platform.<br><br>* **Procedure**:<br><br>   1. In the built\-in skills section, click the icon on the right to expand the skill details page.<br><br>   2. Select "Enterprise\-specific", "Public skills", or "Preset skills", and enable the target skill under the corresponding tab. |
   |Custom initialization script |Configure the `Linux Shell` command to be automatically executed when the image starts. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="GpoGe0XaON" title="YAML">
   <TabTitle>YAML</TabTitle>
   
   
   |**Parameter​**  |**Description** |
   |---|---|
   |Configuration method |Select the configuration method of the custom image. In this case, select **YAML**. |
   |Image version |Displays the latest public image version (for display only). You can click to view version baseline details.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Enterprise administrators can view the latest public image version and update to the latest version under O&M \> Batch O&M \> Version management in the ArkClaw console.</div><br> |
   |Permission scope |Configure the permission scope of this image. The default is "Allow all".<br><br><br>* **Allow all**: The image is visible to and usable by all employees.<br><br>* **Controlled access**: This image is available to specified departments, user groups, or users. Only employees with permission can view and use it.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the effective scope is set to "All employees, Department, or User group", newly added members will automatically inherit this permission rule.   </div><br>   <br><br>* **Deny all**: The image is invisible to and unusable by any employees. |
   |YAML configuration |Select an existing custom image and directly import its YAML configuration. |
   |YAML |Configure the professional soul (SOUL.md), built\-in plugins, built\-in skills, and platform specification (AGENT.md) of the current image.<br><br>**Configuration example**:<br><br>```Python```<br>```name: DocTest```<br>```description: "YAML Image Creation Test"```<br>```plugins:```<br>```    - id: agent-identity-plugin```<br>```      name: agent-identity-plugin```<br>```      display-name: agent-identity-plugin```<br>```      source: ""```<br>```      blacklist: false```<br>```      type: built-in```<br>```      description: ""```<br>```      version: 0.8.3```<br>```    - id: dingtalk-connector```<br>```      name: dingtalk-connector```<br>```      display-name: DingTalk Channel```<br>```      source: ""```<br>```      blacklist: false```<br>```      type: built-in```<br>```      description: Official OpenClaw DingTalk channel plugin```<br>```      version: 0.8.20```<br>```skills:```<br>```    - name: byted-seedance-video-generate```<br>```      display-name: "U0001F4E6 byted-seedance-video-generate"```<br>```      description: Generate videos```<br>```      blacklist: false```<br>```      slug: ""```<br>```      type: built-in```<br>```    - name: byted-seedream-image-generate```<br>```      display-name: "U0001F4E6 byted-seedream-image-generate"```<br>```      description: Generate high-quality```<br>```      blacklist: false```<br>```      slug: ""```<br>```      type: built-in```<br>```soul: "IyBTT1VMCllvdSBhcmUgYSByZWxpYWJsZSBlbnRlcnByaXNlIGFzc2l****"```<br>```agents: "IyBBR0VOVApGb2xsb3cgdGhlIHBsYXRmb3JtIHJ1bGV****"```<br><br><br> |
   
   
   
   
   
   </Tab>
   </Tabs>
   

4. After the configuration is complete, click "Confirm" to create a custom image. Enterprise administrators can modify its permissions at any time. For details, see [Managing assignees](https://docs.byteplus.com/en/docs/ArkClaw/Image_management?lang=en#GYxrLDxS).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After an image is created, if the administrator updates the skills added within the image, the changes only take effect for Claw instances subsequently created from that image. Existing Claw instances are not affected.   </div>
   

<span id="K8lZga1P"></span>
## Copying custom images

<span id="ZjBDqvcQ"></span>
### Scenarios

Creating by copying applies to scenarios where you want to reuse an existing custom image configuration rather than modifying the original image directly. For example, you can create an image with a similar configuration for another department based on a department's standard image, or fine\-tune plugins, skills, personas, or configuration files based on an existing image to create an independent version for canary testing or scenario isolation, or explore new configuration combinations while keeping the original image stable and available.

Creating by copying is not an update to the original image, nor a version branch. **The copied image is a new and independent custom image**. The original image and the copied one are independent of each other. Future editing, publishing, or deleting either one does not affect the other.

<span id="EoqUHqGf"></span>
### Prerequisites

An existing copyable custom image is required, meaning the [Create custom image](https://docs.byteplus.com/en/docs/ArkClaw/Image_management) operation has been completed.

<span id="Zht2yB3z"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Image management". In the image list, click the name of the image to be copied.

3. On the image details page, click "Copy image" in the upper\-right corner. See [Create custom images](https://docs.byteplus.com/en/docs/ArkClaw/Image_management) to modify the image configuration, and click "Confirm" to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system copies both the <strong>form configuration</strong> and the <strong>YAML configuration</strong> from the source image. You can select either method to configure the custom image.   </div>
   

<span id="JNFMdA3W"></span>
## Edit a custom image

<span id="iUD30uIl"></span>
### Scenarios

When an enterprise needs to adjust the name, description, or permission scope of an existing custom image, editing the custom image is an appropriate option.  After the image is created, its core configurations (such as the professional souls, plugins, and skills) are fixed. You can only modify the name, description, and permission scope. To change the core configuration, we recommend creating a new custom image.

<span id="4JhIEDvj"></span>
### Prerequisites

An existing custom image to be edited is required, meaning the [Create custom image](https://docs.byteplus.com/en/docs/ArkClaw/Image_management) operation has been completed.

<span id="XuxQJTSq"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Image Management".

3. In the image list, find the target image and click the "Edit" button in the Actions column.

4. In the edit pop\-up window, modify the image's name, description, and permission scope.

5. After modification, click "Confirm" to complete the operation.


<span id="GYxrLDxS"></span>
## Manage assignees

<span id="tt40wX5u"></span>
### Scenarios

After a custom image is created, it is visible only to employees with the appropriate permissions. When a custom image is intended only for certain employees, departments, or project members, you can control its visibility by managing the distribution scope. For example, distributing a data analysis image to the data team, a development aid image to the R&D team, or making a new image available only to designated employees during canary testing.

**Assignee settings only affect whether employees can view and use the image**. They do not modify the image's own configuration content. Employees with permission can select this image when creating Claw instances. Those without permission cannot see it in the available image list.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After removing an assignee, Claw instances already created from that image will remain unaffected and usable, but that image can no longer be used to create new Claw instances.</div>


<span id="acmCP15C"></span>
### Prerequisites

An existing custom image whose assignees need to be managed is required, meaning the [Create custom image](https://docs.byteplus.com/en/docs/ArkClaw/Image_management) operation has been completed.

<span id="yKgB5y33"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Image Management".

3. In the image list, click the target image name.

4. On the "Assignees" tab, click the "Manage assignee" button.

5. Manage assignees. Click "Confirm" when you complete management operations.

   * **Add assignee**: On the "Manage Assignees" page, select the permission scope. If "Controlled access" is chosen, you also need to select the target employees or departments.

   * **Remove assignee**: On the "Manage Assignees" page, click the "Remove" button in the Actions column of the target employee or department.


<span id="fXXpWMDB"></span>
## Delete custom image information

<span id="d1MjHsOS"></span>
### Scenarios

When a custom image configuration is no longer applicable, duplicates exist, or it has been replaced by a new image, you can delete that custom image. **Before deletion, we recommend checking whether the image is still in use by employees to avoid affecting subsequent Claw instance creation**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The impacts of deleting an image are as follows:</div>



* <div data-tips="true" data-tips-type="warning">The image will become unavailable and <strong>unrecoverable</strong>. Existing Claw instances created from this image can be used as expected<strong>.</strong></div>


* <div data-tips="true" data-tips-type="warning">Claw instances created from this image will <strong>not be able to restore factory settings</strong>. For related descriptions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restore_Claw_instance_to_factory_settings">Restoring Claw instances to factory settings</a>.</div>



<span id="dT2u5OmY"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Image Management".

3. In the image list, find the target image and click the "Delete" button in the Actions column.

4. In the confirmation pop\-up window, after verifying the information, click the "Confirm" button to complete the operation.
