---
title: "Data security overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-dlp-overview"
---

Data Security protects business data through risk employee analysis, data posture, investigation audits, and other methods. It helps detect and trace data leakage risks promptly and records alert events. Screen watermark and peripheral control policies further strengthen Data Security protection.

 &nbsp;

<span id="注意事项"></span>
# Notes


* Enterprises must sign relevant usage agreements and authorization agreements with employees. Before or when requiring employees to install SealSuite, the enterprise must clearly, explicitly, and specifically inform employees of the data types collected by SealSuite, the purposes of use, methods of use, and scope of use.

* Endpoint\-side Data Security supports Windows, macOS, and Linux desktop endpoints. Specific capabilities depend on the supported scope of each feature. Web Data Protection and GenAI Data Protection perform detection when traffic passes through SWG. For usage requirements, see their configuration documents.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The Linux endpoint currently supports Ubuntu 22.04, Ubuntu 20.04, Ubuntu 18.04, and Ubuntu 16.04 operating systems.   </div>
   

 &nbsp;

 &nbsp;

<span id="功能介绍"></span>
# Feature introduction

Data Security protects business data, detects data leakage risks promptly, and traces them. This helps enterprises manage secure office work more effectively. SealSuite protects business data mainly through the following methods and policies.


* **Risk employees**

   View employee information for employees with outbound risk alerts and local sensitive files. You can also view their Outbound file transfer details, local sensitive file overview, encrypted file overview, local sensitive file details, and sensitive file flow status.

* **Data posture**

   Data posture displays the distribution of sensitive data on enterprise endpoints and provides global data posture awareness. From the enterprise perspective, view where sensitive data is stored and how it is sent outbound. Search by keywords such as file content or sensitive data names to trace sensitive files. Sensitive file lineage analysis is also supported.

* **Policy Center**

   Configure and manage data control policies in Policy Center to centralize management of outbound data behaviors.

   * **Outbound file control**: Monitors and controls employees' Outbound file transfer behavior through storage devices, desktop software, Web applications, and other channels. Configure unified Outbound file control policies to audit identified risky behavior, including recording alerts, capturing screenshots as evidence, and archiving original files. You can also block the behavior directly to support post\-event tracing and source\-level leak prevention.

   * **Web Data Protection**: Detects sensitive content in text and uploaded files when traffic passes through SWG. Text transfers can be audited or blocked; file uploads support auditing only. For downloads, policies check file size and type without scanning file contents.

   * **GenAI Data Protection**: Detects prompts that employees send to AI applications or submit through large language model APIs. It identifies sensitive content through classification and grading rules, and audits or blocks the activity based on policies.

   * **Channel control**: Blocks high\-risk operations in chat software or cloud drive applications on Windows and macOS endpoints in real time, such as sending files to external contacts. After a block is triggered, the system records the event and reports it to the Admin Console.

   * **Clipboard control**: Monitors and controls sensitive data that endpoint employees copy and paste across applications. It supports audit alerts and blocking actions.

   * **Channel list**: Provides a unified channel capability matrix. It centrally displays all application channels that SealSuite supports for control and the corresponding control details, and supports custom channel configuration and management.

   * **Agent policies**: An intelligent audit and risk assessment system built on a vertical security large model (Doubao large model). It combines enterprise background knowledge with AI logical reasoning to address pain points such as inaccurate traditional rule\-based identification and low efficiency in analyzing massive logs.

* **Data identification**

   Enterprise sensitive data repositories. An administrator can preset sensitive data resource libraries, such as sensitive word libraries, file fingerprint libraries, file type libraries, and file source libraries, and define unified classification and grading rules through logical orchestration. Based on these rules, the system automatically determines the security level (L1~L4) of Endpoint files. This provides the identification basis and standards for subsequent controls. Web Data Protection and GenAI Data Protection also identify sensitive content through classification and grading rules.

* **Watermark management**

   Configure watermark management policies for evidence collection and tracing during data leaks.

