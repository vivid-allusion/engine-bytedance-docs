---
title: "Managing sensitive thesaurus"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-sensitive-thesaurus"
---

The Sensitive Thesaurus is a cornerstone of SealSuite’s data identification capability. It allows you to centralize the management of sensitive information, such as specific project names or patterns like ID and employee numbers (using regular expressions).


* **High Reusability:**  Configure a sensitive word once and reference it across multiple classification and grading rules without repetitive manual entry.

* **Professional Accuracy:**  Leverage a vast library of pre\-defined, industry\-standard regular expressions (regex). You can also create copies of these built\-in rules to fine\-tune them for complex compliance requirements.


<span id="5f0e06fb"></span>
## Use Cases

Sensitive Thesaurus is ideal for precisely targeting sensitive data through specific keywords, phrases, or fixed formats.


* **Project and Confidentiality Identifiers**: Identify filenames or content containing project codes or sensitivity labels.

* **Privacy and Compliance Auditing**: Use regex to detect personally identifiable information such as ID numbers, phone numbers, and credit card details.

* **Core Asset Protection**: Monitor the transmission of technical terminology, names of senior executives, or specific financial accounts.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">These resources can be applied to scan both <strong>file name</strong> and <strong>file content</strong>. You can select which scanning dimension to use when configuring classification and grading rules.</div>


2. <div data-tips="true" data-tips-type="tip">To audit <strong>interactive text</strong> in web\-based AI chat tools, you must first add sensitive words here, and then select <strong>file content</strong> as the condition type when configuring classification and grading rules.</div>



<span id="874525d1"></span>
## Prerequisites

Ensure your account has the following permissions. See [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1) for details.


* **Menu Permissions**: **Security** \> **DLP** \> **Data Identification** \> **Sensitive Thesaurus**.

* **Operation Permissions**: **DLP** \> **Data Identification Related Permissions**.


<span id="4ec59f62"></span>
## Navigation Path


1. Log in to the Admin Console.

2. In the left navigation bar, choose **DLP** \> **Data Identification**.

3. Click the **Sensitive Thesaurus** tab at the top of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76d3aa6730d047bf8720e832d974ccdb~tplv-goo7wpa0wc-image.image) </span>


<span id="c5df4d82"></span>
## Adding Sensitive Words

Manually define keywords or regex patterns tailored to your business needs.


1. On the **Sensitive Thesaurus** page, click  **+ Add Sensitive Word**.

