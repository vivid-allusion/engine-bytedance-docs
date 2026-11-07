---
title: "One-click integration with ArkClaw"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/One-click_integration_with_ArkClaw"
---

ArkClaw is a cloud\-based AI agent service provided by BytePlus. It helps you deploy OpenClaw on the cloud with just one click, eliminating complex configurations and supporting 24/7 online availability. This allows you to use OpenClaw with zero barriers, and seamlessly utilize your subscribed ModelArk Coding Plan / Agent Plan, freeing you from concerns about Pay\-as\-you\-go token billing.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can also use an application template to quickly deploy an <strong>ECS instance preinstalled with OpenClaw</strong> with simple configuration. In addition to using OpenClaw features, you can manage the ECS instance. For example, you can start and stop the instance, and upgrade the instance configuration. <a href="https://docs.byteplus.com/en/docs/ecs/Quickly_deploying_Moltbot_on_the_cloud_to_create_a_private_AI_assistant">Learn more</a>.</div>


<span id="RwGCSWnt"></span>
## Considerations


* If you have subscribed ModelArk [ Medium/Large/Max Medium/Large/Max](https://docs.byteplus.com/en/docs/82379/2366394?lang=en), you can use the relevant services provided by ArkClaw during the subscription validity period. When your **Agent Plan** expires, the ArkClaw you created will be suspended immediately. Your data will be **retained for 24 hours** and automatically deleted after this period. To continue using the service, click the "Continue to use" button and follow the on\-screen instructions to [activate ModelArk ArkClaw](https://docs.byteplus.com/en/docs/87732/2275195) or [renew Agent Plan](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&_vtm_=a106466.b106468.0_0.0_0.0.2024_7613594367911118351&advancedActiveKey=agentPlan).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You will not obtain entitled ArkClaw for free by subscribing to <strong>Agent Plan Small</strong>. You can <a href="https://docs.byteplus.com/en/docs/87732/2253818?lang=en#F0e9F6CX">purchase ArkClaw separately</a> based on your needs.   </div>
   

* You will not obtain entitled ArkClaw for free by subscribing to ModelArk Ark Coding Plan. ArkClaw instances that have been activated and are within the trial period can still be used.

   * Starting from **12:00 on May 18, 2026**, subscribers to the [Coding Plan Pro ](https://docs.byteplus.com/en/docs/ModelArk/1925114#2ee4a6ee)package will no longer be entitled to free ArkClaw trials. For detailed rules, please refer to [Announcement on termination of ArkClaw benefit campaign for Coding Plan Pro](https://docs.byteplus.com/en/docs/82379/2406398).

   * Starting from ** ** **16:00 on March 24, 2026**, new subscriptions to [Coding Plan Lite](https://docs.byteplus.com/en/docs/ModelArk/1925114#2ee4a6ee) will no longer include the 7\-day free trial of ArkClaw.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When your ArkClaw trial expires, the ArkClaw instance you created will not be available in ModelArk Playground, and its data will be <strong>retained for 24 hours</strong>. To continue using the service, click the "Continue to use" button and follow the on\-screen instructions to <a href="https://docs.byteplus.com/en/docs/87732/2275195">activate ModelArk ArkClaw</a> or upgrade Coding Plan to <a href="https://docs.byteplus.com/en/docs/82379/1925114#6e51df70"><strong>Coding Plan Pro</strong></a><strong>.</strong>   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The ArkClaw trial version provides only <strong>one conversation page</strong> and is suitable for quickly trying basic capabilities. To learn about or use advanced features, hover over "Official version" to view feature details, or click the "Go to the official version to unlock more capabilities" button to go to the ArkClaw console and access the full set of capabilities.   </div>
   


&nbsp;

<span id="4wBqL9tq"></span>
## Create and use ArkClaw

Use or create ArkClaw based on whether you have subscribed to ModelArk Agent Plan/Coding Plan.


<Tabs>
<Tab zoneid="SeP53yDaLn" title="ModelArk Agent Plan Subscribed">
<TabTitle>ModelArk Agent Plan Subscribed</TabTitle>

If you have subscribed to the ModelArk , you can use the relevant services provided by ArkClaw during the subscription validity period without additional payment or configuration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The ArkClaw obtained as a complimentary benefit from ModelArk Playground is the <strong>Starter</strong> edition, suitable for basic personal agent use and meeting preliminary exploration and usage needs. <a href="https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios">Learn more</a>.</div>


1. Log in to ModelArk [Playground > ArkClaw](https://console.byteplus.com/ark/region:ark+ap-southeast-1/experience).

2. In the left navigation pane, click "ArkClaw".

3. In the upper\-left corner of the page, select "Agent Plan" to start a conversation with ArkClaw in ModelArk.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can perform personalized configuration and management of ArkClaw by following the <a href="https://docs.byteplus.com/en/docs/ecs/One-click_integration_with_ArkClaw#NxLmzbFS">usage tips</a>, such as configuring the message channel, switching the model, and defining the soul.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">At the top of the chat interface, you can view the remaining available days of ArkClaw at any time.   </div>
   


</Tab>
<Tab zoneid="rh8NLaSEDp" title="ModelArk Agent Plan/Coding Plan expired or not subscribed">
<TabTitle>ModelArk Agent Plan/Coding Plan expired or not subscribed</TabTitle>

If you have not subscribed to ModelArk Agent Plan/Coding Plan, subscribing to ModelArk Agent Plan/Coding Plan is also required when you create an ArkClaw instance.


1. Log in to ModelArk [Playground > ArkClaw](https://console.byteplus.com/ark/region:ark+ap-southeast-1/experience).

2. In the upper\-left corner of the page, select "Coding Plan" or "Agent Plan" **.** 

3. Click the "Create now" button, choose to purchase ArkClaw separately or purchase a bundle as needed, and refer to the table below to configure the following parameters.

   * Bundle purchase: The bundle purchase includes ArkClaw and the Agent Plan/Coding Plan large model subscription package. This applies when the ModelArk Agent Plan/Coding Plan has expired.

   * Purchase ArkClaw separately: Purchasing ArkClaw separately (with an existing large model subscription package) applies to scenarios where you have already subscribed to a ModelArk Agent Plan/Coding Plan large model subscription package and the package is valid.

   
   |Configuration item |Description |
   |---|---|
   |Confirm specification |The ArkClaw you create in ModelArk Playground is the **Starter** edition, suitable for basic personal agent use and meeting preliminary exploration and usage needs. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios). |
   |Agent Plan/Coding Plan large model subscription |Select the Agent Plan/Coding Plan edition you want to subscribe to as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Configuration is required only for bundle purchase.</div><br><br><br><br>* **Agent Plan**<br><br>   * Small (Coding Plan Small): For medium\-intensity development tasks, suitable for most developers.<br><br>   * Medium (Coding Plan Medium): For complex project development, suitable for developers with high\-intensity workloads.<br><br>   * Large (Coding Plan Large): For ultra\-large projects, complex multi\-task collaboration and advanced intelligent business scenarios, suitable for professional teams and senior developers for in\-depth usage.<br><br>* **Coding Plan**<br><br>   * Lite: Coding Plan Lite, for medium\-intensity development tasks, suitable for most developers.<br><br>   * Pro: Coding Plan Pro, for complex project development, suitable for developers with high\-intensity workloads.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To learn more about the supported models, usage quotas, and other information of the Agent Plan package, see <a href="https://docs.byteplus.com/en/docs/82379/2366394?lang=en">Package overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To learn more about the supported models, usage quotas, and other information of the Coding Plan package, see <a href="https://docs.byteplus.com/en/docs/82379/1925114">Package overview</a>.</div><br> |
   |Subscription duration |Please select the subscription duration for the ArkClaw and Agent Plan/Coding Plan package as needed. |
   |Automatic renewal |Select whether to enable automatic renewal upon expiration.<br><br><br>* **Enable automatic renewal**: If automatic renewal is enabled, ArkClaw is automatically renewed for 1 month by default. When ArkClaw expires, the platform automatically deducts the fee for the next month of the current package, including ArkClaw and the Agent Plan or Coding Plan large model subscription package.<br><br><br> We recommend that you enable automatic renewal to prevent service suspension upon expiration and ensure uninterrupted usage.<br><br><br>* **Disable automatic renewal (default)** : If automatic renewal is not enabled, you can manually [renew ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Renewing_ArkClaw) after it expires.Manual renewal |
   |Service rules and related agreement |Read and agree to the related service rules and program agreement of ArkClaw, and then check "I have read and agree to the ArkClaw service rules and User Experience Improvement Program Agreement and ModelArk Coding Plan Promotion Rules and BytePlus Data Authorization Agreement". |
   

4. After confirming the information is correct, click the "Pay now" button to submit the purchase request.

5. On the payment page, confirm the order and amount information, select a payment method, and click "Pay now" to complete the payment.

6. After ArkClaw is created, you can chat with it in ModelArk.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can perform personalized configuration and management of ArkClaw by following the <a href="https://docs.byteplus.com/en/docs/ecs/One-click_integration_with_ArkClaw#NxLmzbFS">usage tips</a>, such as configuring the message channel, switching the model, and defining the soul.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">At the top of the chat interface, you can view the remaining available days of ArkClaw at any time.   </div>
   


</Tab>
<Tab zoneid="UskCwQfwop" title="ModelArk Coding Plan subscribed">
<TabTitle>ModelArk Coding Plan subscribed</TabTitle>

If you have subscribed to the ModelArk [Coding Plan Pro](https://docs.byteplus.com/en/docs/ModelArk/1925114#2ee4a6ee), you can use the relevant services provided by ArkClaw during the subscription validity period without additional payment or configuration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The ArkClaw you create in ModelArk Playground is the <strong>Starter</strong> edition, suitable for basic personal agent use and meeting preliminary exploration and usage needs. <a href="https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios">Learn more</a>.</div>


1. Log in to ModelArk [Playground > ArkClaw](https://console.byteplus.com/ark/region:ark+ap-southeast-1/experience).

2. In the upper\-left corner of the page, select "Coding Plan" **.** 

3. Click the "Create now" button to create ArkClaw.

4. After ArkClaw is created, you can chat with it in ModelArk.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can perform personalized configuration and management of ArkClaw by following the <a href="https://docs.byteplus.com/en/docs/ecs/One-click_integration_with_ArkClaw#NxLmzbFS">usage tips</a>, such as configuring the message channel, switching the model, and defining the soul.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">At the top of the chat interface, you can view the remaining available days of ArkClaw at any time.   </div>
   





</Tab>
</Tabs>


<span id="NxLmzbFS"></span>
## Usage tips

<span id="HShrkq12"></span>
### View and learn skills

ArkClaw includes some commonly used built\-in skills that can be automatically matched and called based on task requirements. You can install skill plug\-ins for ArkClaw from channels such as ClawHub and BytePlus exclusive Skill Hub. You can expand new skills for ArkClaw in multiple fields, such as programming, browser operations, office work, and expert roles as needed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Skills are essentially capability units with encapsulated logic for executing specific tasks (for example, your Python language capability, addition operations, English language, or other skills). When performing tasks, ArkClaw automatically selects the appropriate skills from its skill list to complete operations (for example, during programming, you might select skills such as Python or English). <a href="https://agentskills.io/home">Learn more</a>.</div>



<Tabs>
<Tab zoneid="yFWxbM9sCU" title="View my skills">
<TabTitle>View my skills</TabTitle>

You can view the currently available skills, including preset skills and skills you have installed.


1. Click the "Skills" button, and in the pop\-up window, click "View my skills".

2. You can view information about the currently installed skills based on the ArkClaw reply.


</Tab>
<Tab zoneid="yYsvF9KATZ" title="Learn skills">
<TabTitle>Learn skills</TabTitle>

Skills are various tools that enable ArkClaw to help you​ quickly complete different tasks. ArkClaw can learn new skills based on your needs.


1. Click the "Skills" button. In the pop\-up window, select the skill you need based on the recommendation prompts. In this example, install the "code\-optimization" skill.

2. After you confirm that the skill to be installed in the dialog box meets your requirements, press the Enter key to initiate the command.

3. Check the skill installation based on the ArkClaw response.

4. Use the installed skill. For example, enter "Help me optimize the following code" in the dialog box.

   ```Python
   result = ''
   for item in very_large_list:
       result += str(item)
   ```
   

5. If the preset skills available for learning do not meet your requirements, you can ask ArkClaw to install skills in conversation. Example: Install the weather skill for me.


</Tab>
</Tabs>


<span id="eCRjvyLk"></span>
### Viewing and configuring scheduled tasks

ArkClaw can not only passively answer and address your questions in real time, but also execute the scheduled tasks you set and **proactively send you reminders**.


<Tabs>
<Tab zoneid="QZHxfPIN" title="View current scheduled tasks">
<TabTitle>View current scheduled tasks</TabTitle>

You can view the currently configured scheduled tasks and clearly see all task details.

> If you have not configured a scheduled task, see "Configure scheduled tasks" for setup instructions.



1. Click the "Scheduled tasks" button, and in the pop\-up window, click "View my scheduled tasks".

2. Based on the ArkClaw response, you can view the details of your currently configured scheduled tasks.


</Tab>
<Tab zoneid="LYWnIybT" title="Configure scheduled tasks">
<TabTitle>Configure scheduled tasks</TabTitle>

If you have not configured a scheduled task or need to add a new one, follow the ArkClaw prompts to complete the setup.


1. Click the "Scheduled tasks" button. In the pop\-up window, select the target task based on the recommendation prompts. In this example, select "Temporary reminder".

2. After you confirm the content in the dialog box, press Enter to run the command.

3. (**Optional**) If the content does not meet your requirements, manually modify it in the dialog box and then press Enter to run the command.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you set a scheduled task, we recommend specifying the following information:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Execution time</strong>: The time when you want to be reminded. For example, every day at 8:00 AM.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Task content</strong>: The reminder details. For example, summarize the top 10 news stories in the AI field today.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Output format</strong>: How the information is displayed. For example, return the information in a table.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Limits</strong>: Rules and limitations regarding task execution, content scope, language style, and other aspects. For example, use only Chinese and include a risk warning for unofficial news.   </div>
   

   * **Recommended prompt template:** 

      Execute  **[task]**  at  **[time]** , output in  **[format]** , and comply with  **[limits]** .

   * **Sample prompt**

      At 8:00 AM every day, summarize the top 10 news stories in the AI field today and send them to me in a table (with the following headers: News Source, News Title, Content Summary, and Publication Time). Unofficial news must include a risk warning. Each news summary should be within 200 words.

4. Check the scheduled task configuration based on the ArkClaw response. If a message similar to the following is displayed, the scheduled task is set successfully.


</Tab>
</Tabs>


<span id="2QJXIw3g"></span>
### Configure message channels

ArkClaw supports integration with your ** Telegram bot**  and other message channels. After integration, you can chat with ArkClaw through the corresponding bot. ArkClaw can also use bot capabilities to help you perform operations such as scheduling calendar events. For details, see [Configuring message channels](https://docs.byteplus.com/en/docs/ecs/Configuring_message_channels).

<span id="8VFxARVI"></span>
### Configure soul

You can define a soul for ArkClaw to build it into a "soulful" AI assistant.


1. Click the "Soul" button.

2. In the pop\-up window, select a commonly used soul example, or enter the soul you want to define for ArkClaw (such as its name, form of address to you, personality, and way of handling tasks), and click "Confirm".

3. After the ArkClaw configuration is complete, ArkClaw will chat with you and perform related tasks using the soul you set.


<span id="svhvfhkX"></span>
### Use the fast file transfer feature to upload/download files

You can use a TOS bucket from the [Torch Object Storage (TOS)](https://docs.byteplus.com/en/docs/6349) as a cloud disk to quickly upload files to and download files from the cloud. ArkClaw can use files from the cloud disk as task materials, and can also place files generated after task execution (such as documents, images, and videos) into the cloud disk. This makes the files available for you to download locally.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Using a TOS bucket incurs additional fees. For specific billing standards and service rules, please refer to <a href="https://docs.byteplus.com/en/docs/tos/docs-storage-fee">Reserved storage capacity fees</a>.</div>


<span id="j8phYkJ4"></span>
#### Step 1: Configure cloud disk

Configure the TOS bucket to be mounted as a cloud disk.


1. In the [ArkClaw console](https://console.byteplus.com/ark/region:ark+cn-beijing/experience/claw), choose how to access the cloud disk configuration page based on your actual situation.

   * If you are a **new user**, select "Fast file transfer  **\>**  Configure now" to enter the cloud disk configuration page.

   * If you ** have used ArkClaw**, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_300a8e7a172ea3be4987e66e9b22271a.png) </span> icon in the upper right corner of the page. Then, click "Configure cloud disk" to enter the network disk configuration page.

2. Configure the following information in the pop\-up window, and click the "Confirm" button to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not enabled the TOS service, go to the <a href="https://console.byteplus.com/tos">TOS console</a> to enable the service first.   </div>
   

   
   |Parameter​ |Description |
   |---|---|
   |**Select TOS bucket** ||
   |Region |The region where your TOS bucket supported by ArkClaw is located. |
   |TOS bucket name |Select the name of the TOS bucket you need ArkClaw to use.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Select the cloud disk you need to mount. If you have not created a TOS bucket yet, follow the page instructions for creation first.</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">Click the "Create TOS bucket" button and configure the following information. Other settings can remain as default.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Name: Customize the TOS name. For example, <code>arkclaw-0304</code>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Region: Select the region where the TOS bucket is located. The TOS bucket must be in a region supported by ArkClaw.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Click the "Confirm" button to complete the operation.</div><br> |
   |**Configure key**<br><br>Obtain the Access Key ID and Secret Access Key to mount the TOS bucket as a local directory. This allows ArkClaw to directly read and write cloud storage data. ||
   |Access Key ID |Enter the Access Key ID and Secret Access Key.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Access Key ID and Secret Access Key are the API access keys of the BytePlus account to which the TOS bucket you create belongs:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can go to the <a href="https://console.byteplus.com/iam/keymanage/">Access Key Management console</a> to create or obtain them.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Be sure to keep them secure.</div><br> |
   |Secret Access Key ||
   

3. After configuration is complete, BytePlus will mount the TOS bucket you select as an ArkClaw local directory, with the path `/root/.openclaw/workspace/tos_storage`.

4. (**Optional**) Modify the network disk configuration.

   > Perform this operation when you need to replace a TOS bucket or modify your Access Key ID and Secret Access Key.   
   

   1. Select "Settings  **\>**  Configure cloud disk".

   2. Click the "Update cloud disk configuration" button, and modify the cloud disk configuration based on the table information in "Step 1: Configure cloud disk".

   3. Click the "Confirm" button to complete the modification.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">ArkClaw update is expected to take about 1 minute. Please wait patiently.      </div>
      

<span id="9Qp0xVHl"></span>
#### Step 2: (Optional) Download the network disk client

After downloading the network disk client, you can visually manage TOS storage space via the GUI, such as uploading and downloading files, without command lines. This makes operations simpler and more efficient. After installation, you can open it locally.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Install the network disk client on a local PC that can access the public network. If you have installed this tool, skip this step.</div>



1. On the network disk configuration page, click "Step 2: Download network disk client" and download the corresponding installation package according to your operating system.

&nbsp;

   
   |**Operating system** |**Operating system requirements** |**Download link for installation package** |
   |---|---|---|
   |Windows |* Windows 7 Pro SP1 64\-bit<br><br>* Windows 10 Pro 64\-bit<br><br>* Windows Server 2016 standard 64\-bit |[TOS Browser-win64](https://tos-tools.tos-ap-southeast-1.bytepluses.com/windows/TOS_Browser_BytePlus_Public-win32-x64.exe) |
   |macOS |* Mac OS X10.13.3 (distinguishes between Intel and Apple Silicon)<br><br>* Mac OS X10.15.7 (distinguishing between Intel and Apple Silicon)<br><br><br>&nbsp;<br><br>The macOS system cannot open unverified developer apps by default. If the installation of TOS Browser prompts that the developer cannot be verified, you need to modify the system settings. For details, see [When installing TOS Browser on a macOS system, it prompts that the developer cannot be verified](https://docs.byteplus.com/en/docs/tos/Tools#64c5af56). |* Intel chip: [TOS Browser-darwin-intel](https://tos-tools.tos-ap-southeast-1.bytepluses.com/darwin/TOS_Browser_BytePlus_Public-darwin-x64.dmg)<br><br>* Apple chip: [TOS Browser-darwin-arm64](https://tos-tools.tos-ap-southeast-1.bytepluses.com/darwin/TOS_Browser_BytePlus_Public-darwin-arm64.dmg) |
   

3. Double\-click the installation package and follow the prompts to complete the installation.

4. After installation, open the network disk client and complete the developer application verification.


<span id="9Kf8qbqI"></span>
#### Step 3: Log in to TOS Browser


1. Click the "Fast file transfer" button.

2. In the pop\-up dialog box, click the "Open TOS Browser" button to quickly start TOS Browser.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After selecting "Always allow console.colcengine.com to open relevant links in associated applications", you can skip this step when you need to start TOS Browser later.   </div>
   

3. On the local TOS Browser page, click the "Log in" button.

4. You are then redirected to the local TOS Browser page, where you can see that you have logged in successfully.


<span id="IDODmwhg"></span>
#### Step 4: Upload/download files via TOS network disk


1. Upload local files to TOS as needed. This allows you to use ArkClaw to analyze, summarize, and perform other operations on corresponding files.

   1. On the file list page, click the "Upload file" button at the top left of the page.

   2. In the "Pending upload" module, click the "Select file" or "Select folder" button based on the content you want to upload.

   3. In the pop\-up window, select the local file or folder you need to upload to the TOS bucket, and click the "Confirm" button.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For parameter details of the file uploading feature, see <a href="https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file">Uploading files</a>.      </div>
      

2. Use ArkClaw to analyze uploaded files or store task\-generated files in TOS for download.

   * **Analyze** ** uploaded files**

      * **Sample prompt:** 

         Find the "AI Market Analysis Report" in my TOS bucket, summarize it, and send me the conclusions.

   * **Store** ** task\-generated files in TOS**

      * **Sample prompt:** 

         Research the top 10 most downloaded skills in ClawHub, compile their functions, features, installation methods, and other information into a document, and put it in your TOS bucket.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Subsequently, in TOS Browser, click "Download" in the "Actions" column of the target file and select a path to download the file.         </div>
         

<span id="34jlFX4O"></span>
### Use quick commands

ArkClaw includes preset commands for common operations, such as creating a new conversation, viewing system status, and clearing the context. You can send relevant commands with one click as needed to let ArkClaw perform corresponding operations.


1. Click the "Quick commands" button.

2. Select the required command in the pop\-up window.

   
   |Command |Description |
   |---|---|
   |New chat |Sends the `/new` command to instruct ArkClaw to create a new session. This is applicable when you want ArkClaw to start executing a new task, or when you do not want the old conversation content to interfere with subsequent conversations. |
   |System status |Sends the `/status` command to view the current ArkClaw status. This is ideal for checking the service version, inference model, token consumption, and other information of ArkClaw. |
   |View context |Sends the `/context list` command to list all context data (such as files, code snippets, and chat history) loaded or referenced by ArkClaw in the current session. This helps you verify what ArkClaw "remembers" and ensure it has not missed important information. |
   |Clear context |Sends the `/clear` command to clear the conversation history or context of the current session. This applies to scenarios where an overly long conversation causes ArkClaw context disorder or token limit exhaustion. |
   |Summarize chat |Sends the `/summarize` command to summarize the current session or context. This is ideal for quickly reviewing key points after a long conversation, or for preparing to hand over the current task to another person or another session. |
   |View plan |Sends the `/plan` command to view the plan for the current task. This is applicable when you want ArkClaw to generate step plans before starting complex development, or to check whether the current task deviates from the original plan. |
   |Tool list |Sends the `/tools list` command to list the available tools or plugins for ArkClaw (for example, code execution, file read/write, network requests). This is ideal for viewing which external features ArkClaw currently supports. |
   

4. You can view the command execution result based on the ArkClaw reply.


<span id="sMdwUjY6"></span>
### Manage ArkClaw

<span id="SLFTbgHj"></span>
#### Adjust inference model

You can use another supported inference model in Coding Plan as needed to provide inference services for ArkClaw.


1. Click the "Settings" button in the upper right corner.

2. Click the "Configure model" button to go to the [Model activation page](https://console.byteplus.com/ark/region:ark+ap-southeast-1/openManagement?LLM=%7B%7D&advancedActiveKey=subscribe).

3. On the Coding Plan tab, select the model you need ArkClaw to use.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend selecting <code>Auto</code>, the smart model scheduling option. With this model, ModelArk selects the optimal computing power and model combination for your ArkClaw based on both effectiveness and speed, providing a more effortless experience.   </div>
   

4. **The new configuration takes effect automatically within 3\-5 minutes**. Once it takes effect, ArkClaw will use the new model for inference.


<span id="lxt4NuD6"></span>
#### Restarting ArkClaw

You can manually restart ArkClaw when you need to load new ArkClaw configuration, when ArkClaw responds slowly, or in other situations.


1. Click the "Settings" button in the upper right corner.

2. Click the "Restart" button.

3. In the pop\-up window, click "Confirm" to restart the ArkClaw service.


<span id="TYfN3X5x"></span>
#### Restore ArkClaw to factory settings

You can reinitialize the ArkClaw service and reset it to its initial available state when the configuration is corrupted and causes a service crash, or when system failures or abnormal states occur and cannot be recovered.


1. Click the "Settings" button in the upper right corner.

2. Click the "Restore factory settings" button.

3. In the pop\-up window, click "Confirm" to reset the ArkClaw service.


<span id="8uiPRBhC"></span>
#### Auto healing of ArkClaw

When your ArkClaw becomes unavailable due to tasks, setting adjustments, or other reasons, you can use the auto healing feature to attempt to restore it to the latest available state.


1. Click the "Settings" button in the upper right corner.

2. Click the "Automatic repair" button.

3. In the pop\-up window, click the "Confirm" button. BytePlus will attempt to restore ArkClaw to its latest available state.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Automatic ArkClaw repair takes 1–3 minutes. Please wait patiently.   </div>
   

<span id="fYM2xYNJ"></span>
#### Accessing ArkClaw from terminals

You can access ArkClaw from a terminal and use Shell commands to perform various operations (such as viewing directories and files in the current path, creating tasks, and so on). **This is suitable for technical developers who need in\-depth usage.** 


1. In the upper right corner of the ArkClaw page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_832c02964893a6022129c864d723344e.png) </span>.

2. Click the "View terminal" button to access the terminal.

3. Enter the specified command and execute it to complete the corresponding action. Example:

   Execute the following command to view the current OpenClaw version.

   ```Bash
   openclaw --version
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3db566e93fa12fefa46797cb2e3f2129.png) </span>