* **Peripheral control**

   Peripheral control policies restrict read/write permissions and Outbound file transfer behavior after external devices connect to employee endpoints. After an employee connects a peripheral device to an endpoint and triggers a peripheral control policy, the SealSuite client audits and alerts or blocks the action according to the policy, and pushes a corresponding message notification to the employee endpoint. In addition, after the policy is triggered, the SealSuite Admin Console records the corresponding alert event. This effectively controls data leakage risks from physical media such as USB flash drives and removable hard disks.


 &nbsp;

 &nbsp;

<span id="操作指引"></span>
# Operation guide

SealSuite recommends deploying the Data Security system according to the following business flow:

 
&nbsp;

1. **Define sensitive data and identification standards**

   * Configure atomic resource libraries: [Manage the sensitive word library](https://docs.byteplus.com/en/docs/sealsuite/managing-sensitive-thesaurus?lang=en), [Manage the file fingerprint library](https://docs.byteplus.com/en/docs/sealsuite/managing-the-file-fingerprint-library?lang=en), [Manage the file type library](https://docs.byteplus.com/en/docs/sealsuite/managing-the-file-type-library?lang=en), [Manage the file source library](https://docs.byteplus.com/en/docs/sealsuite/managing-the-file-source-library?lang=en)

   * Orchestrate rules and assign levels: [Manage classification and grading rules](https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules?lang=en)

       &nbsp;

2. **Implement control policies**

   * Understand channel capabilities: [Channel query and custom configuration](https://docs.byteplus.com/en/docs/sealsuite/channel-lookup-and-custom-configuration?lang=en)

   * Configure control policies: [Outbound file control policy management](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule?lang=en), [Channel control policy management](https://docs.byteplus.com/en/docs/sealsuite/Configuring_block_policy_for_application?lang=en), [Clipboard control policy management](https://docs.byteplus.com/en/docs/sealsuite/configuring-clipboard-control-policies?lang=en), [Configure a Web Data Protection policy](https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en), [Configure a GenAI Data Protection policy](https://docs.byteplus.com/en/docs/sealsuite/configure-genai-data-protection-policy?lang=en)

   * Configure whitelists: [Internal address configuration guide](https://docs.byteplus.com/en/docs/sealsuite/internal-address-configuration?lang=en), [File outbound control whitelists](https://docs.byteplus.com/en/docs/sealsuite/managing-file-outbound-block-allowlists), [File scan whitelists](https://docs.byteplus.com/en/docs/sealsuite/managing-file-scan-whitelists), [Process injection whitelists](https://docs.byteplus.com/en/docs/sealsuite/managing-process-injection-whitelists)

       &nbsp;

3. **Configure tracing and peripheral protection**

   * Configure watermarks: [Configure a screen watermark policy](https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-watermark-rules?lang=en), [Configure print watermarks](https://docs.byteplus.com/en/docs/sealsuite/config-print-watermark?lang=en), [Extract hidden watermarks](https://docs.byteplus.com/en/docs/sealsuite/docs-invisible-watermark?lang=en)

   * Configure peripheral permissions: [Configure a peripheral control policy](https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-peripheral-control-rules?lang=en), [Configure a peripheral control policy whitelist](https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-peripheral-control-rules-allowlist?lang=en)

       &nbsp;

4. **Monitor risks and audit**

   * View global posture: [View data posture](https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-data-trends?lang=en)

   * Analyze violation events: [Investigation audit](https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-audit-alerts?lang=en), [View channel block logs](https://docs.byteplus.com/en/docs/sealsuite/Viewing_channel_block_alerts?lang=en), [View clipboard logs](https://docs.byteplus.com/en/docs/sealsuite/viewing-clipboard-logs?lang=en), [View peripheral control alert events](https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-peripheral-control-events?lang=en), [View Web data outbound logs](https://docs.byteplus.com/en/docs/sealsuite/view-web-data-outbound-logs?lang=en), [View GenAI data outbound logs](https://docs.byteplus.com/en/docs/sealsuite/genai-data-outgoing-logs-view?lang=en)

   * AI\-assisted assessment: Overview of the Data Security Agent solution