2. Configure the following settings in the drawer.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c87564dada8346d19ef885407e2b2f64~tplv-goo7wpa0wc-image.image) </span>

   * **Match Type**: Select a type based on the data characteristics.

      
      |**Match Type** |**Logic** |**Use Case** |
      |---|---|---|
      |**Keywords** |**Exact matching** of the specific text provided. |Best for known terms like project names, sensitivity labels, or specific people. |
      |**Regular expression** |**Pattern matching** for strings that follow a specific format. |Essential for data with fixed patterns but variable values, such as ID numbers, API keys, or database connection strings. |
      |**Dictionary** |Combines multiple **Keywords** or **Regular expression** rules to match sensitive content in batches.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Dictionary rule is supported only on SealSuite client version <strong>3.3.18 and later</strong>.</div><br> |Suitable for complex business information that requires weighted evaluation across multiple keywords or regular expression rules, such as R&D materials, contracts, transaction orders, or bidding documents. |
      

   * **Name**: A descriptive name for the rule. The name must be unique and cannot exceed 50 characters.

   * **Tag** (Optional): Custom labels to help filter and categorize rules later.

   * **Matching Rules**:

      
      |**Settings** |**Description** |**Best Practices & Examples** |
      |---|---|---|
      |**Keywords \- Content** |Enter the text to be identified. |Use for specific identifiers like "Project X" or "Confidential". |
      |**Keywords \- Number of matches** |The minimum number of occurrences required in a single file to trigger a hit. |For highly sensitive words (e.g., "Top Secret"), set to **1**. For common terms (e.g., "Salary"), set to **3–5** to reduce false positives in casual conversation. |
      |**Regular expression \- Content** |Enter the standard regex pattern. |SealSuite includes dozens of built\-in regex patterns for global PII (addresses, IDs, etc.). **We recommend using built\-in patterns first** for higher accuracy. Filter by **Pre\-defined** in the **Creation Type** dropdown to find them.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78cc7e9cff864bc89dc2dca132fdc4e2~tplv-goo7wpa0wc-image.image) </span> |
      |**Regular expression \- Number of matches** |The minimum number of pattern matches required in a single file to trigger a hit. |Set to **10–20** for items like "Phone Numbers" to ignore single mentions but catch bulk data exports. |
      |**Regular expression \- Deduplication enabled?**  |If enabled, identical matches count as a single occurrence. |* **Enabled (Recommended)** : Useful for detecting bulk leaks of different records (e.g., 100 different ID numbers).<br><br>* **Disabled**: Useful for identifying the density of sensitive info, regardless of whether the content repeats. |
      |**Dictionary \- Content** |* **Keywords**: Directly enter the word to be identified.<br><br>* **Regular expression**: Enter a regular expression that defines a character pattern. |For configuration recommendations, refer to the descriptions of **Keywords** and **Regular** **expression** above.<br><br>Click  **+ Add** to add a rule entry. Added rule entries can be edited or deleted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A dictionary can contain up to <strong>500</strong> keywords and regular expression rule entries in total.</div><br> |
      |**Dictionary \- Weight** |* **Rule weight**: Set the weight of each keyword or regular expression rule entry. The value ranges from 1 to 100.<br><br>* **Total weight**: Set the threshold for triggering the dictionary rule, displayed as “At least N to trigger this rule”. The default value is 1. |**Calculation logic**: If the`Keyword rule weight + the Regular expression rule weight >= the Total weight`, the dictionary rule is triggered.<br><br>Assume that the following rule entries are configured in a dictionary:<br><br><br>* Keyword `A`: Weight **2**.<br><br>* Keyword `B`: Weight **3**.<br><br>* Regular expression `X`: Weight **5**.<br><br>* The total weight is set to "At least **5** to trigger this rule".<br><br>   * If **Deduplication enabled?**  is turned on, when the same rule appears multiple times, its weight is counted only once.<br><br>      * If a file contains both Keyword `A` and Keyword `B` multiple times, the total weight is **2 + 3 = 5**, and the rule is triggered.<br><br>      * If a file contains only Regular expression `X`, the total weight is **5**, and the rule is triggered.<br><br>      * If a file contains both Keyword `A` and Regular expression`X`, the total weight is **2 + 5 = 7**, and the rule is triggered.<br><br>      * If a file contains only Keyword `A`, the total weight is **2**, and the rule is not triggered.<br><br>   * If **Deduplication enabled?**  is turned off, when the same rule entry appears multiple times in a file, its weight is accumulated repeatedly.<br><br>      * If a file contains only Keyword `A`, Keyword `A` must appear at least **3 times**. The total weight is **2 + 2 + 2 = 6**, and the rule is triggered.<br><br>      * If a file contains only Keyword `B`, Keyword `B` must appear at least **2 times**. The total weight is **3 + 3 = 6**, and the rule is triggered.<br><br>      * If a file contains only Regular expression `X`, **1** occurrence gives a total weight of **5**, and the rule is triggered. |
      |**Dictionary \- Deduplication enabled?**  |After **Deduplication enabled?**  is turned on, the system handles duplicate matches in the following two scenarios:<br><br><br>* **Duplicate matches of the same rule entry**: If the same rule, such as Keyword `A`, appears multiple times in the text, its weight is counted only once.<br><br>* **Content at the same position matched by different rule entries**: The **content exclusivity principle** applies. Even if the same text segment matches multiple rules, such as both Keyword `A` and Regular expression `A`, the system counts it as only one valid detection and does not accumulate the weight. |**The switch is enabled by default** to prevent the score from being inflated due to repeated occurrences of the same feature in the text. |
      

   * **Manage labels**: Associate the current sensitive word with specific tags (optional). The drop\-down list only displays tags that the current administrator has been granted. By associating tags, you can enforce permission isolation between administrators of different regions or business lines. To add or adjust the visible tag options in the drop\-down list, a super administrator must modify the **Managed tag scope** for your administrator role under **Settings** \> **Admin Access**.

