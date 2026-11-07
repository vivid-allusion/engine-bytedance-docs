---
title: "BytePlus Notice on Emergency Response to the axios npm Supply Chain Poisoning"
product: "BytePlus Security Bulletins"
product_code: "byteplus-security-bulletins"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-security-bulletins/axios_poisoning"
---

<span id="background"></span>
# Background

Recently, a supply\-chain poisoning incident involving the `axios` npm package and OpenClaw has been disclosed, resulting in critical security risks. The BytePlus Security Team responded promptly and provided comprehensive and reliable mitigation measures for BytePlus customers. We recommend that enterprises immediately investigate their environments and remediate any affected assets.

<span id="incident-description"></span>
# Incident Description

An attacker compromised the maintainer account of the `axios` package and injected a malicious dependency, `plain-crypto-js`, into the `package.json` file of version `1.14.1`. When users install affected `axios` versions or perform an update in OpenClaw, the malicious script is executed. It collects host, directory, and process information from the user's machine and deploys a command\-and\-control (C2) backdoor Trojan for remote control.

<span id="risk-level"></span>
# Risk Level

Critical

<span id="risk-status"></span>
# Risk Status

As of 2026\-03\-31 20:00:00 (UTC+8).


|Risk details |PoC status |In\-the\-wild exploitation |
|---|---|---|
|Publicly disclosed |Publicly available |Detected in the wild |


<span id="scope-of-impact"></span>
# Scope of Impact

The following packages have been confirmed as malicious in this incident:


* axios@1.14.1

* axios@0.30.4

* plain\-crypto\-js@4.2.1


<span id="mitigation-measures"></span>
# Mitigation Measures

For BytePlus customers, the platform provides comprehensive and reliable security solutions. You can investigate and mitigate this risk by following the steps below.

<span id="i-global-self-examination-identify-your-risk-exposure-surface"></span>
### I. Global self\-examination: identify your risk exposure surface

Use **Cloud** **Security** **Center** to investigate and locate assets affected by the axios npm package supply chain/OpenClaw poisoning incident, and view detailed remediation recommendations.


> 1. Apply for early access, log in to Cloud Security Center, and purchase the Advanced edition: https://console.byteplus.com/security\-center

> 2. Navigate to the **Risk Management \> Vulnerability Detection** page and click **Scan Now**. After the scan completes, search for "axios" to check for poisoning incidents. If a vulnerability is found, click **Details** to view affected assets and follow the provided remediation advice.

> 3. Go to the **System Configuration \> Install/Uninstall** page and ensure that security protection is enabled for all hosts to provide real\-time detection of malicious activity related to axios poisoning. This also enables continuous detection of post\-exploitation behavior, such as suspicious file access, command execution, persistence, and privilege escalation.


<span id="ii-prevention-and-hardening-restrict-the-conventional-attack-kill-chain"></span>
### II. Prevention and hardening: restrict the conventional attack kill chain

Use **Cloud Firewall** to restrict unauthorized access and allow only trusted internal or local IP addresses to access your service ports.


> 1. Activate and log in to Cloud Firewall: https://console.byteplus.com/firewall

> 2. On the Firewall Switches page, select **Internet Border Firewall**. Locate the **public** **EIP** **address** of your service asset and enable the protection switch.

> 3. Go to **Access Control \> Internet Border**. Under the Inbound Rules and Outbound Rules tabs, click **Add Policy** to create access control rules that only permit trusted IPs to access your asset's service ports.

> 4. Navigate to **Intrusion Prevention \> Rule Configuration** and enable **Basic Protection** and **Virtual Patching** to detect external intrusions and anomalous outbound connections in real time.
