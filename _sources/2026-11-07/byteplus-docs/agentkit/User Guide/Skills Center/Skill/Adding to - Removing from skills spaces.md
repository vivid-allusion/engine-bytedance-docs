---
title: "Adding to/Removing from skills spaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills_in_Skills_Spaces"
---

Skills must be added to skills spaces before they can be retrieved and called by **agents**. This topic describes how to add a skill to one or more skills spaces, as well as how to disassociate a skill from a specified skills space.

## Recommended scenarios

|Add/Remove |Scenarios and descriptions |
|---|---|
|Add a skill to skills spaces |* **Extend agent capabilities**<br><br>   To add specific task processing capabilities for an **agent**, you can add the corresponding skills to its associated skills space.<br><br>* **Centrally manage multiple skills**<br><br>   When a business scenario requires multiple skills, you can add them to the same skills space for unified management and calling.<br><br>* **Isolate business scenarios**<br><br>   When different businesses, projects, or environments require different skill combinations, they can be added to the corresponding skills spaces to enable category management and resource isolation.<br><br>* **Publish a new skill for use**<br><br>   After creating and validating a skill, you can add it to the target skills spaces so that associated **agents** can call it. |
|Remove a skill from a skills space |* **Disable business capabilities**<br><br>   When related businesses no longer require a certain capability, you can disassociate the skill from the corresponding skills spaces.<br><br>* **Replace a skill**<br><br>   When an existing skill is replaced by another skill with the same or better capabilities, you can remove the original skill.<br><br>* **Adjust capabilities within a space**<br><br>   If you need to adjust the capability scope of a skills **space**, you can remove skills that are irrelevant to the current business scenario.<br><br>* **Isolate issues**<br><br>   If a skill is found to have exceptions, security risks, or compatibility issues, you can temporarily remove it to avoid affecting the operation of associated **agents**.<br><br>* **Govern resources**<br><br>   During periodic resource cleanup, you can remove skills that have not been used for a long time or are configured redundantly to reduce management costs. |

## Prerequisites

* You have created a skill. For details, see [Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills).

* You have created a skills space. For details, see [Creating skills spaces](https://docs.byteplus.com/en/docs/agentkit/Skills_space).

## Add a skill to skills spaces

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab.

4. On the skill list page, click the name of the target skill to go to the details page.

5. On the **Basic information** page, in the **Skills spaces added** section, click the "Add" button.

6. In the **Add to skills spaces** dialog box, configure the skill version and target spaces:

   * Click the "Select the version to add to the space" drop\-down list and select the skill version to be added to the space.

   * In the "Select skills space" drop\-down list, select one or more target spaces.

7. After confirming the version and space information, click the "Confirm" button to complete the operation.

## Remove a skill from a skills space

> **warning**

* > The remove operation only disassociates the skill from the specified **skills space** and does not delete the skill.

* > After a skill is removed from a **skills space**, **agents** will no longer be able to retrieve or use this skill when calling that space. Before performing the removal operation, we recommend confirming that the target skill is not relied upon by relevant **agents** or business processes.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab.

4. On the skill list page, click the name of the target skill to go to the details page.

5. In the **Skills spaces added** section, find the target skills space and click the "Remove from this skills space" button in the "Actions" column.

6. After confirming the removal information is correct, click the "Remove" button to complete the operation.
