---
title: "Adding/Removing skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills"
---

Skills must be added to **skills spaces** before they can be retrieved and called by agents. This topic describes how to add an existing or newly created skill to a skills space, as well as how to remove a skill that is no longer used from the space.

## Prerequisites

* A skill has been created. For details, see [Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills).

* You have created a skills space. For details, see [Creating skills spaces](https://docs.byteplus.com/en/docs/agentkit/Skills_space).

## Add a skill in a skills space

You can add existing skills to a skills space, or create a new skill during the adding process.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills spaces" tab, and click the name of the target skills space.

4. Select the "Skill management" tab, then click the "Add skill" button.

5. Select one of the following methods to add a skill as needed **.**

   * **Add an existing skill**: Select the target skill and its version, then add it to the current skills space.

   * **Create and add a skill**

      1. Click the "Create skill" button to enter the skill creation page and complete the configuration. For details, see [Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills).

      2. After the new skill is created, return to the current page and, under "Select existing", find and select the newly created skill and add it to **the current skills space**.

6. After confirming that the selected skill and version information are correct, click the "Confirm" button to complete the operation.

## Remove a skill from a skills space

> **warning**

> After a skill is removed from a skills space, agents will no longer be able to retrieve or use this skill when calling that space. Please proceed with caution.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills spaces" tab, and click the name of the target skills space.

4. Click the "Skill management" tab.

5. In the "Actions" column of the target skill, click the "Remove" button.

6. After confirming that the removal information is correct, click the "Remove" button to complete the operation.

   > **tip**

   > Once removed, the skill will no longer belong to the current skills space, but the skill itself will not be deleted. To use it later, you can re\-add it to the corresponding space.
