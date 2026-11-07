---
title: "Deleting skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_Skills"
---

When the backend service corresponding to a skill has been discontinued, replaced by a new version, or confirmed to no longer be used by any business, you can delete it to clear invalid resources.

> **warning**

* > Deleted skills cannot be restored. After deletion is complete, the skill will be synchronously removed from all associated skills **spaces**, and agents that were previously configured with this skill can no longer call it, which may impact related business operations.

* > Before deleting the skill, we recommend confirming that the target skill is no longer needed. You can go to the skill [details](https://docs.byteplus.com/en/docs/agentkit/Viewing_version_details_of_Skills?lang=en) page to check the reference of this skill in related skills **spaces** and evaluate the impact of deletion on existing agents.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab.

4. In the "Actions" column of the target skill, click the "Delete" button.

5. After you confirm that the deletion information is correct, click the "Delete" button to complete the operation.

   > **tip**

   > If **the skill to be deleted has been added to skills spaces**, we recommend checking the reference of this skill in related skills spaces and calling of this skill by associated agents before the deletion. After verifying that the deletion does not affect existing business, you can proceed.
