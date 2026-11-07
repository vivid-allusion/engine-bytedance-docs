---
title: "Overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Overview_cua"
---

A cloud PC is a fully functional cloud\-based virtual computer hosted in the ArkClaw environment. It provides a complete desktop operating environment, allowing you to browse the web pages and run or manage various applications just like on a local computer.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The cloud PC feature is in<strong> Beta</strong>. Your participation and feedback are welcome. If you experience any problems, exceptions or have any suggestions during use, submit feedback by clicking "Settings \> Feedback".</div>


<span id="GXR3Lxqd"></span>
## **Relationship between cloud PC and cloud browser**

To enhance the automated office experience, the **cloud browser** feature of ArkClaw has been fully upgraded to **cloud PC**. The two are not parallel modules, but have an inclusive relationship:


* **Cloud PC (recommended):**  The cloud PC has **fully integrated** the cloud browser feature. You can not only directly perform tasks such as web access and data extraction, but also manage various desktop applications just like operating a local computer.

* **Cloud browser**: You can still issue and execute web automation\-related commands. However, we recommend that you [upgrade to the cloud PC with one click](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_#Ki12IJPP) to unlock the full desktop\-level environment.


<span id="p0PEWVuD"></span>
## Supported capability


|Operation |Description |
|---|---|
|[Cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_) |It provides a complete cloud desktop environment, allowing you to browse the web pages and run or manage various applications just like on a local computer. |
|[Switching execution mode of cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Switching_execution_mode_of_cloud_PC_) |Supports flexible switching among the auto mode, browser mode, cloud desktop mode, and OpenCli mode to match task complexity. |
|[Automated office capabilities of cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Automated_office_capabilities_of_cloud_PC_) |Supports directly calling and running Office components in the cloud to automate the creation and processing of documents, spreadsheets, slides, and other files. |
|[Desktop operation recording and prompt generation](https://docs.byteplus.com/en/docs/ArkClaw/Desktop_operation_recording_and_prompt_generation_?lang=en) |Supports the generation of structured prompts via cloud PC operation recording. The prompts can be executed automatically in real time or saved as dedicated task templates for reuse. |


<span id="O93cjWyn"></span>
## Limits

When using the cloud PC, please note the following restrictions:


* Specification limits

   * Starting from **00:00:00 on May 21, 2026**, newly created **ArkClaw Starter** instances will no longer support the cloud PC feature. Existing instances created before this date are not affected, but due to resource configuration limitations, the smoothness of cloud PC operations may be compromised.

   * To use this feature or to obtain a better user experience, we recommend that you contact the administrator to upgrade the instance to **Standard** or a higher edition, or [create an instance with a higher specification](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_#SdWGV7CH).

* It is only supported on **PCs**, **Feishu**, and **WeChat**.

* To upgrade from cloud browser to cloud PC, please refer to [One-click upgrade](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_#Ki12IJPP) to complete cloud PC installation. If you have not previously used the cloud browser in ArkClaw, the system will [directly upgrade](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_#Ki12IJPP) it to the cloud PC by default, with no separate configuration required.

* Multi\-agent collaboration and concurrency requirements:

   * Before a sub\-agent (non\-primary agent) initiates a cloud PC task, you need to ensure that the current environment has been configured with the corresponding execution skills (including **computer\-use**, **XUA\-auto**, **opencli**, and **browser**) based on the business needs. Otherwise, the call will fail. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents?lang=en).

   * To avoid operation conflicts and mutual interference caused by resource contention, we recommend that **only one cloud PC task runs on a single ArkClaw instance at any given time**. Avoid triggering high concurrency in multi\-agent or multi\-session scenarios whenever possible.

* Cloud browser/cloud PC cannot be used when the ArkClaw runtime environment is changing or the business logic fails to work. Specific scenarios include:

   * ArkClaw is in the initialization phase.

   * ArkClaw is in the process of restarting.

   * ArkClaw is being fixed.

   * ArkClaw is restoring factory settings.

   * The ArkClaw account is in arrears.
