---
title: "Manage classification and grading rules"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules"
---

The Classification and Grading Rules module serves as the logical orchestration layer of SealSuite's data identification system. Here, administrators combine atomic identification factors—such as sensitive words, file fingerprints, file types, and sources—to define specific rules and assign data classification levels (L1–L9). Once configured, the system automatically determines the security level of a file whenever it matches a rule.

By defining a unified standard for sensitive data identification, administrators can reference these rules in the **Strategy Center** to apply granular controls (e.g., auditing transfers, capturing evidence, or real\-time blocking) based on the file's sensitivity.


* **Efficient Reuse**: Import from over 170 built\-in templates covering PII, industry compliance, and common business data.

* **Flexible Orchestration**: Supports multi\-dimensional "AND/OR" nested logic to handle complex business scenarios.

* **Asset Decoupling**: Rules are independent of the underlying resource libraries. Any updates to a rule are automatically propagated to all associated security policies.


 &nbsp;

<span id="核心概念说明"></span>
## Core concepts

Before defining rules, it is important to understand the components of "Classification and Grading":


* **Classification vs. Grading**

   * **Classification**: Defines "What type of business data is this?" (e.g., Finance, R&D, PII).

   * **Grading**: Defines "How sensitive is the data?" SealSuite supports custom data confidentiality levels (L1~L9). A higher level indicates more critical data.

* **Formula for recognition rules**

   In SealSuite, a complete classification and grading rule consists of the following elements:

   ```Plain
   Rule = Identification Factors + Logical Orchestration (AND/OR/Match Mode) + Data Sensitivity Level (L1–L9)
   ```
   

* **Closed\-loop determination logic**

   The system performs the following process based on preset rules:

   1. **Identify**: Extract file characteristics using word libraries, fingerprints, etc.

   2. **Determine**: Calculate whether the file matches the defined logical criteria.

   3. **Assign**: Automatically tag the matched file with the corresponding classification level.


 &nbsp;

<span id="前提条件"></span>
## Prerequisites


1. The administrator must have the following permissions.

   * **Menu Permissions**: **Security** \> **DLP** \> **Data Identification** \> **Classification and Grading Rules**.

   * **Operation Permissions**: **DLP** \> **Data Identification Related Permissions**.

2. The required custom data confidentiality levels have been defined and enabled in **Sensitive Level Settings**. For more information, see [Managing the Sensitive Level Settings](https://docs.byteplus.com/en/docs/sealsuite/management-grading-settings)

3. **Resource Preparation**: Rules rely on atomic identifiers. Before creating a rule, ensure the following libraries are configured:

   * **Keywords/Regex**: Pre\-load entries in the Sensitive Thesaurus.

   * **Document Features**: Upload samples to the File Fingerprint Library.

   * **Custom Formats**: Add proprietary extensions to the File Type Library.

   * **Data Origins**: Define sources in the File Source Library.


 &nbsp;

<span id="ac3fd311"></span>
## Configuration Approaches

SealSuite offers two configuration paths: importing **built\-in templates** or **manually creating new rules**. You can choose the most suitable approach based on the commonality of your business scenario and your specific customization requirements:

&nbsp;


|**Approach** |**Use Case** |**Advantage** |**Reference** |
|---|---|---|---|
|**Import Template** |General PII (ID numbers, phone numbers), industry compliance (finance, healthcare), or common office documents. |**High Efficiency**: 170+ expert\-tuned rules available for immediate deployment. |[Quick Start: Importing Templates](https://docs.byteplus.com/en/docs/31/91555#120a9062) |
|**Create Custom Rule** |Proprietary corporate assets (project codes, internal employee ID formats, unique technical specs). |**Precision**: Complete control over dimensions and logic to fit unique business processes. |[Advanced: Creating Custom Rules](https://docs.byteplus.com/en/docs/31/91555#2b9467fb) |


<span id="120a9062"></span>
### Quick Start: Importing Templates

Templates are designed with an "Import\-to\-Customize" logic. Once a template is imported, it becomes a standalone custom rule that you can further refine.


1. In the Admin Console, go to **DLP** \> **Data Identification** \> **Classification and Grading Rules**.

2. In the **Built\-in Template Library** section, click the **Built\-in Template** icon on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc4b807f511f43ad92acb3718fd94396~tplv-goo7wpa0wc-topic.webp) </span>

3. Filter rules by industry or language.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60b7d5b2037f4b1793405b4d69253917~tplv-goo7wpa0wc-topic.webp) </span>

4. Click **Details** to preview the dimensions and logic.

5. Select the desired rules and click **Import**.

6. Once imported, you can edit the name, logic, or data level as needed.


<span id="2b9467fb"></span>
### Advanced: Creating Custom Rules

Follow the "Category First, Rule Second" principle to keep your library organized.


1. On the **Classification and Grading Rules** page, click  **+ Create custom category** at the bottom of the left directory tree.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f51e2f7514bc48b69ece2df354ba9e64~tplv-goo7wpa0wc-topic.webp) </span>

