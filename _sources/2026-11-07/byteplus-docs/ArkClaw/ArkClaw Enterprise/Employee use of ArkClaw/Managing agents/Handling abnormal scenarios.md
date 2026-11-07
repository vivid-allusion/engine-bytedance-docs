---
title: "Handling abnormal scenarios"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Handling_abnormal_scenarios"
---

<span id="J2ddOVp9"></span>
## Symptom

During agent usage, Gateway Runtime Registry may fail to promptly identify dynamically added agents, resulting in the following exceptions:


* **Conversation request failure**: Errors including `Agent 'a-xxxxx' no longer exists in configuration` or `unknown agent id` appear when I initiate conversations with the new agents.

* **Configuration failure**: The error message `Skill 'arkclaw-team-project-builder' does not exist` appears when I configure skills or tools for unidentified existing agents. Consecutive errors may also occur when I continue creating new agents.


<span id="uqwAaRY9"></span>
## Solutions

If encountering the above issues, upgrade ArkClaw to the latest BytePlus version (V1.2.1 or above) by performing the following steps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Ongoing conversations may be briefly interrupted during the update. We recommend that you upgrade ArkClaw during off\-peak hours.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page and click the details icon in the upper\-right corner.

3. Click the "Check for updates" button to upgrade ArkClaw to the latest version.

4. After the update is complete, reinitiate a conversation or reconfigure settings to verify system recovery.