3. Click **Confirm**.


<span id="853f57f9"></span>
## Adding sensitive words in bulk

The sensitive thesaurus supports batch importing keywords, regular expressions, and dictionaries by using templates. The following example describes how to batch import dictionaries by using a template.


1. In the upper\-right corner of the **Sensitive Thesaurus** page, click **Add sensitive words in bulk** \> **Import Template Dictionary**.

2. Click **Download** to get **Sensitive Words Dictionary Import Template**, and fill in dictionary entries according to the template requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6df99d2951a442ff847403cb02465ec8~tplv-goo7wpa0wc-image.image) </span>

3. After completing the template, click **Upload** or directly drag the completed file to import it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file size must be no larger than <strong>10 MB</strong>. If the file exceeds this limit, import it in batches.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the file is uploaded, the system automatically validates whether the table content meets the requirements. If validation fails, modify the template content based on the error message and <strong>upload it again</strong>.   </div>
   


<span id="ccc0c5e8"></span>
## Managing the Sensitive Word List

You can search and manage all rules from the main list page.


|**Field** |**Description** |
|---|---|
|**Sensitive Word Name** |The unique identifier for the rule. |
|**Creation Type** |* **Pre\-defined**: Pre\-defined system rules. The matching logic cannot be modified or deleted.<br><br>* **Custom**: Rules created manually or generated from copies. These are fully editable. |
|**Tag** |Custom classification labels that allow you to quickly filter and locate specific sensitive words. |
|**Match Type** |* **Keywords**: Matches specific text strings.<br><br>* **Regular expression**: Matches strings following a defined character pattern. |
|**Actions** |* **Custom Rules**: You can view **Details**, **Edit**, or **Delete** these rules.<br><br><br>*Note: Rules currently referenced by a Classification and Grading Rule cannot be deleted until the association is removed.* <br><br><br>* **Built\-in Rules**: You can **Create a Copy**. Since built\-in regex logic is deeply optimized for industry standards, the regex patterns themselves are encapsulated and non\-editable. However, creating a copy allows you to fine\-tune settings like match counts and de\-duplication for your specific business needs. |


<span id="4badae26"></span>
## Reusing Pre\-defined Regex

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Any built\-in rules you modified in the old version have been automatically converted to custom rules named "<strong>Original Name_Copy</strong>". Existing policy associations remain intact; no reconfiguration is required.</div>


Built\-in regex rules default to a match count of 1. If this is too strict, use the **Create a copy** feature to adjust the thresholds.


1. In the **Actions** column of a built\-in rule, click **More** \> **Create a copy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22300c0724b2438d90f9d83eb0e67a27~tplv-goo7wpa0wc-image.image) </span>

2. The system suggests a name with a "_Copy" suffix, which you can rename.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef1ac4d85727475cb8a9e59929489350~tplv-goo7wpa0wc-image.image) </span>

3. In the copy, you can modify the **Tag**, **Match Count**, or **De\-duplication** settings. The core regex pattern itself remains locked to ensure accuracy.

4. Once saved, the copy appears as a **Custom** rule in your library.


<span id="a140db8c"></span>
## Next Steps

After configuring your sensitive word library, you must link these rules to a **Classification and Grading Rule** to enforce security. Go to the **Classification and Grading Rules** page and refer to [Managing classification and grading rules](https://docs.byteplus.com/docs/sealsuite/managing-classification-and-grading-rules). By mapping sensitive words to data levels (L1–L4), you can then trigger specific audits or blocking actions in your security policies.