2. Enter a name (e.g., "R&D," "Finance") and click **Confirm**.

3. Click  **+ Create Rule** on the right side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91e623c2cb9143bd8c1f2cd48518c9e4~tplv-goo7wpa0wc-topic.webp) </span>

4. Configure the basic information:

   * **Rule name**: A unique, descriptive name.

   * **Data sensitive level**: Assign a sensitivity level (L1–L9).

&nbsp;

      
      |**Level** |**Description** |
      |---|---|
      |**L1 Public** |Data for public consumption or all employees. |
      |**L2 Internal** |General data for internal use; low impact if leaked. |
      |**L3 Confidential** |Business\-critical data; significant negative impact if leaked. |
      |**L4 Restricted** |Core competitive assets or technology; major loss if leaked. |
      |**Custom levels (L5 ~ L9)**  |Go to the Sensitive Level Settings to customize their names and applicable scenarios. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This level is the basis for differentiated control in the <strong>Strategy Center</strong> (e.g., auditing lower levels and blocking higher levels).      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For Windows and macOS, to automatically apply visible labels to matched files, refer to <a href="https://docs.byteplus.com/en/docs/sealsuite/configuring-document-sensitivity-labels">Configuring document sensitivity labels (for Windows and macOS)</a>.      </div>
      

   * **Select category**: Assign the rule to a category.

   * **Manage labels**: Associate the current rule with specific tags (optional). The drop\-down list only displays tags that the current administrator has been granted. By associating tags, you can enforce permission isolation between administrators of different regions or business lines. To add or adjust the visible tag options in the drop\-down list, a super administrator must modify the **Managed tag scope** for your administrator role under **Settings** \> **Admin Access**.

5. Click  **+ Add Configuration Item** to define identification dimensions:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31675d6ccc6f4b36a44d34d999406fbc~tplv-goo7wpa0wc-topic.webp) </span>

   * **File name**: Matches based on the name of the file.

   * **File Type**: Matches based on the file extension.

   * **File Content**: Matches based on data inside the file. You must select this option to audit **interactive text** in web\-based AI chat tools.

   * **File Size**: Matches based on the file's storage size.

   * **File Source**: Matches based on the file's origin (URL, app, or repo).

6. Orchestrate the logical relationships (see the guide below).

7. Click **Confirm**.


<span id="6298c33e"></span>
## Logic Orchestration Guide

Rules use a **three\-layer nested logic** to ensure precision.


* **Layer 1: "AND" Logic between Configuration Items**

   * The outermost layer. Different dimensions (e.g., File name AND File size) are always connected by "AND." All items must match for the rule to trigger.

* **Layer 2: "AND/OR" Logic between Conditions**

   * Inside a single configuration item (e.g., File name), you can create multiple condition blocks. Choose **AND** (all blocks must match) or **OR** (any block can match).

* **Layer 3: "Match Mode" within a Condition Block**

   * Defines how objects within a group are matched:

&nbsp;

      
      |**Match Mode** |**Logic** |**Typical Application** |
      |---|---|---|
      |**Match Any** |The condition is met if any object in the group is found. |General feature identification to broaden coverage. |
      |**Match All** |The condition is met only if **every** object in the group is found. |Correlated feature identification to improve accuracy. |
      |**Match Partial** |The condition is met if a **specific number** of objects are found. |Threshold\-based matching (e.g., must match 2 out of 4). |
      |**Does Not Include Any** |The condition is considered NOT met if any object in the group is found. |Whitelisting/Exclusion logic to filter non\-sensitive noise. |
      


<span id="6631cfc3"></span>
## Managing the Rule List

On the list page, you can monitor and maintain your identification rules.

&nbsp;


|**Field** |**Description** |
|---|---|
|**Name** |The unique identifier for the rule. |
|**Data Sensitivity Level** |The sensitivity level assigned by the rule (L1–L9). |
|**Number of Hit Policies** |The number of policies in the **Strategy Center** referencing this rule. Click the number to view specific policies. |
|**Action** |* **Details**: View the full logical diagram.<br><br>* **Edit**: Modify names, categories, or logic.<br><br>* **Create a Copy**: Clone a rule for rapid adjustment.<br><br>* **Move to...** : Change the rule's category.<br><br>* **Delete**: Only available if the number of hit policies is 0. |


<span id="2d0e5231"></span>
## Next Steps

Classification rules only define what data is sensitive. To actually audit or block file transfers, you must reference these rules in the **Strategy Center**. Refer to the [Outbound file control policy management](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule) documentation for details.
