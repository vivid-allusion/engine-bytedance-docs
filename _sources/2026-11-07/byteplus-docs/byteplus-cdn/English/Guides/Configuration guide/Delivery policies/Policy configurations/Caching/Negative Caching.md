---
title: "Negative Caching"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-negative-caching"
---

To reduce the load on your origin server from repeated requests for content that returns an error, you can configure negative caching.

This feature allows BytePlus CDN to cache non\-2xx status code responses (specifically 400\-599) for a set period, preventing frequent origin requests for the same error\-producing content. This guide provides step\-by\-step instructions on how to configure negative caching rules for your domain.

Currently, you can only configure negative caching for status codes within the 400\-599 range.

<span id="steps"></span>
## Steps


1. Open the **Negative Caching** configuration page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**.

   You can add a maximum of 50 rules.

3. Refer to the following configuration instructions.

4. Once the configuration is complete, click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24e177de713f4cd6ae79baad46a5af23~tplv-goo7wpa0wc-image.image) </span>

<span id="configuration-instructions"></span>
## Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Priority |Indicates the priority of the negative caching rule. If you have configured multiple rules, CDN executes the rules based on priority. You can drag rules to adjust their priority. |
|Condition |Specifies the condition for matching a request. This configuration has the following options:<br><br><br>* **URL Path Extension**: Matches requests for files with a specific file extension.<br><br>* **URL Path Directory**: Matches requests for files with a specific directory path.<br><br>* **URL Path**: Matches requests for files with a specific URL path. |
|Patterns |Represents the content of the rule, which cannot exceed 1,024 characters and cannot include the following characters:<br><br><br>* Consecutive slashes (//), spaces, dollar signs ($), question marks (?), Delete (ASCII code 127).<br><br><br>In addition,<br><br><br>* If the rule type is **URL Path Extension**, the rule content must be one or more file extensions separated by semicolons (;). Do not include a leading period (.) in the extensions. For example: png;txt.<br><br>* If the rule type is **URL Path Directory**, the rule content must be one or more directory paths separated by semicolons (;). Directory paths must start and end with a slash (/). For example: /chs/foods/;/us/birds/.<br><br>* If the rule type is **URL Path**, the rule content must be one or more file paths separated by semicolons (;). File paths must start with a slash (/) and can include an asterisk (\*) as a wildcard to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |
|Ignore Case |Indicates whether the matching process is case\-sensitive. The setting is off by default, meaning it is case\-sensitive.<br><br>&nbsp;<br><br>**Example**: If you set the Pattern to png;txt and disable **Ignore Case** (making the match case\-sensitive), the rule matches requests for `HTTPS://www.EXAMPLE.com/food.png`, but cannot match requests for `https://www.example.com/food.PNG`. |
|Status Code |Specifies the status codes to cache. The range of status codes you can enter is 400\-599. You can enter 4xx or 5xx. 4xx represents all status codes from 400 to 499. 5xx represents all status codes from 500 to 599. |
|Cache TTL |Indicates the caching duration.<br><br><br>* If you select **Seconds** as the unit, the maximum caching duration you can enter is 315360000.<br><br>* If you select **Minutes** as the unit, the maximum caching duration you can enter is 5256000.<br><br>* If you select **Hours** as the unit, the maximum caching duration you can enter is 87600.<br><br>* If you select **Days** as the unit, the maximum caching duration you can enter is 3650. |
