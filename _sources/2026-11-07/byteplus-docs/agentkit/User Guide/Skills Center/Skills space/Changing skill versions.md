---
title: "Changing skill versions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Changing_Skill_versions"
---

A skill can be continuously iterated and released in multiple versions to adapt to business requirements and feature changes. In a skills space, you can switch an added skill to a specified version for associated agents to call.

> **tip**

> Before changing the version, we recommend confirming the functionality, configuration, and compatibility of the target version to avoid impacting existing business.

## Recommended scenarios

* **Version upgrade**: Switch the current skill to a newly published version to use new features or fixes.

* **Version rollback**: If the new version cannot meet business requirements or has compatibility issues, you can switch back to a previous stable version.

* **Canary verification**: Switch versions in a specified skills space to verify the actual calling results of different versions.

## Prerequisites

* The target skill has at least two published versions.

* A skills space has been created, and the target skill has been added to the space. For details, see [Creating skills spaces](https://docs.byteplus.com/en/docs/agentkit/Skills_space).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skill Space" tab, and click the target skills space name.

4. Click the "Skill management" tab.

5. In the "Actions" column of the target skill, click "Change version".

6. Select the target version from the drop\-down list and click "Confirm" to complete the operation.
