---
title: "Migrating OpenClaw to ArkClaw"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Migrating_OpenClaw_to_ArkClaw__"
---

With the migration feature, you can quickly migrate existing OpenClaw data to ArkClaw. After migration, ArkClaw will use the memories, skills, and other data accumulated in OpenClaw to maintain consistency with your original usage habits and operation logic. This enables a smooth transition with zero learning cost and no service interruption.

<span id="thPxwkMK"></span>
## Usage notes


* Migrating OpenClaw deployed locally or on major cloud platforms (such as Alibaba Cloud, Huawei Cloud, and Tencent Cloud) is supported. You only need to ensure that OpenClaw is deployed on the Linux operating system, and its version is between **2026.2.13** and **2026.5.7** (including versions **2026.2.13** and **2026.5.7**).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can confirm via conversation (for example: "Tell me your current OpenClaw version and whether the operating system of the deployment environment is Linux?").   </div>
   

* For details about the scope of data imported to ArkClaw, see [Import scope instructions](https://docs.byteplus.com/en/docs/ArkClaw/Migrating_OpenClaw_to_ArkClaw__#RNPNUwIt).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Files larger than 200 MB will not be migrated.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Migration will not proceed if the total size of all OpenClaw files exceeds 1 GB.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Inference model information configured in OpenClaw will not be migrated to ArkClaw. ArkClaw uses models supported by the ModelArk Coding Plan by default. You can <a href="https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=zh">adjust the inference model</a> as needed.   </div>
   

* After the import, existing configurations in ArkClaw will **be overwritten and unrecoverable**. We recommend that you [back up](https://docs.byteplus.com/en/docs/ArkClaw/Backing_up_and_restoring_ArkClaw_data__?lang=zh) ArkClaw before importing data.


<span id="Sd9jMiTK"></span>
## Procedure

<span id="UJosAkMp"></span>
### Step 1: Obtain the OpenClaw import URL

You can use the export command to quickly export your original OpenClaw data to a temporary dedicated ArkClaw space and generate a dedicated and secure OpenClaw import URL.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw where you want to import OpenClaw. In the upper\-right corner, click " <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10c2e2685e2d24f9ba458cb83d98ed3e.png) </span>\> Migrate OpenClaw to ArkClaw".

3. Click the copy button to obtain the export command.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The export command is<strong> valid for 2 hours</strong>. Use it within the validity period. If the command expires, reopen the page to obtain a new command.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The export command packages and uploads your OpenClaw data to a temporary dedicated ArkClaw space without modifying any configurations of your original OpenClaw.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you perform the import operation (whether successful or failed), the temporarily stored OpenClaw data will be <strong>deleted immediately</strong>. If no import operation is performed, the data will be <strong>retained for 24 hours</strong> and automatically deleted upon timeout.   </div>
   

4. You can execute the export command in the terminal to obtain the OpenClaw import URL.

   1. Log in to the server where OpenClaw is deployed.

   2. Execute the export command you obtained earlier in the terminal.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f300850a8ae68f6137eb3084f8ce6746.png) </span>

5. After the command is executed, copy the OpenClaw import URL displayed in the output.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c653bbb48781d93da587721fef0a9ee.png) </span>


<span id="7tRAUmYk"></span>
### Step 2: Import OpenClaw


1. Return to the ArkClaw console where you want to import OpenClaw. In the upper\-right corner, click " ··· \> Migrate OpenClaw to ArkClaw".

2. Enter the OpenClaw import URL you obtained in [Step 1](https://docs.byteplus.com/en/docs/394/104355#UJosAkMp) and click the "Import and restart ArkClaw" button.

3. Confirm the risks in the pop\-up window and click "Confirm" to start the import process.

4. After ArkClaw is imported, you can chat with ArkClaw to verify that all configurations are completely consistent with the original OpenClaw configurations.

5. If the import fails, ArkClaw will automatically roll back to its pre\-import state. You can refer to **Step 1** and **Step 2** again to re\-import OpenClaw.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If ArkClaw fails to start and you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Backing_up_and_restoring_ArkClaw_data__?lang=zh">backed it up</a> before migration, you can use the backup to restore ArkClaw to a normal running state. Otherwise, you can try <a href="https://docs.byteplus.com/en/docs/ArkClaw/Auto_healing_of_ArkClaw__?lang=zh">ArkClaw auto healing</a> or <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__?lang=zh">restore ArkClaw to factory settings</a>.   </div>
   

<span id="RwzpaK7h"></span>
### Step 3: Configure message channels

The migration feature does not migrate message channel configurations from OpenClaw to ArkClaw. You need to manually configure message channels for ArkClaw.


* We recommend that you create new bots for the corresponding message channels and integrate them into ArkClaw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en).

