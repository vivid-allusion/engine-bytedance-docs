---
title: "Viewing and fixing security scan issues"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing-and-fixing-security-scan-issues"
---

The **security scan** feature helps ensure the security and compliance of published skills. After you create a skill or generate a new version, the platform automatically runs a security scan on the package contents of the current version to identify potential risks such as hardcoded secrets, malicious code, insecure network access, and non\-compliant resource usage. The scan results can serve as an important basis for skill publishing decisions.

You can view the security scan results to understand the scan status and risk distribution of the current version, and follow the fix recommendations to complete the fix and re\-verify the issues. This can reduce the risk of releasing or distributing a skill with security defects.

> **warning**

> During a security scan, the system performs only offline analysis of the code and configuration files within the skill package. **The security scan cannot replace runtime monitoring, permission review, or manual security review**. Even if all security scan results pass, this only means that no risks covered by the scan rules were detected. The scan cannot cover potential risks across all business scenarios.

## Trigger mechanism

The system **automatically triggers ** a security scan in the following scenarios:

* **Skill creation is complete**

   After a skill is created, the platform automatically triggers a security scan and generates the scan results for the corresponding version. For information about how to create a skill, see [Manually creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills?lang=en).

* **Skill update is complete**

   After you update the skill content and generate a new version, the platform automatically triggers a security scan and generates the scan results for the corresponding version. For information about how to update a skill, see [Updating skills](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills?lang=en).

## Scan scope

|**Scan dimension** |**Description** |
|---|---|
|Package file compliance |Checks the file types, directory contents, and abnormal files in the skill package to identify package contents that do not meet security requirements. |
|Declaration layer security |Checks the skill declaration information and related configurations to identify risks that may lead to permission abuse or capability overreach. |
|Code layer security |Performs static analysis on scripts and code to identify hardcoded secrets, dangerous functions, command execution, and other potential security vulnerabilities. |
|Network and resource usage security |Checks network access, external resource references, and resource usage behavior to identify suspicious connections or insecure calls. |
|Open source compliance |Checks the usage of open\-source components and dependencies to identify potential license and supply chain risks. |
|Threat intelligence |Identifies known malicious files, suspicious signatures, and other security threats based on threat intelligence. |

## Recommended scenarios

|Scenarios |Description |
|---|---|
|**After skills are first created or introduced** |After you create a skill, we recommend that you view the security scan results to check for potential risks in the declaration, code, dependencies, and other related content. |
|**After a skill version update** |After you modify scripts, configurations, dependencies, or external resource references to generate a new version of a skill, we recommend that you view the security scan results of the new version to confirm whether this change **has introduced new security issues**.<br><br>> **tip**<br><br><br>> **The scan results of historical versions cannot reflect the security status of the new version**. If you ignore the newly added risks, you may bring vulnerable dependencies, insecure network access, or unauthorized operations into subsequent invocation flows.<br> |
|**Before a skill is published or goes live** |Before a skill is published to the target skills space or integrated into production workloads, we recommend that you verify the version corresponding to the scan results and confirm that the risks have been mitigated as required for publishing. |
|**When troubleshooting security alerts or anomalies** |When a skill shows suspicious network access or abnormal resource usage, or triggers a security alert, you can view the security scan results to troubleshoot potential risks in the related code, configurations, and resource references. |

## Procedure

### Step 1: Go to the details page of the target skill

Based on the skill creation source, select the corresponding entry to go to the details page of the target skill, where you can view and manage the security scan results for the skill.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab and click the name of the target skill to go to the details page.

### Step 2: View the security scan results

On the skill details page, click the "Security scan" tab. View the **Scan overview** and **Issues** to understand the issue distribution and specific issues of the current skill version. This provides a security basis for subsequent fixes and skill publishing.

> **tip**

> If the security scan page displays **No security scan initiated**, it may be because the existing skill was not scanned automatically, so no scan results are available yet. You can click the "Initiate scan" button to manually trigger a security scan. After the scan is completed, view the risk overview and issue details and handle the related risks based on the fix suggestions.

|**Category** |**Description** |
|---|---|
|Scan overview |Displays the **security scan** execution status, current version number, and the distribution of issues by severity for the current skill version. This helps you quickly understand the task progress and overall security risk of the current version.<br><br><br>*  **① Scan status**<br><br>   Displays the execution status of the security scan for the current skill version, helping you determine whether the scan task is running or completed. It includes the following statuses:<br><br>   * **Security scan passed**: The security scan task is complete.<br><br>   * **The security scan task is queued for execution**: The security scan task is queued for execution, and the results will be updated automatically once it is complete.<br><br>*  **② Current version**<br><br>   Displays the skill version associated with the security scan result. When you are viewing the results, confirm the version number to avoid confusing them with the scan results of other versions.<br><br>*  **③ Risk overview**<br><br>   Aggregates and displays all security issues detected for the current skill version. This section also includes statistics on the number of issues at each of the four risk levels—Critical, High, Medium, and Low—to visually present the overall risk distribution.<br><br>   * **Critical**: The highest risk level. Critical\-level issues may cause major security incidents, sensitive information leakage, or system compromise, and must be fixed first.<br><br>   * **High**: High\-risk issues with a high probability of being exploited, which may noticeably affect the system, data, or business. Fix these issues as soon as possible.<br><br>   * **Medium**: This risk level indicates potential security risks that may affect system security under certain conditions. We recommend that you fix these issues promptly based on their actual impact.<br><br>   * **Low**: The risk impact is relatively low and usually does not cause direct, serious security harm. You can optimize issues at this level at a scheduled time based on your business plan. |
|Issues |Displays the specific security issues detected by the security scan of the current skill version. Each scan result includes the rule, issue severity, issue, and fix suggestion, which can be used to quickly locate the problem file and specific line number and carry out the fix. |

### Step 3: Fix quality check issues

View the various issues detected by the security scan and complete the fixes based on the issue severity, fix suggestions, and file location information.

> **tip**

> We recommend that you handle issues in the order of **Critical \> High \> Medium \> Low** to reduce the impact of security issues on skill operation and improve the overall fix efficiency.

1. In the issue list, view the matched rule, severity, issue description, and fix suggestion of the target issue to determine the cause and the direction for handling it.

2. Click the corresponding file name or line number next to **Issue location** to go to the affected file. For example, when the page shows SKILL **.md:59**, it indicates that the security issue detected by this security scan is located at line **59** of the SKILL **.md** file.

3. After you modify the corresponding content based on the fix suggestion, click the "Save" button.

4. After you confirm that the fixes are correct, click the "Confirm" button to complete the fix. The system automatically updates the skill, generates a new version, and **triggers a security scan for the new version**.

### Step 4: Verify the fix results

After the system completes the **security scan** for the new version, it returns to the **security scan** page of the new version and updates the scan results. In the ** Issues** section, you can confirm whether the original issues have been eliminated and check whether this modification has introduced new security issues. If any original issues remain or new issues are detected, refer to [Step 3 ](https://docs.byteplus.com/en/docs/347/122483#irfLSHJU)to locate the files and line numbers again. Continue fixing until the results meet expectations or all issues are resolved.
