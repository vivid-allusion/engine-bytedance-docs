---
title: "SWG sensitive word library management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-sensitive-data"
---

The **SWG sensitive word library** is a resource configuration item dedicated to the Secure Web Gateway (SWG) module. Administrators can define specific keywords or regular expressions here to provide matching criteria for text outbound transfer detection in **cloud application control** policies. This helps identify and control sensitive text transmitted through web pages or SaaS clients.

This article describes how to use built\-in sensitive word resources and how to create and maintain enterprise\-specific custom SWG sensitive words.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">To add sensitive words or configure Web data protection policies later, go to <strong>DLP \> Data Identification \> Sensitive Thesaurus</strong>. Select a built\-in sensitive word library or create a custom sensitive word library. Then reference it through classification and grading rules, and apply the rules to Web data protection policies.</div>


<div data-tips="true" data-tips-type="warning">Your existing SWG sensitive words and policies remain available and are not affected by this adjustment.</div>


<div data-tips="true" data-tips-type="warning">For instructions, see <a href="https://docs.byteplus.com/en/docs/sealsuite/managing-sensitive-thesaurus?lang=en">Manage sensitive word libraries</a>, <a href="https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules?lang=en">Manage classification and grading rules</a>, and <a href="https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en">Configure Web data protection policies</a>.</div>


 &nbsp;

 &nbsp;

<span id="敏感词分类"></span>
## Sensitive word categories


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **System Settings** \> **Resource Management** \> **Sensitive Database**.

3. On the **SWG Sensitive Word Library** tab, view sensitive word categories in the tree directory on the left.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/070951278e014451b5afbac19231db54~tplv-goo7wpa0wc-image.image) </span>

 &nbsp;

 &nbsp;

<span id="内置敏感词"></span>
### Built\-in sensitive words

SealSuite provides standard built\-in word libraries that cover healthcare, personal privacy, enterprise trade secrets, business management, and many other areas.


* **Permission description**: System built\-in sensitive word entries support only **previewing** matching logic. Editing, moving, and deletion are not supported.

* **Quick reuse**: To fine\-tune a built\-in word library, click **Create Copy** in the operation column. The system generates an editable custom word entry.


 &nbsp;

 &nbsp;

<span id="自定义敏感词"></span>
### Custom sensitive words

Administrators can create dedicated word libraries based on enterprise\-specific business terms, project code names, and other information.


* **Prerequisite operation**: Before creating a custom sensitive word, click  **+ Create Custom Category** at the bottom of the left directory.

* **Management logic**: Each custom sensitive word entry must belong to a custom category.


 &nbsp;

 &nbsp;

<span id="新建自定义敏感词"></span>
## Create custom sensitive words

Select a custom category directory, click  **+ Create Sensitive Word** on the right side of the page, and configure the following parameters:


* **Name**: Define the display name of the sensitive word entry.

* **Applicable language**: Select the language that applies to the word entry. **General**, **Chinese**, and **English** are supported. The system applies the corresponding word segmentation and matching algorithm based on the selected language.

* **Matching rule**:

   * **Match any**: The policy is triggered if any rule item defined in "Matching content" is matched.

   * **Match all**: The policy is triggered only if all rule items defined in "Matching content" are matched.

* **Matching content**

   You can identify sensitive content in three ways. In the same rule block, multiple input items use a fixed OR matching relationship. Click  **+ Add Rule** and select one of the following identification methods:

   * **Keyword**: Enter plaintext characters directly. You can enter enterprise\-specific project code names, sensitive terms, and more.

   * **Built\-in regex**: Use system built\-in regular expressions, such as mobile numbers, ID card numbers, and bank card numbers.

   * **Custom regex**: An administrator manually writes a specific regular expression to identify enterprise\-specific data formats with fixed formatting rules, such as contract numbers in a specific format.

* **General determination parameters**

   * **Match count**: Set the minimum number of times the keyword must appear in a single file. The entry is considered matched when this value is reached. For example, if this parameter is set to 3, the word must appear at least 3 times in a single file to be considered matched. This helps reduce false positives.

   * **Deduplication**: Determine whether identical matched items are counted repeatedly. After this option is enabled, identical matching results are counted only once. For example, if the same ID card number appears 100 times in one outbound transfer, it usually represents information about one person. However, 100 different ID card numbers indicate a potentially large\-scale leak.


 &nbsp;

 &nbsp;

<span id="词库运维与管理"></span>
## Word library operations and management

Administrators can view resource distribution on the **SWG Sensitive Word Library** page and maintain existing sensitive word entries by adjusting categories and updating content.

 &nbsp;

 &nbsp;

<span id="资源概览与分类检索"></span>
### Resource overview and category search


* **Data dashboard**: The top of the page displays resource statistics, including the total number of sensitive words, custom entries, and built\-in entries. This helps administrators understand the current resource structure.

* **Multi\-dimensional filtering**:

   * **Search**: Search sensitive word names by keyword.

   * **Conditional filtering**: Filter by **applicable language** (general/Chinese/English), **matching type** (keyword/regex), or both.

* **Directory switching**: Use the tree directory on the left to quickly switch between system built\-in categories and custom categories created by Administrators.


 &nbsp;

 &nbsp;

<span id="自定义敏感词管理动作"></span>
### Custom sensitive word management actions

For entries in custom directories, the operation column provides the following management features:

&nbsp;


|Operation item |Execution logic and description |
|---|---|
|**Preview** |View detailed information about the current word entry, including its applicable language, matching rule, and specific configuration content. |
|**Edit** |Go to the configuration page and modify all parameters of the word entry, including the matching rule, hit count, and deduplication setting. |
|**Create Copy** |Quickly clone the current word entry. The system generates a new entry with identical configurations. This helps administrators create similar matching rules. |
|**Move to.../Batch Move** |Adjust the custom category to which the word entry belongs. Administrators can migrate it to another custom\-level directory that has been created. |
|**Delete/Batch Delete** |Permanently remove one or more sensitive word entries. **Caution**: If the word entry is referenced by "cloud application control" policies, the corresponding policy logic becomes invalid after deletion because it loses its matching criteria. Confirm policy associations before this operation. |


 &nbsp;

 &nbsp;

<span id="应用词库"></span>
### Apply word libraries

This section applies only to maintaining legacy policies. Existing legacy policies continue to use the original SWG sensitive word library. Related configurations are not affected by the entry point adjustment.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">For new data protection policies, use the new entry point: Prepare a sensitive word library in <strong>DLP \> Data Identification \> Sensitive Thesaurus</strong>, reference it through <strong>classification and grading rules</strong>, and then go to <strong>DLP \> Strategy Center \> Control Strategy \> Network DLP</strong> to add the classification and grading rules to a policy. Do not continue using the legacy process to create application protection policies in "cloud application control".</div>


<div data-tips="true" data-tips-type="warning">For instructions, see <a href="https://docs.byteplus.com/en/docs/sealsuite/managing-sensitive-thesaurus?lang=en">Manage sensitive word libraries</a>, <a href="https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules?lang=en">Manage classification and grading rules</a>, and <a href="https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en">Configure Web data protection policies</a>.</div>
