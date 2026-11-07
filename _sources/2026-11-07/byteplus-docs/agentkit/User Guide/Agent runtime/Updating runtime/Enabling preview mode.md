---
title: "Enabling preview mode"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Enabling_preview_mode"
---

Preview mode is enabled by default. It isolates the version under testing from production, preventing changes made during testing from affecting production.

<span id="dmtQI8Ni"></span>
## Usage notes

Preview mode is enabled by default and cannot be disabled once enabled. After preview mode is enabled, the system distinguishes between the **Latest version** and the **official version**.


* **Latest version**: Supports modifying runtime configurations and initiating testing and evaluation.

* **Official version (read\-only)** : You can view the version but cannot modify it. To make changes, modify the **Latest version** and republish the agent.


For agents without preview mode enabled, the system does not distinguish between the **Latest version** and the **official version**. All changes are directly applied to the current version in production and take effect immediately after publishing.

<span id="lHNrneeP"></span>
## Procedure

Preview mode can be enabled in the following two ways.

<span id="EXZtzd3S"></span>
### Enable when creating an agent

Preview mode is enabled by default when you create an agent. During creation, go to **Basic configuration \> Preview mode**. Ensure preview mode is switched on, and then create the agent.

<span id="nlf0LutZ"></span>
### Enable on the agent details page

If preview mode was not enabled when the agent was created, follow these steps:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When the agent is in the <strong>Publishing</strong> state, preview mode cannot be enabled. Wait until publishing is complete before proceeding.</div>



1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Agent Runtime".

3. Click the target agent runtime name to go to its details page.

4. Click "··· \> Enable preview mode".

5. In the dialog box that appears, click "Enable".

   After preview mode is enabled, you can modify runtime configurations in the **Latest version** and initiate testing or evaluations. Once the results meet your expectations, [release](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes) the Latest version as the official version to apply the changes to production.
