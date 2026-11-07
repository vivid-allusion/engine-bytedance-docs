---
title: "Publishing skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills"
---

After a skill has been updated, you need to publish a new version so that the updated capabilities can take effect in the associated **agents**. This topic describes how to publish a skill in the **AgentKit** console.

## Background information

Skills support version management. You can publish different versions of a skill to different skills spaces for use by corresponding **agents**. This is applicable in scenarios such as multi\-version coexistence and grey release.

## Prerequisites

* [The skill has been updated](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills).

* The skill has been added to at least one skills space. For details, see [Adding to skills space](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills_in_Skills_Spaces).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab.

4. On the skill list page, click the name of the target skill to go to the details page.

5. Click the "Publish" button in the upper\-right corner of the page.

6. In the confirmation pop\-up window, select the target skills spaces where you want the publication to take effect. After confirming the selected spaces are correct, click the "Publish" button to complete the publication of the new skill version.

   > **tip**

   > If the message "The quality check results for the current version contain 'P0 Blocked' issues. Please confirm whether you still want to publish." appears during publishing, the current skill version has blocking\-level defects that may affect the executability or security of the version. We strongly recommend that you go to the **Quality check** page, locate and fix all **P0 Blocked** issues, and then publish the skill. For details, see [Viewing and fixing quality check issues](https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-quality-check-issues?lang=en).

## Subsequent steps

After the new skill version is published, you also need to **update the skill version to the newly published version** in the corresponding skills spaces so that the updated capability can be called by **agents**. Refer to [Changing skill versions](https://docs.byteplus.com/en/docs/agentkit/Changing_Skill_versions?lang=en) to switch the skill version.
