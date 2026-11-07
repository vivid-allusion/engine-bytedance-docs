---
title: "Import Knowledge Engine"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Import_Knowledge_Engine"
---

Supports the segmented content output to the specified enterprise knowledge engine, supports the output of multiple columns, and the input column of the operator is generally the output column of the knowledge segmentation operator. This article shows you how to use the import knowledge engine operator.

<span id="35eb0dcc"></span>
# Prerequisite

You need to first create a corresponding knowledge base in the enterprise knowledge engine to achieve subsequent knowledge import. For specific operations, please refer to [Create a New Knowledge Base](https://docs.byteplus.com/docs/undefined/69e591f8ad0646055cc24c72).

<span id="7becf5b3"></span>
# Operating instructions

<span id="4f1db1b3"></span>
## New import knowledge engine operator

After the knowledge segmentation operator, click the plus sign + to add the import knowledge engine operator and configure the operator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fd10172062145f99ae37703cfc32623~tplv-goo7wpa0wc-image.image) </span>

<span id="6b9f08cf"></span>
## Configuration parameters

<span id="7af42f76"></span>
### **Export to Knowledge Base**

The parameter configuration of the knowledge base is explained as follows


|parameter |explain |
|---|---|
|import segmented column |Support for selecting multiple columns, usually the output column of the `knowledge segmentation operator`. Can be string type or json serialized Array < string \> type |
|knowledge data name |Support for selecting from upstream nodes as a basis for generating knowledge data names. The file path column or file name column is generally selected, and the system will generate the knowledge data name according to the column name selected by the user.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00c6cf4a637845149bd83a67eed8bf0d~tplv-goo7wpa0wc-image.image) </span> |
|knowledge Base |In the drop\-down box, select the specified knowledge base to import, enabling the selection of user\-created knowledge bases. |


<span id="3192153a"></span>
### Dependency configuration

Configure the data dependencies of tasks, and support configuring upstream dependencies and self\-dependencies


* **Upstream dependencies** support system auto\-configuration and custom configuration.

   * The automatic configuration of the system will automatically generate upstream data dependencies, and you can decide whether to use them according to the actual situation.

   * When selecting a custom configuration, you can manually add data dependencies

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1443d4d51fb459b8121e5d0a54c0f04~tplv-goo7wpa0wc-image.image) </span>

      After entering the new dependency interface, you can search for the corresponding task or dataset to create a dependency, and the corresponding dependency will be generated after selecting the corresponding task. If you need to create a system custom dependency manually, you can contact technical support for assistance.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb503c012c124e5b80a3aa58e92df163~tplv-goo7wpa0wc-image.image) </span>

* **Self\-dependency:** 

   * When the switch is turned on, the current task is dependent on the operation of the task in the past, and supports setting the earliest data backtracking time configuration. If the task of the previous cycle fails, the task of the next cycle cannot be run.

   * When the switch is turned off, the current task does not depend on the operation of the task in the past, and even if the task of the previous cycle fails, the task of the next cycle can be run normally.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e43ea3dfdc22463b9be65ec73b3ca9ca~tplv-goo7wpa0wc-image.image) </span>


<span id="29b6bb62"></span>
### Advanced Configuration

Further configuration of advanced parameters for the operator to perform tasks is supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f17a7702747f4b97b6e2626ceaeb4941~tplv-goo7wpa0wc-image.image) </span>

<span id="45261b13"></span>
### Monitoring configuration

Support setting multiple alarm rules, each alarm rule is set up to 5 alarm conditions, or the logical relationship between the rules, that is, to meet any one will trigger a notification, support the user according to the drop\-down box selection result **abnormal alarm, failure alarm, timeout alarm** 3 types.

When the task execution meets the alarm conditions, it supports notifying the designated user through Feishu, DingTalk, etc

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66914735ab144447af10fc49f170b227~tplv-goo7wpa0wc-image.image) </span>
