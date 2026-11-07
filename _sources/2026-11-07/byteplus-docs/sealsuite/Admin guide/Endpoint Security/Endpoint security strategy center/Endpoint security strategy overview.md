---
title: "Endpoint security strategy overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/endpoint-security-strategy-overview"
---

The SealSuite endpoint security system integrates policy management for two core endpoint security capabilities: **Endpoint Detection and Response (EDR)**  and **Antivirus**. It is designed to provide enterprises with a comprehensive defense solution against both known viruses and unknown advanced threats through the coordinated use of "low\-level behavior monitoring" and "upper\-level threat detection and removal."

<span id="af232df5"></span>
## Defense Philosophy

By integrating EDR and antivirus capabilities, SealSuite delivers in\-depth defense that combines broad coverage with targeted protection.


* **Antivirus (AV): Static Blocking Based on Known Signatures**

   The antivirus module mainly relies on local virus databases and cloud threat intelligence. By comparing static file characteristics (such as hashes and signatures), it quickly identifies and blocks known malicious files. Its advantages are fast detection and low resource usage, making it the first line of defense against common viruses.

* **Endpoint Detection and Response (EDR): Continuous Monitoring and Tracing Based on Dynamic Behavior**

   When advanced threats bypass static signature\-based blocking (for example, memory injection attacks that execute without writing files to disk), EDR continuously collects and records low\-level endpoint behaviors (such as process startup, registry modification, and network connections). The system automatically correlates and analyzes these behavior traces to identify abnormal actions that match attack chains (such as APT attacks and lateral movement), and generates dynamic threat behavior alerts. This provides technical support for security teams to trace attack origins and block malicious process chains.


<span id="6c7598d7"></span>
## Core Capabilities

By configuring and delivering security policies, you can achieve the following core defense capabilities.


* **Comprehensive Endpoint Behavior Collection (EDR)** 

   You can customize the collection scope and depth of endpoint behaviors (such as process creation, file read/write, network connections, and registry modification). The collected behavior logs are used not only for post\-event security tracing and evidence collection, but also as the data foundation for the system to generate advanced "threat behavior" alerts and block fileless attacks (such as ransomware and cryptomining).

* **Multi\-Engine Static Threat Detection and Removal (Antivirus)** 

   The system can block malicious files in real time in high\-risk scenarios such as file downloads, program startup, and peripheral device access. It also supports periodic full\-disk scans to comprehensively remove hidden Trojans and malware.

* **Cloud Threat Intelligence Integration**

   The system supports subscribing to the latest advanced cloud threat intelligence (such as phishing software and specific APT attack tools). Whether during static file scanning by the antivirus module or low\-level behavior collection by EDR, the system extracts characteristics and compares them with the threat intelligence database in real time, enabling near\-instant blocking of newly emerging threats.

* **Fine\-Grained Security Control and Exception Management**

   * **Differentiated delivery**: Supports delivering security policies with different strengths based on department, role, or device group.

   * **Performance balance**: Provides multiple levels of resource usage control, including daily mode and forensic mode for EDR, as well as experience first, balanced mode, and safety first for Antivirus, to balance the endpoint user experience with security detection strength.

   * **Exception management**: Provides a global blacklist/whitelist management to ensure that core business operations are not mistakenly blocked by security policies.


<span id="8f5355e3"></span>
## Configuration Guide

You can independently configure and manage the following policies.


|**Feature module** |**Description** |**Related Documents** |
|---|---|---|
|**EDR Behavior Collection** |Defines the types of behavior events that endpoints need to report (such as process startup and network connections). By configuring this policy, the system can obtain key security telemetry data, providing the data foundation for advanced threat alerts and security tracing. |[Configuring EDR behavior collection policy](https://docs.byteplus.com/docs/sealsuite/configuring-edr-behavior-collection-policy) |
|**Virus Detection** |Specifies detection items, detection frequency (real\-time scanning or scheduled scanning), and automated handling methods for malicious files. It also supports enabling system defense against suspicious PowerShell scripts. |[Configuring virus detection policy](https://docs.byteplus.com/docs/sealsuite/docs-policy-configuration) |
|**File Intelligence Library** |Enables subscriptions to a large cloud\-based feature database of advanced malicious files. After the file intelligence database is configured, the endpoint engine synchronizes the latest threat intelligence at high frequency, enabling proactive blocking of unknown threats such as phishing, Trojans, and ransomware. |[Configuring file intelligence library](https://docs.byteplus.com/docs/sealsuite/file-intelligence) |
|**Blacklist/Whitelist** |Provides a globally effective mechanism for exception and risk definition. It supports forcibly exempting specific files from scanning (whitelist), or marking them as known risks (blacklist), based on dimensions such as file hash and path. |[Configuring blacklist](https://docs.byteplus.com/docs/sealsuite/configuring-blacklist)<br><br>[Configuring whitelist](https://docs.byteplus.com/docs/sealsuite/configuring-whitelist) |
|**General Settings** |Centrally defines the basic runtime parameters of the endpoint antivirus module, including maximum scanned file size, antivirus engine switches (local or cloud scan), virus database update frequency, and user trusted zone permissions. |[Configuring general settings](https://docs.byteplus.com/docs/sealsuite/configuring-general-settings) |
