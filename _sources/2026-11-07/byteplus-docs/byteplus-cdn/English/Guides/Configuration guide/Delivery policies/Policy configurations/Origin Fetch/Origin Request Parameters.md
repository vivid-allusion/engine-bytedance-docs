---
title: "Origin Request Parameters"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-query-parameters_1"
---

This document introduces the Origin Request Parameters feature in BytePlus CDN.

<span id="overview"></span>
## Overview

The Origin Request Parameters feature in BytePlus CDN gives you control over the query parameters sent to your origin server. While all user request parameters are passed to the origin by default, this feature allows you to create rules to modify this behavior. You can add, delete, or change specific parameters in origin requests to align with your caching policies or backend application logic.

If you need to modify the query parameters or parameter values included in origin requests, you can create rules in the Origin Request Parameters feature, and define request matching conditions and the actions to perform on origin parameters within these rules.

<span id="preset-rule"></span>
## Preset Rule

There is a preset rule in the Origin Request Parameters feature. This rule applies to all files and always has the lowest priority. If a user request doesn't match any of the rules you create, it will match this preset rule. You cannot delete this preset rule, adjust its priority, or modify the filter type and patterns in this rule. You can only modify the **Query Parameters from User Request** configuration in this rule. The default setting is **Include All**.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4c28c8507fd6f7715fe0d8cc81da25b9.png) </span>

<span id="steps"></span>
## Steps


1. Open the **Origin Request Parameters** configuration page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**. You can add up to 50 rules.

3. Refer to the following configuration description.

4. After configuring, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4a48070d19bd0fba75a16a2d50cd6f08.png) </span>

<span id="configuration-description"></span>
## Configuration Description


|Configuration |Description |
|---|---|
|Priority |Indicates the priority of the rule. When receiving a user request, CDN processes rules based on their order in the list. While processing rules, CDN attempts to match the rule with the user request. If any rule matches the user request, CDN executes the action specified in that rule and stops processing the remaining rules. You can drag rules to adjust their order in the list. |
|Filter Type |Indicates the filter type in the rule. This configuration has the following options:<br><br><br>* **URL Path Extension**: Indicates the extension in the request URL.<br><br>* **URL Path Directory**: Indicates a directory in the request path.<br><br>* **URL Path**: Indicates the request URL path.<br><br>* **URL RegEx**: Indicates matching the request URL through regular expressions. To use this option, please [submit a ticket](https://console.byteplus.com/workorder/create). |
|Patterns |Indicates the content of the rule. The content length cannot exceed 1,024 characters and cannot include the following characters:<br><br><br>* Consecutive slashes (//), spaces, dollar signs ($), question marks (?), Delete (ASCII code 127).<br><br><br>When matching user requests, the patterns are case\-insensitive.<br><br>Additional explanations for this configuration are as follows:<br><br><br>* If **Filter Type** is **URL Path Extension**, the patterns must be one or more file extensions separated by semicolons (;). File extensions don't need to start with a period (.). For example: `png;txt`.<br><br>* If **Filter Type** is **URL Path Directory**, the patterns must be one or more directory paths separated by semicolons (;). Directory paths must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If **Filter Type** is **URL Path**, the patterns must be one or more URL paths separated by semicolons (;). URL paths must start with a slash (/) and can include asterisks (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If **Filter Type** is **URL RegEx**, the patterns are regular expressions used to match the path in the user request URL. See [Configuration Examples](https://docs.byteplus.com/en/docs/18/6590#url-regex-configuration-examples). |
|Query Parameters from User Request |Indicates how query parameters are set in the origin request URL. This configuration has the following options:<br><br><br>* **Include All**: Indicates that the origin request URL includes all query parameters from the user request URL.<br><br>* **Include None**: Indicates that the origin request URL doesn't include any query parameters from the user request URL.<br><br>* **Add Parameters**: Indicates that the origin request URL includes all query parameters from the user request URL, and additionally includes those specified in **Parameters with Values**.<br><br>* **Include Specified**: Includes only the query parameters from the user request that are specified in **Parameters**.<br><br>* **Include All Except**: Indicates that the origin request URL includes all query parameters from the user request URL, except for those specified in **Parameters**.<br><br>* **Set Parameters**: Indicates that the origin request URL includes all query parameters from the user request URL. Additionally, for the query parameters and values you specify in **Parameters with Values**, CDN performs the following actions:<br><br>   * If these query parameters are in the user request URL, CDN will set their values in the origin request URL to the values you specified.<br><br>   * If the user request URL doesn't include these query parameters, CDN will add them to the origin request URL. |
|Parameters |Indicates one or more query parameters, separated by semicolons (;), with a total length not exceeding 1,024 characters. Query parameters can only contain letters, numbers, underscores (_), commas (,), hyphens (\-), periods (.), and exclamation marks (!).<br><br>&nbsp;<br><br>When matching query parameters in the request URL, the parameters in this configuration are case\-sensitive.<br><br>&nbsp;<br><br>This configuration only appears when **Query Parameters from User Request** is set to **Include All Except** or **Include Specified**. |
|Parameters with Values |Indicates one or more key\-value pairs, representing query parameters and parameter values.<br><br>&nbsp;<br><br>The format of key\-value pairs is `key=value`, with multiple pairs separated by semicolons (;), and a total length not exceeding 1,024 characters. Key\-value pairs can only contain characters other than spaces. For example: `size=12-inch;food=pizza;type=pepperoni`.<br><br>&nbsp;<br><br>When matching query parameters in the request URL, the parameters in this configuration are case\-sensitive.<br><br>&nbsp;<br><br>This configuration only appears when **Query Parameters from User Request** is set to **Add Parameters** or **Set Parameters**. |


<span id="url-regex-configuration-examples"></span>
### URL RegEx Configuration Examples


|User Request |Specified URL RegEx |Description |
|---|---|---|
|/a/bbb/image.png |^/a{1,2}.g$ |The regular expression matches the path in the request URL. |
|/aaa/bbb/image.png |/a{1,2}.g |The regular expression matches the path in the request URL. |
|/food/aaa/pngs/image.png ||The regular expression matches the path in the request URL. |
|/aaa/bbb/image.png |aaa. |The regular expression matches `aaa/bbb/image.png` in the request path. |
|/aaa/bbb/image.png |aaa/. |The regular expression matches `aaa/bbb/image.png` in the request path. |
