---
title: "Data Rate Limiting"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-data-rate-throttling"
---

This topic describes how to configure Data Rate Limiting in BytePlus CDN.

Data Rate Limiting caps the data transfer rate for each request. During traffic spikes, it helps reduce peak bandwidth usage and provides a more consistent data transfer rate across requests. You can create rules that set a maximum data transfer rate for requests matching specified conditions. When a request matches a rule, BytePlus CDN applies the rate limit configured in that rule.

<span id="steps"></span>
## Steps


1. Open the **Data Rate Limiting** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Refer to the following configuration instructions.

4. After configuring, click **Save**.


<span id="configuration"></span>
## Configuration


|**Setting** |**Description** |
|---|---|
|Priority |The priority of the rule. A rule with a priority of 1 has the highest priority. When BytePlus CDN receives a request, it evaluates the rules in descending order of priority. After the request matches a rule, BytePlus CDN applies that rule and stops evaluating subsequent rules. You can drag rules to change their priority. |
|Schedule |The days and time range during which the rule is active. You can select one or more days from Monday through Sunday, or select **Every Day**. The time range is accurate to the minute and uses UTC+08:00. |
|Match Type |The type of condition used to match requests. The following options are available:<br><br><br>* **Path Extension**: Matches requests for files with the specified extensions.<br><br>* **Path Directory**: Matches requests for files under the specified directory paths.<br><br>* **Full Path**: Matches requests for the specified URL paths.<br><br>* **Path Regex**: Matches requests by applying regular expressions to URL paths.<br><br>* **All Files**: Matches all requests. |
|Match Value / Pattern |The values or patterns used to match requests. The total length cannot exceed 1,024 characters. For non\-regex match types, the value cannot contain consecutive slashes (`//`), spaces, dollar signs (`$`), question marks (`?`), or Delete (ASCII code 127).<br><br>The input requirements depend on **Match Type**:<br><br><br>* If **Match Type** is **Path Extension**, enter one or more file extensions separated by semicolons (`;`). Do not include a leading period (`.`). For example: `png;txt`.<br><br>* If **Match Type** is **Path Directory**, enter one or more directory paths separated by semicolons (`;`). Each directory path must begin and end with a slash (`/`). For example: `/chs/foods/;/us/birds/`.<br><br>* If **Match Type** is **Full Path**, enter one or more URL paths separated by semicolons (`;`). Each path must begin with a slash (`/`) and can include an asterisk (`*`) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If **Match Type** is **Path Regex**, enter one or more regular expressions used to match URL paths.<br><br>* If **Match Type** is **All Files**, **Match Value / Pattern** is unavailable because the rule applies to all requests. |
|Throttling Method |The method used by the rule to limit the data transfer rate. |
|Rate Limit |The data transfer rate threshold. The supported range is 1 B/S–1,000,000 GB/S, using a base of 1,024. If the data transfer rate of a request exceeds this threshold, BytePlus CDN limits the rate to the configured value. |
|Effective After |The amount of data that can be transferred before the rate limit takes effect. The supported range is 0 B–1,000,000 GB, using a base of 1,024. For a request that matches the rule, BytePlus CDN applies the rate limit after transferring the specified amount of data. If this value is set to `0`, the rate limit takes effect from the first byte. |


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260920092147-1600496193117.png) </span>
