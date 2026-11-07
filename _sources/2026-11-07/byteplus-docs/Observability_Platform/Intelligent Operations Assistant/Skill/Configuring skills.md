---
title: "Configuring skills"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_skills"
---

A skill is a standardized capability package encapsulated for specific business scenarios. Configuring skills for an agent provides it with a complete set of operational specifications, enabling it to autonomously identify intent, complete professional tasks based on defined workflows, and deliver practical execution capabilities. Intelligent O&M assistant offers open skill management capabilities, allowing skills derived from observability experience to be uploaded to the platform for use. This topic describes how to upload and manage skills in the intelligent O&M assistant.

> **tip**

> For the complete skill usage workflow, see [Custom agent use cases](https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_Intelligent_Operations_Assistant#9ALnhE5L).

## Built\-in skills

The intelligent O&M platform provides multiple built\-in skills. They cover session diagnostics, capacity and performance metric analysis, root cause identification, health checks, and trace troubleshooting. Use them as needed.

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Skill** to view all built\-in skills preset by the system on the "Built\-in Skills" tab.

## Upload a skill

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Skill**.

3. Click  **"Upload skill"** , select a ZIP file that meets the requirements in the pop\-up window, and click  **"Upload skill"**  after confirming that the file is correct.

   > **tip**

   * > `SKILL.md` must be located in the root directory of the folder. Otherwise, the upload will fail.

   * > After decompression, there must be exactly one folder, and its name must be consistent with the skill name defined in `SKILL.md`.

## Add a skill

After skills are uploaded to the platform, you can add them to custom expert agents. The VeOps Agent is enabled by default.

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Skill**.

3. Click  **"Add"**  on the target skill card.

4. Select the agent to which you want to add the skill, and click  **"Add"**  at the bottom of the pop\-up window.

## Download a skill

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Skill**.

3. Click  **"View details"**  on the target skill card.

4. On the skill details page, click `"..."` in the upper\-right corner  and select **Download** to download the skill ZIP file locally.

## Delete a skill

> **warning**

* > Custom expert agents to which this skill has already been added will no longer be able to call it.

* > Deleted skills cannot be recovered. Proceed with caution.

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Skill**.

3. Click  **"View details"**  on the target skill card.

4. On the skill details page, click `"..."` in the upper\-right corner  and select **Delete** if you no longer need the skill.
