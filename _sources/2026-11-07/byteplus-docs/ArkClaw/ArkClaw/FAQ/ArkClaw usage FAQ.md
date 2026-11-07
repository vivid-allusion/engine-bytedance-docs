---
title: "ArkClaw usage FAQ"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ"
---


|Category |Issue |
|---|---|
|Cost\-related questions |[Is ArkClaw a free or paid product?](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#Pm4K3h1F) |
|Installation and deployment |[What is the difference between local deployment and cloud deployment?](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#0leIHpoO) |
||[What is the difference between ArkClaw and ArkClaw in ModelArk Playground?](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#DaEy1Df0) |
|Use ArkClaw |[Common ArkClaw error information and solutions](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#2OaotWgM) |
||[Why can't I find files or upload or download files to or from my TOS bucket?](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#GedgVfAI) |
||[Will my custom configuration and data in ArkClaw be deleted after a restart or auto‑healing?](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#lAAfJLOX) |
||[What should I do if an error occurs during restoration?](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_usage_FAQ#mopXdnmX) |


<span id="XjFkVfZ1"></span>
## Cost\-related questions

<span id="Pm4K3h1F"></span>
### Is ArkClaw a free or paid product?

ArkClaw is a paid product that uses a prepaid billing model (pay first, use later). You can subscribe to ArkClaw monthly or daily. For details, see [Billing method and description](https://docs.byteplus.com/en/docs/ArkClaw/Billing_method_and_description).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you buy ArkClaw now, you can enjoy the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Limited-time_first-purchase_discount_promotion">first purchase discount promotion</a> and <a href="https://docs.byteplus.com/en/docs/ArkClaw/Long-term_discount_package_for_first-time_purchase">regular discount package </a>for a more cost\-effective service.</div>


<span id="pqxa66rf"></span>
## Installation and deployment

<span id="0leIHpoO"></span>
### What is the difference between local deployment and cloud deployment?

**ArkClaw** fully manages the **security, operations, and environment configuration** required for local deployment. ArkClaw retains all local deployment capabilities (**OpenClaw**) while significantly **reducing usage barriers and security risks**. The detailed differences are as follows:


|**Dimension** |**Local deployment (OpenClaw)**  |Cloud deployment (**ArkClaw**) |
|---|---|---|
|**Deployment method** |Requires self\-procurement of servers, environment configuration, and dependency installation. High technical barrier. |Supports creating out\-of\-the\-box **ArkClaw** with one click, without O&M required. |
|**Network security** |The control port is easily exposed to the internet without authentication protection, making it vulnerable to attacker scanning and exploitation, which may cause unauthorized device takeover. |Deployed within the BytePlus security network. You do not need to open internet ports, which is secure and reliable. |
|**Plugin security** |Provides third\-party skills not uniformly reviewed. This poses security risks such as malicious plugins stealing keys or implanting trojans. |All preset skills have passed malicious code scanning and security audit, with security ratings included for safer use. |
|**High\-risk operation protection** |No built\-in protection mechanism. Accidental operations, such as executing rm `-rf`, will cause system crashes. |Automatically intercepts high\-risk operations through pre\-execution intent recognition. Critical operations require a second confirmation. All code runs safely in a sandbox environment. |
|**Data isolation** |Shares the runtime environment with the host machine. Data security must be configured by the user. |Runs on independent ECS instances. User data is isolated and stored, accessible only to the owner. |
|**Maintenance cost** |Requires manual monitoring, version updates, and troubleshooting, which consume significant, continuous time and effort. |The platform offers fully automatic O&M, which is stable online 24 hours a day, 7 days a week, and can reduce overall usage costs by over 60%. |


<span id="DaEy1Df0"></span>
### What is the difference between ArkClaw and ArkClaw in ModelArk Playground?

ArkClaw and ArkClaw in ModelArk Playground are the same product accessed via different entries.


* **ArkClaw**

   Refers to ArkClaw purchased and managed via the [ArkClaw console](https://console.byteplus.com/arkclaw/welcome).

   * You can purchase multiple ArkClaw of different specifications at the same time (including **Starter**, **Standard**, and **Premium**). [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios).

   * Supports all features such as multiple sessions, backup/restoration of ArkClaw data, and migration from OpenClaw to ArkClaw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Overview_2).

   * User experience improvements and new features are continuously being updated and released.

* **ArkClaw in ModelArk Playground**

   * Refers to ArkClaw created via [ModelArk Playground](https://console.byteplus.com/ark/region:ark+cn-beijing/experience/claw).

   * Only supports activating one ArkClaw (default configuration: [Starter](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios)), and does not support specification selection.

   * Only supports some features, such as configuring message channels and skills, and does not support the latest ArkClaw features.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To continue using ArkClaw created in ModelArk Playground after it expires, you can <a href="https://docs.byteplus.com/en/docs/ArkClaw/Activating_ModelArk_ArkClaw">activate BytePlus ModelArk ArkClaw</a> or <a href="https://docs.byteplus.com/en/docs/ArkClaw/Creating_your_dedicated_ArkClaw_with_one_click">quickly purchase a new ArkClaw</a>.   </div>
   

<span id="3zyJKncL"></span>
## Use ArkClaw

<span id="2OaotWgM"></span>
### Common ArkClaw error information and solutions


|Error message |Error cause |Solution |
|---|---|---|
|* API rate limit reached<br><br>* Your ArkClaw has been temporarily rate\-limited. Please wait. |Coding Plan package has [usage quota limit](https://docs.byteplus.com/en/docs/ModelArk/2165245#what-are-the-usage-quota-limits-for-coding-plan). Your ArkClaw has temporarily reached the limit. |* Go to [Coding Plan console](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=subscribe) to view quota\-related details and the quota refresh time. You can continue using it after the quota is refreshed.<br><br>* If you are using Coding Plan Lite, you can go to [Coding Plan console](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=subscribe) to upgrade to Coding Plan Pro and increase model call quota.<br><br>* [Adjust the inference model](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_inference_models). You can use models from ModelArk "Foundation models" to provide inference services for ArkClaw. This has no quota limit but incurs [additional charges](https://docs.byteplus.com/en/docs/ModelArk/1544106#token-consumption-based-billing). |
|Range of input length should be [1, 30720] |The input length for a single request exceeds the maximum context length of ArkClaw. |We recommend reducing the length of each input or sending input in batches to ArkClaw. |
|No API key found for provider "xxxx" |ArkClaw cannot call the inference model because no model API Key has been configured. |You can tell ArkClaw the model API Key in the conversation. |
|401 The API key format is incorrect |The configured API Key format is invalid, or a relay key was used. |Reconfigure the API Key or use an official API Key. ArkClaw does not support third\-party Keys. |
|400 Total tokens of image and text exceed max message tokens. Request id: |The content of a single session is too long and exceeds the inference model context limit. |We recommend using [quick commands ](https://docs.byteplus.com/en/docs/ArkClaw/Using_quick_commands)`/new` to compress sessions or [create a new session](https://docs.byteplus.com/en/docs/ArkClaw/Creating_conversations). |


<span id="GedgVfAI"></span>
### Why can't I find files or upload or download files to or from my TOS bucket?

Possible causes are as follows:


* **Configuration and association\-related reasons**

   * Unconfigured cloud disk

      Since the basic configuration of the iDrive has not been completed for ArkClaw, the system has no available storage target. [Configure the cloud disk](https://docs.byteplus.com/en/docs/ArkClaw/Using_fast_file_transfer_feature_to_upload_download_files#eE3RWntk).

   * Cloud disk configuration exception

      The configuration information is incorrect or has not taken effect. Reconfigure the cloud disk. For details, see [Configuring cloud disks](https://docs.byteplus.com/en/docs/ArkClaw/Using_fast_file_transfer_feature_to_upload_download_files#eE3RWntk).

   * ArkClaw has not been associated with TOS

      TOS configuration has been completed, but ArkClaw has not been associated with the corresponding storage bucket. Files will be stored in the local path by default. Reconfigure the cloud disk to complete the association. For details, see [Configuring cloud disks](https://docs.byteplus.com/en/docs/ArkClaw/Using_fast_file_transfer_feature_to_upload_download_files#eE3RWntk).

* **Storage, synchronization, and permission\-related reasons**

   * Files are stored locally only and not synchronized to TOS

      ArkClaw by default stores generated files in the local path` /root/.openclaw/workspace`. Without explicit synchronization instructions, files will not be automatically uploaded to TOS. [You need to upload files via the TOS cloud disk](https://docs.byteplus.com/en/docs/ArkClaw/Using_fast_file_transfer_feature_to_upload_download_files#a8pIKicT).

   * TOS billing delay

      TOS calculates usage for all billing items on an hourly basis, generates bills based on usage, and applies resource package deductions. Newly purchased resource packages or recently uploaded files may not be reflected immediately. We recommend checking the remaining resource package balance again after receiving the bill before use.

   * Unsupported storage type

      ArkClaw only supports TOS buckets as cloud disk storage media. Uploading or reading files via GitHub, group files, email, or other methods will fail, and the corresponding files cannot be found. [Upload or download files via a TOS cloud disk](https://docs.byteplus.com/en/docs/ArkClaw/Using_fast_file_transfer_feature_to_upload_download_files#a8pIKicT).


<span id="lAAfJLOX"></span>
### Will my custom configuration and data in ArkClaw be deleted after a restart or auto‑healing?

No.


* The restart process only involves restarting the ArkClaw service and does not affect configuration or data.

* During restarting or auto\-healing, only the corrupted configuration items are fixed. All custom configuration, chat history, skill files, and other items that do not cause ArkClaw service failures are fully preserved.


<span id="mopXdnmX"></span>
### What should I do if an error occurs during restoration?

Save the error information and obtain support via [feedback](https://docs.byteplus.com/en/docs/ArkClaw/Feedback).
