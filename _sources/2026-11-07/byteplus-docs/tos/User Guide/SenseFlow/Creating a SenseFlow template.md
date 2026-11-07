---
title: "Creating a SenseFlow template"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-template"
---

A SenseFlow template is an essential component of a SenseFlow rule. When creating a rule, you must associate it with a template. SenseFlow provides preset templates for intelligent security and media asset management, allowing you to quickly implement smart capabilities. For more information, see [Preset templates](https://docs.byteplus.com/en/docs/tos/Preset-templates).

You can also create custom templates to meet your business's specific needs. This topic describes how to use SenseFlow custom templates and their limitations.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">SenseFlow is currently in closed beta and is only available in China (Beijing). Please contact your account manager for access.</div>


<span id="4Po6sdvU"></span>
## Prerequisites


|Category |Description |
|---|---|
|Account registration and real name verification |Make sure that you have created a BytePlus account and completed real name verification. For more information, see [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/Account/sign-up-and-verify-byteplus-account?redirect=1). |
|Activating TOS |Make sure that you have [activated TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1) for your account or Identity and Access Management users. |
|Adding a workflow to your custom template |You must add at least one workflow to your custom template. Create a workflow that meets your needs in advance. For more information, see [Creating a SenseFlow workflow](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-workflow). |


<span id="HbVKIxHH"></span>
## Notes

The first time you use SenseFlow, you must obtain the necessary permissions. Click **To authorize** to enable access to the data processing feature and Key Management Service (KMS) **,**  and to create the following IAM roles: `ServiceRoleforTOSDataProcess` and `ServiceRoleforTOSSenseflow`.

<span id="p2n42lIS"></span>
## Creating a custom template


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Content perception and processing \> Template management**.

3. On the **Template management** page, click **Create custom templates** or  **+ Custom template**.

4. On the **Create custom templates** page, configure the following parameters.

   
   |Parameter | |Description |
   |---|---|---|
   |Basic information |Template name |Enter a name for the custom template. |
   ||Describe |Provide additional information about the template. The description cannot exceed 50 characters. |
   |Workflow settings |Select workflow |Select or view one or more workflows.<br><br><br>* To add a workflow:<br><br>   Click **Add workflow** to select a workflow in the **Add workflow** panel. If no suitable workflow is available, click **Create workflow** to make a new one.<br><br>* To view workflow details:<br><br>   Navigate to the **Add workflow** page, and click **View details** in the **Actions** column of a workflow to view its details. For more information, see [Creating a SenseFlow workflow](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-workflow). |
   

5. Once you have finished configuring, click **Select**.


<span id="PMHB964C"></span>
## Viewing template details


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Content perception and processing** \> **Template management**.

3. On the **Template management** page, find the template you want to check and click **Details** on its card.

4. On the **Template details** page, you can view its basic information, workflows, video summary, and other details.
