---
title: "Viewing and fixing quality check issues"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-quality-check-issues"
---

Quality check displays the static quality check results for the **current** skill **version**. It helps you quickly identify potential issues in the structure, formatting, resource references, and security of the skill. The check scope typically includes the skill package structure, **SKILL.md** metadata (such as frontmatter, name, and description), and script parseability. It also covers conventions for referencing resources such as links and reference documents.

The **Check overview** and **Issues** sections show the distribution of issues by level: P0 Blocked, P1 Warning, and P2 Suggestion. You can locate and fix issues based on the matched rules, issue categories, fix recommendations, and file locations.

## Trigger mechanism

The system **automatically triggers** a quality check in the following scenarios:

* **Skill creation completed**: After a **skill** is created, the platform automatically triggers a quality check and generates the check results for that version. For information about how to create a skill, see [Creating skills in Skill Center](https://docs.byteplus.com/en/docs/agentkit/create_skills?lang=en).

* **Skill update completed**: After the skill content is updated and a new version is generated, the platform automatically triggers a quality check and generates the check results for that version. For information about how to update a skill, see [Updating skills](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills?lang=en).

## Check scope

|**Check category** |**Description** |
|---|---|
|Metadata |Checks whether the **frontmatter** and metadata fields in **SKILL.md** (such as **name**, **description**, **compatibility**, and **metadata**) are complete, well\-formed, and parseable. |
|Directory structure |Checks whether the file directory organization, file naming, artifact storage locations, and root directory structure meet the requirements. |
|Markdown |Checks whether the syntax, heading hierarchy, links, and formatting in **SKILL.md** and other Markdown files are correct. |
|Scripts |Checks whether the encoding and syntax of script files, such as Python scripts, meet the requirements, ensuring that the scripts are parseable and executable. |
|Resource references |Checks whether links, attachments, and other resources are referenced correctly. Identifies broken links, unreferenced resources, and excessively deep reference nesting. |
|Security |Checks for potential hardcoded keys, high\-entropy strings, sensitive information, and other security risks. |

## **Recommended scenarios**

* **Creating a new skill or adding a skill to a skills space**

   After you create a new skill or add it to a **skills space**, view the quality check results. This helps identify structural, formatting, security, and executability issues early and avoid publishing a skill with known issues.

* **After a skill version update**

   After you update the skill content and generate a new version, review the quality check results for the new version. This confirms that the changes have not introduced new issues.

* **Issue troubleshooting phase**

   When a skill call fails, returns unexpected responses, or triggers alerts, view the quality check results. Use the results to determine whether there are potential issues in file structure, script syntax, resource references, or rules.

* **Version delivery or go\-live review**

   Before you officially publish a skill, make it publicly available, or integrate it with upstream systems, review the quality check results. Use the results as a quality baseline for version delivery and go\-live review.

## Procedure

> **warning**

* > Quality check results correspond to a specific skill version. The results for each version reflect only the file quality status of that version.

* > After you [update](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills?lang=en) a skill and generate a new version, the system automatically re\-runs the quality check on the new version. When viewing the results, check the version number shown on the page to avoid confusing issues from a previous version with those from the current version.

### Step 1: Go to **the details page of the target skill**

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab and click the name of the target skill to go to the details page.

### Step 2: View the quality check results

On the skill details page, click the "Quality check" tab. The **Check overview** and **Issues** sections help you understand the issue distribution and specific issues for the current skill version, providing a basis for subsequent fixes.

|Category |Description |
|---|---|
|Check overview |Displays the **quality check** execution status, total issue count, and issue count by level for the current skill version. You can use it to quickly understand the task progress and overall quality status.<br><br><br>*  **① Check status and total issue count**<br><br>   Shows the execution status and total issue count for the current skill version's quality check task. You can use it to quickly track task progress and the total issue count.<br><br>*  **② Current version**<br><br>   Shows the skill version that the quality check results belong to. Confirm the version number when viewing results to avoid confusion with results from other versions.<br><br>*  **③ Risk overview**<br><br>   Summarizes all quality issues detected for the current skill version, grouped by level: P0 Blocked, P1 Warning, and P2 Suggestion. You can use it to quickly assess the overall quality status of the skill.<br><br>   * **P0 Blocked**: Indicates critical structural errors, security risks, or non\-executable issues. **We strongly recommend that you fix these issues** to reduce risks related to execution, formatting, and maintainability.<br><br>   * **P1 Warning**: Indicates important compliance issues or potential quality risks. These issues do not block publishing by default, but may affect runtime stability. We recommend that you fix them first.<br><br>   * **P2 Suggestion**: Indicates optimization items related to development best practices, code standards, directory structure, or documentation formatting. These issues do not block publishing by default. You can address them based on your business requirements. |
|Issues |Displays the specific issues found during the **quality check** for the current skill **version**. Each result includes the matched rule, issue category and level, and fix recommendations. You can use it to quickly locate the affected files and line numbers and fix the issues. |

### Step 3: Fix quality check issues

View the issues detected by the quality check. Fix them based on the issue level, fix recommendations, and file location information.

> **tip**

> We recommend that you address issues in the order of **P0 Blocked \> P1 Warning \> P2 Suggestion**. This reduces the impact of fundamental defects on skill execution and improves overall fix efficiency.

1. In the issue list, view the matched rule, severity, issue description, and fix suggestion of the target issue to determine the cause and the direction for handling it.

2. Click the corresponding file name or line number next to **Issue location** to go to the affected file. For example, if the page shows **SKILL.md:3**, the issue is on line **3** of **SKILL.md**.

3. After you modify the corresponding content based on the fix suggestion, click the "Save" button.

4. After you confirm that the fixes are correct, click the "Confirm" button to complete the fix. The system automatically updates the skill, generates a new version, and ** triggers a quality check for the new version**.

### **Step 4: Verify the fix results**

After the system completes the **quality check** for the new version, you are returned to its **quality check** page, where the scan results are updated. In the **Issues** section, confirm whether the original issues have been resolved. Check whether the changes have introduced new quality issues. If any original issues remain or new issues are detected, refer to [Step 3](https://docs.byteplus.com/en/docs/347/122482#6Z5uMhKX) to locate the files and line numbers again. Continue fixing until the results meet expectations or all issues are resolved.
