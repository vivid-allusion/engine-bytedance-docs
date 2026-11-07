---
title: "Configuring file intelligence library"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/file-intelligence"
---

SealSuite’s **File Intelligence** feature relies on a large cloud\-based threat intelligence center to provide a massive database of advanced malicious file signatures. By configuring the file intelligence library, administrators can subscribe to various types of advanced threat intelligence, such as phishing software, Trojans, and ransomware, and seamlessly integrate the intelligence with the endpoint antivirus detection engine. Once the engine detects a malicious file that matches the intelligence database, the system automatically blocks, quarantines, or deletes the file according to your virus detection policy configuration, comprehensively improving the enterprise’s ability to defend against unknown and highly stealthy threats.

<span id="7d2df9bf"></span>
## Antivirus Detection Mechanism Comparison

By default, the endpoint antivirus engine relies on the local virus database and regular cloud scan engine for detection. Although this covers most known threats, there may still be update delays and blind spots in advanced threat identification.


|Detection Mechanism |Data Scope and Update Mechanism |Network Dependency |Core Positioning and Advantages |
|---|---|---|---|
|**Local virus database** |**Basic/full signatures**: Contains the most common and active virus signatures accumulated over time. It relies on fixed, low\-frequency periodic updates. |**Available offline**: Fully relies on local computing and remains effective in disconnected environments. |**Baseline defense**: Provides stable and basic virus detection and removal capabilities with relatively controllable resource usage. |
|**File intelligence library** |**Advanced/specialized signatures**: Focuses on the most active advanced threats, such as new Trojans and specific APT attacks. Through high\-frequency dynamic subscription, the latest intelligence of specific types from the cloud is delivered to and retained in the local engine. |**Available offline**: Requires network access to download the latest intelligence from the cloud. Once intelligence signatures are synchronized to endpoints, threats that match the intelligence can still be blocked even when the endpoint is disconnected. |**Proactive blocking**: Uses high\-frequency updates to block highly stealthy threats in the early outbreak stage before the local virus database is updated. |


<span id="0f97a61d"></span>
## Prerequisites

**An effective Virus Detection policy must exist.**  The file intelligence library only provides malicious file signatures and does not have independent handling capabilities. When a file matches the intelligence library, the system relies on the effective endpoint antivirus policy to determine whether to allow or quarantine the file. If an antivirus policy is not in effect, File Intelligence cannot perform blocking.

<span id="1aa0b6e0"></span>
## How to Configure the File Intelligence Library


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Endpoint Security** \> **Threat Intelligence**.

3. Click the **File Intelligence** tab, then click **Library Configuration** in the top\-right corner.

4. In the **Threat Types** section, select the categories of threats you want to detect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9efcb7be25e04f3eb9d22d949ce94fd8~tplv-goo7wpa0wc-image.image) </span>

5. In the **Remediation** section, ensure the Anti\-Virus toggle is **Enabled** and click **Confirm**.

   * **Enabled:**  The selected threat intelligence categories will be added to the Endpoint Antivirus detection engine.

   * **Disabled:**  The Endpoint Antivirus engine will not scan for these specific malicious file types.


<span id="2bf41fda"></span>
## Handle False Positives (Add to Whitelist)

For internally developed enterprise software or trusted files that are incorrectly flagged by threat intelligence sources, you can add them to the unified file whitelist to ensure normal operation. For detailed steps, see [Configuring whitelist](https://docs.byteplus.com/docs/sealsuite/configuring-whitelist).

<span id="6a71fb12"></span>
## Viewing File Intelligence Alerts

When a file triggers a File Intelligence rule, an alert is generated in the Antivirus log. See [Auditing virus-related events through the Audit Logs](https://docs.byteplus.com/docs/sealsuite/docs-virus-log-audit) for details.
