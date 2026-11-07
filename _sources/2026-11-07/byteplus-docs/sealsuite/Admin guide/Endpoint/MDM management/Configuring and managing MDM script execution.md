---
title: "Configuring and managing MDM script execution"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-and-managing-mdm-script-execution"
---

To achieve fine\-grained management and tailored control over mobile devices in your corporate, you can use the MDM script execution feature to write and deploy customized scripts. This guide provides step\-by\-step instructions for adding scripts from scratch or templates, managing their configurations, and monitoring execution jobs across macOS, Windows, and Linux platforms.

<span id="857bf170"></span>
## Feature Overview

The MDM script execution feature allows you to write and deploy customized scripts to achieve fine\-grained management and tailored control over mobile devices. SealSuite provides a comprehensive **Template Library** that covers various administrative scenarios, including system maintenance, hostname configuration, user permission setup, security patching, remote access control, service management, location services, network settings, device locking, and user logout.

<span id="ca947ea6"></span>
## Adding a Script

By adding scripts, administrators can enforce unified management standards and operational consistency across all organizational devices, significantly enhancing the security of the IT environment.


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Scripts**.

3. You can add a script using one of the following methods:

   * **Method 1: Create from Scratch**: In the **Configurations** tab, click  **+ Create** and select the target platform: **macOS**, **Windows**, or **Linux**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3225ddea4924838a13269316c4bbf02~tplv-goo7wpa0wc-image.image) </span>

   * **Method 2: Use a Template**: Click the **Template** tab, find the required template, and click **Use**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd4be7d26a574e608357ec1ac92a79dd~tplv-goo7wpa0wc-image.image) </span>

4. Configure the script parameters as described below:

   
   |Section |Parameter |Required |Description |
   |---|---|---|---|
   |**General Info** |**Name** |Yes |A unique identifier for the script (up to 50 characters). |
   ||**Description** |No |Administrative notes for the script. |
   |**Script Configuration** |**Script Content** |Yes |The actual payload of the script. You can write a **Custom Script** directly in the editor or click **Import from Templates** to select a pre\-configured script based on type tags. |
   ||**Timeout** |Yes |The maximum duration (60–3600 seconds) allowed for execution before the process is forcibly terminated. |
   ||**Script Signature** |Yes |Required if **Security Check** is enabled. You must enter your **Private Key** and click **Generate Signature** to ensure script integrity. |
   |**Scope** |**Assignment** |Yes |Specify the target audience by **User** (Department/Role) or **Device** (Group/ID). |
   ||**Exclude object** |No |Define specific exceptions within the assigned scope. |
   

5. After configuration, click **Complete** to save the script as a draft, or click **Complete and Execute** to deploy the script to the target scope immediately.


<span id="efc6ebdb"></span>
## Managing Scripts

Managing scripts involves maintaining and updating existing code, adjusting target scopes, and manually triggering executions to meet evolving organizational needs.


1. In the Admin Console, navigate to **Endpoint** \> **MDM** \> **Scripts** \> **Configurations**.

2. Use the search bar to filter by **Operating System** or **Script Name/Description**.

3. Perform the following actions:

   * **Run Script**: Click **Execute** next to a script to trigger its deployment immediately.

   * **Edit Script**: Click **Edit** to modify basic information, script payload, or target assignments.

      *Note: Modified scripts must be manually re\-executed to apply the changes to devices.* 

   * **Delete Script**: Click **Delete** to permanently remove the script configuration.


<span id="684c4039"></span>
## Managing Script Tasks

Task management allows you to monitor, optimize, and audit the execution process. You can track progress, analyze results, or terminate unnecessary tasks.


1. In the Admin Console, navigate to **Endpoint** \> **MDM** \> **Scripts** \> **Jobs**.

2. Filter the task list by **Operating System**, **Execution Status** (In Progress, Canceled, or Completed), or **Name**.

3. Perform the following actions:

   * **Monitor Execution**: Click **View** to see the **Execution Status** (success/failure rates) and the **Script Configuration**. You can **Refresh** the data or **Export** the device compliance list.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/218b82cd85b64b0792fba7d14297173a~tplv-goo7wpa0wc-image.image) </span>

   * **Drill\-down into Device Logs**: Click a **Device Name** to view its specific information. Under the **MDM** \> **Scripts** tab of the device details, you can view every script execution record for that specific device.

   * **Terminate Tasks**: Click **Cancel Job** for any task currently in the **In Progress** state to abort the deployment.