* If you want to use an existing bot, make sure that it is not used by another OpenClaw instance. If it is already configured and used in another OpenClaw instance, you can:

   1. Stop the OpenClaw service or disable the message channel.

      
      <Tabs>
      <Tab zoneid="Y6YnPIY816" title="Completely stop the OpenClaw service (recommended)">
      <TabTitle>Completely stop the OpenClaw service (recommended)</TabTitle>
      
      If you no longer use the original OpenClaw, you can stop its service directly.
      
      
      1. Log in to the server where OpenClaw is deployed.
      
      2. Execute the following command to stop the OpenClaw service.
      
         ```Bash
         sudo openclaw gateway stop 2>/dev/null
         sudo systemctl --user disable openclaw-gateway.service
         ```
         
      
      
      <span id="KAACUMyY"></span>
      #### 
      
      
      </Tab>
      <Tab zoneid="xuGz6vBYAK" title="Only disable specific message channels">
      <TabTitle>Only disable specific message channels</TabTitle>
      
      If you want to continue using your original OpenClaw, you can disable the message channels it integrates with while keeping OpenClaw running.
      
      
      1. Log in to the server where OpenClaw is deployed.
      
      2. Execute the following command to disable specific message channels.
      
         ```Bash
         # Disable the Feishu channel
         openclaw config set channels.feishu.enabled false
         
         # Disable the WeCom channel
         openclaw config set channels.wecom.enabled false
         
         # Disable the DingTalk channel
         openclaw config set channels.dingtalk-connector.enabled false
         
         # Disable the QQ channel
         openclaw config set channels.qqbot.enabled false
         ```
         
      
      3. Execute the following command to restart the OpenClaw gateway for the configuration to take effect.
      
         ```Bash
         openclaw gateway restart
         ```
         
      
      
      
      
      
      </Tab>
      </Tabs>
      

   2. Refer to the instructions in [Configuring message channels](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en) to configure Feishu, WeChat, or other message channels for ArkClaw as needed.


<span id="RNPNUwIt"></span>
## Import scope instructions

This feature imports the following OpenClaw configurations into ArkClaw.


|Module |Configuration imported to ArkClaw |Description |
|---|---|---|
|Identity (identity and soul) |* SOUL.md: Contains OpenClaw information such as soul and personality definitions.<br><br>* IDENTITY.md: Contains OpenClaw name, profile, signature, and other information.<br><br>* USER.md: Contains information about you that OpenClaw has learned.<br><br>* AGENTS.md: Behavior guidelines for the workspace.<br><br>* TOOLS.md: Environment\-specific tool notes.<br><br>* HEARTBEAT.md: Heartbeat check checklist.<br><br>* VOICE_GUIDE.md: Voice guidance (imported only if the file exists).<br><br>* BOOT.md: Boot guidance (imported only if the file exists). |These files define what OpenClaw is. Importing them to ArkClaw retains its original role and personality settings, ensuring it remains your familiar dedicated AI assistant after migration. |
|Memory<br><br> |* MEMORY.md: This file stores long\-term curated memory of OpenClaw.<br><br>* memory/: This directory contains OpenClaw daily notes in the format of YYYY\-MM\-DD.md.<br><br>* Checkpoint: This file acts as a conversation context checkpoint.<br><br>* Status JSON files: Examples include heartbeat\-state.json. |These files contain long\-term memory of OpenClaw, including accumulated user preferences, project progress, and historical decision. Importing them to ArkClaw prevents memory loss.<br><br> |
|Skills |workspace/skills/: Workspace skills installed locally. |Skills equip OpenClaw with various capabilities (e.g., weather query, stock analysis, video generation). Importing them to ArkClaw maintains the full skill set of the AI assistant. |
|Plugins (plugins and extensions) |.openclaw/extensions/: Workspace extensions. |Plugins extend the underlying capabilities of OpenClaw, including message channel connectors (Feishu, WeCom, and DingTalk), memory engine, and browser control. |
|Sessions (session history and scheduled tasks) |* sessions.json: Stores session data for each OpenClaw instance.<br><br>* Conversation transcript files: Transcription files in .jsonl format.<br><br>* cron/jobs.json: Scheduled task configurations. |Session files store conversation context, and scheduled task files define automated behaviors such as regular reminders and checks. Importing them from OpenClaw to ArkClaw preserves your original workflow continuity. |
|Source (source code) |Custom source code in the workspace/src/ directory |Custom scripts, tools, and other source code files you have written in the workspace will also be imported into ArkClaw. This ensures that your personalized code assets are ready for use out of the box. |
