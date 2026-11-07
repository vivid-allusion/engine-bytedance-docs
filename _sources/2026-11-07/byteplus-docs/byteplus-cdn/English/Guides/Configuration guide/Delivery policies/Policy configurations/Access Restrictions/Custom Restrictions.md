---
title: "Custom Restrictions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/custom-restrictions_en"
---

The Custom Restrictions feature in BytePlus CDN allows you to create detailed rules for managing incoming traffic.

By setting conditions based on request attributes like URL path, query parameters, and client IP address, you can control how CDN handles matching requests.

This guide shows you how to configure rules to either block access by responding with a 4xx error or redirect requests to a different URL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


<span id="restrictions-priority"></span>
## Restrictions Priority

The series of access restrictions provided by CDN have different priorities. When CDN processes user requests, these restrictions take effect according to their priorities. Refer to [Access Restrictions Priority](https://docs.byteplus.com/en/docs/byteplus-cdn/access-control-priorities_en).

<span id="steps"></span>
## Steps


1. Open the **Custom Restrictions** configuration page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enable.

3. Click **Add Rule** to add a rule. You can add up to 10 rules.

4. Refer to the following [configuration instructions](https://docs.byteplus.com/en/docs/18/36368#configuration-instructions).

5. After configuring, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0e6bc58b7d5590383ecc38378dd8699d.png) </span>

<span id="configuration-instructions"></span>
## Configuration Instructions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the input requirements of the following configurations, see <a href="https://docs.byteplus.com/en/docs/18/36368#configuration-input-requirements">Configuration Input Requirements</a>.</div>



|**Configuration** |**Description** |
|---|---|
|Rule Name |Specifies the name of the rule. |
|Conditions |Indicates one or more matching conditions used to match requests. Click **Add** to create a matching condition. You can create up to 5 matching conditions. If no conditions are added, the rule applies to all requests.<br><br>&nbsp;<br><br>In each matching condition, you need to set the matching type, comparison type, and matching value. The matching value can be multiple. If the matching type is **User\-Agent**, multiple matching values are separated by a vertical bar (\|). If the matching type is not **User\-Agent**, multiple matching values are separated by a semicolon (;). The relationship between multiple matching values is "OR".<br><br>&nbsp;<br><br>The description of matching types is as follows:<br><br><br>* **URL Path**: Indicates the path in the request URL.<br><br>* **URL Path Directory**: Indicates a directory in the path.<br><br>* **URL Path Extension**: Indicates the extension at the end of the path.<br><br>* **URL Path Regex**: Indicates the path in the request URL, matched by a regular expression.<br><br>* **Request Query String**: Indicates the query string in the request URL.<br><br>* **Request Query Param**: Indicates a query parameter in the request URL.<br><br>* **Client IP**: Indicates the client's IP address.<br><br>* **User\-Agent**: Indicates the User\-Agent header in the request.<br><br>* **Custom Request Header**: Indicates a custom header in the request.<br><br><br>If the matching type is **URL Path RegEx** or **Request Query String**, each matching value is a regular expression. To use these two matching types, please [submit a ticket](https://console.byteplus.com/workorder/create).<br><br>&nbsp;<br><br>Regarding the comparison type, please note:<br><br><br>* **Equal To, Match**: If the request matches any of the matching values, the condition is met.<br><br>* **Not Equal To, Not Match**: The condition is met if the request does not match any of the specified values.<br><br>* **Belongs To Universal Catalog/Not Belongs To Universal Catalog**: Only applicable to **Request Query Param**, indicating a universal catalog of type "general list". The "general list" is used to define a large number of matching values. |
|Request Handling |Indicates how CDN handles requests that meet the matching conditions. Available options:<br><br><br>* **Respond 4xx**: Indicates that CDN responds with a 4xx error code.<br><br>* **Redirect Request**: Indicates that CDN redirects the request to another URL.<br><br><br>If you plan to create multiple rules, **Request Handling** in each rule must be the same. |


When **Request Handling** is **Respond 4xx**, you can set the following additional configurations:


|**Configuration** |**Description** |
|---|---|
|Response Status Code |Indicates the response status code of CDN for requests that meet the matching conditions. You need to set an error code in the range of 400\-499, such as `405`. |
|Response Body |Indicates the content in the response body. The options for this configuration are:<br><br><br>* **System Default**: Indicates that CDN uses the standard response body for 4xx error codes.<br><br>* **Custom**: Indicates that CDN uses a custom response page. You can select a custom page from the **Response Page** drop\-down list. The pages in the drop\-down list is populated from the **Response Pages** tab under the **Universal Catalog** page. To create a custom response page, please [submit a ticket](https://console.byteplus.com/workorder/create). |


When **Request Handling** is **Redirect Request**, you can set the following additional configurations:


|**Configuration** |**Description** |
|---|---|
|Response Status Code |Indicates the response status code of CDN for requests that meet the matching conditions. You can set **301** or **302**. |
|Redirect URL |Indicates a redirect URL. |


<span id="rule-priority"></span>
## Rule Priority

The rules in the rule list have priorities, and the rule with the highest priority takes effect first. When a request matches a rule, that rule is applied and processing stops; subsequent rules are ignored. You can drag the rules to adjust their priority.

<span id="more-information"></span>
## More Information

<span id="configuration-input-requirements"></span>
### Configuration Input Requirements


|**Configuration** |**Input Requirements** |
|---|---|
|Rule Name |The length should not exceed 20 characters and can include letters, numbers, underscores (_), hyphens (\-), and Chinese characters. One Chinese character counts as 3 characters. |
|Conditions |The input requirements for matching values in the matching conditions are as follows:<br><br><br>* If the matching type is **URL Path**, each matching value represents a file path. Each file path must start with a slash (/). You can use one or more asterisks (\*) in the path, each asterisk representing one or more characters. For example: `/www/img/my*image.png`.<br><br>* If the matching type is **URL Path Directory**, each directory in the matching value must start and end with a slash (/). For example: `/www/img/`.<br><br>* If the matching type is **URL Path Extension**, each extension in the matching value does not need to start with a period (.). For example: `png;txt`.<br><br>* If the matching type is **URL Path**, **URL Path Directory**, or **URL Path Extension**, the total length of the matching values should not exceed 1,024 characters and should not contain the following characters:<br><br>   * Consecutive slashes (//), spaces, dollar signs ($), question marks (?), Delete (ASCII code 127).<br><br>* If the matching type is **Request Query Param**, the parameter name and matching value have the following requirements:<br><br>   * You can only specify one parameter name and one parameter value as the matching value.<br><br>   * The length of the parameter name and matching value should not exceed 256 characters.<br><br>   * The parameter name and matching value can include numbers, letters, percent signs (%), underscores (_), and hyphens (\-).<br><br>* If the matching type is **Client IP**, the matching value has the following requirements:<br><br>   * The total length should not exceed 30,000 characters.<br><br>   * The number of IP addresses should not exceed 50.<br><br>   * IP addresses can be IPv4 addresses, IPv4 CIDR addresses, IPv6 addresses, or IPv6 CIDR addresses.<br><br>* If the matching type is **Custom Request Header** or **User\-Agent**, the matching value has the following requirements:<br><br>   * The total length should not exceed 1,024 characters. Except for the beginning and end, the matching value should not contain \*. \* represents one or more arbitrary characters.<br><br>   * The number of matching values should not exceed 50.<br><br>* If the matching type is **Full Path RegEx** or **Request Query String**, each matching value is a regular expression, and the total length should not exceed 1,024 characters. |
|Redirect URL |The URL must start with `http://` or `https://` and should not exceed 1,024 characters in length. |
