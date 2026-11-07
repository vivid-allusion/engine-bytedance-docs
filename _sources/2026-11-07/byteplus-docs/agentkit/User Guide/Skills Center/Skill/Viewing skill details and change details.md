---
title: "Viewing skill details and change details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_version_details_of_Skills"
---

By viewing skill details, you can obtain basic information and code package details of the skill, and manage its versions. You can also view the directory structure and code details of a specified version of the skill to fully understand the implementation content of each version.

## Viewing skills

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. On the "Skill" tab, click the name of the target skill to view the following information.

   > **tip**

   > You can also quickly locate the skills that need to be handled through the**Pending quality improvement**,**Pending risk handling**, and **Pending evaluation** tabs. This reduces the cost of case\-by\-case review and allows you to enter the corresponding workflow based on the issue type.

   * > Pending quality improvement: Aggregates skills with quality\-check issues. This makes it easier to view quality issues centrally and arrange optimization.

   * > Pending risk handling: Aggregates skills with security scan risks. This makes it easier to prioritize issues that may affect compliance or operational security.

   * > Pending evaluation: Aggregates skills whose evaluation has not been completed. This makes it easier to complete the evaluation process and confirm the effect and operational performance of the skills.

   |Tab |Parameter​ |Description |
   |---|---|---|
   |Basic information |Skill metadata |Displays the skill name, ID, and description. |
   ||Quality check |Displays the results of the most recent static quality check for the current skill version, helping you understand the distribution of issues in skill structure, format, resource references, and basic security.<br><br>Click the **View details** button to go to the quality check details page and view the complete report. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-quality-check-issues?lang=en) |
   ||Security scan |Displays the security scan status of the current skill version and the number of issues at each severity level, helping you identify potential security risks in code, configurations, and resources.<br><br>Click the **View details** button to go to the security scan details page and view the complete report. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-security-scan-issues?lang=en) |
   ||Other information |Displays the status, associated project, and other information of the current skill version.<br><br><br>* **Status**: The availability status of the current skill version.<br><br>   * **Available**: Indicates that the skill version has been created and the current version is running. It can be called by **agents**.<br><br>   * **Unavailable**: Indicates that the skill version failed to be created and the current version cannot be called. We recommend checking the file content and metadata, then creating or publishing it again.<br><br>* **Associated project**: The project to which the current skill belongs, which is used to identify the resource management scope. A resource can belong to only one project and can be accessed and used only by users with permissions for that project. |
   ||Skills spaces added |Displays all skills spaces associated with the current skill version. You can view space details here and add or remove the skill to/from spaces. For details, see [Adding to/Removing from skills spaces](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills_in_Skills_Spaces?lang=en). |
   |Skill details |\- |Displays the package directory structure and code details of the **current skill version**, as well as [skill change details](https://docs.byteplus.com/en/docs/347/90864#t9pJMtA5). |
   |Version management |\- |Displays **all version** information for the skill. You can also click "View" to see the basic information for the target version, code package details, [skill change details](https://docs.byteplus.com/en/docs/347/90864#t9pJMtA5), quality check, security scan, and skill evaluation. |

## View skill change details

Skills provide a version comparison feature that allows you to compare the current version against any historical version. You can go to the skill details page to view the differences between versions and get a clear view of the specific changes.

### Prerequisites

You have changed and published a skill. For operation details, see [Updating skills](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills) and [Publishing skills](https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills).

### Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab. In the "Actions" column of the target skill, click the "Details" button.

4. On the skill details page, click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82f2c7ccb4216ac709026b8b0c79c7ea.png) to enable Diff, and select a historical version to compare with the current version.

5. In the "Project files" section, click the target file to view its content changes. The system uses different colors to indicate the status of each change, making version differences easy to identify:

   * Light green: New content.

   * Dark green: Content differences between versions.

   * Red: Deleted content.
