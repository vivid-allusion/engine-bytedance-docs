---
title: "Browser Caching"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-browser-caching"
---

This document describes how to set up the caching behavior of user browsers for requested files in BytePlus CDN.

<span id="overview-of-browser-caching"></span>
## Overview of Browser Caching

To optimize content delivery and control how end\-user browsers cache your files, you can configure browser caching policies in BytePlus CDN. This guide explains the available policies—Always Cache, Follow Origin Directives, and Do Not Cache—and provides step\-by\-step instructions for creating rules that apply these policies to specific files based on their path, directory, or extension.

Browser caching policies relate to the caching behavior indicated in the response from the origin server. When the CDN requests a file from the origin server, the server's response header indicates the caching behavior for that file. The CDN records this response header when it caches the file.

<span id="browser-caching-policies"></span>
## Browser Caching Policies

Browser caching policies specify how the CDN should set the browser's caching behavior. The CDN provides the following browser caching policies:


* Always Cache. The logic of this policy is as follows:

   * This policy applies if the origin's response does not include the `no-cache`, `no-store`, or `private` directives in its `Cache-Control` header. In this case, the CDN adds a `Cache-Control: max-age=N` header to its response to the browser—this header tells the browser to cache the file, with the cache duration (N) being the expiration time you specify in the policy.

* Follow Origin Caching Directives. The logic of this policy is as follows:

   * When responding to user requests, the CDN will include the caching\-related response headers from the origin server for the requested file.

* Do Not Cache. The logic of this policy is as follows:

   * The CDN instructs the browser not to cache the requested file. When responding to user requests, the CDN will include a `Cache-Control: no-store` response header.


<span id="steps"></span>
## Steps


1. Open the **Browser Caching** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**.

   You can add a maximum of 50 rules.

3. Configure the rule using the settings described below.

4. Once the configuration is complete, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2a4d9a4017e977841ca28d86a1573441.png) </span>

<span id="configuration-instructions"></span>
### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Priority |Indicates the caching rule's priority. If there are multiple rules, they are executed based on their priority levels. When a request matches a rule, no further rules are evaluated. You can adjust the priority of a rule by dragging and dropping. |
|Condition |Specifies the matching condition for the rule. This configuration has the following options:<br><br><br>* **URL Path Extension**: Indicates that the rule is used to match requests for files ending with a specific suffix.<br><br>* **URL Path Directory**: Indicates that the rule is used to match requests for files under a specific directory path.<br><br>* **URL Path**: Indicates that the rule is used to match requests for specific files. |
|Patterns |Specifies the pattern to match, which cannot exceed 1,024 characters and cannot include the following characters:<br><br><br>* Double slashes (//), spaces, dollar signs ($), question marks (?).<br><br><br>Additionally,<br><br><br>* If the rule type is **URL Path Extension**, the rule content must be one or more file extensions separated by semicolons (;). Extensions do not need to start with a dot (.). For example: `png;txt`.<br><br>* If the rule type is **URL Path Directory**, the rule content must be one or more directory paths separated by semicolons (;). Directory paths must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If the rule type is **URL Path** , the rule content must be one or more file paths separated by semicolons (;). File paths must start with a slash (/) and can include asterisks (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |
|Caching Policy |Set a caching policy. The options for this setting are as follows:<br><br><br>* **Always Cache**<br><br>* **Follow Origin Caching Directives**<br><br>* **Do Not Cache**<br><br><br>For a description of each policy, see [Browser Caching Policies](https://docs.byteplus.com/en/byteplus-cdn/docs/browser-caching#65c5ae28/31916#65c5ae28). |
|Ignore Case |Indicates whether the matching process is case\-sensitive. The setting is off by default, meaning it is case\-sensitive.<br><br>&nbsp;<br><br>Example: For the file extension rule, you set **Ignore Case** to off. Your entered rule content is `png;txt`. In this case, the rule can match requests for `HTTPS://www.EXAMPLE.com/image.png`, but cannot match requests for `https://www.example.com/image.PNG`. |
|Cache TTL |Specify a time unit and enter the duration for caching. This setting is only valid when **Caching Policy** is set to **Always Cache**. The available settings are as follows:<br><br><br>* If you specify the time unit as **Second**, the range of values you can enter is 0 \- 31536000. 31,536,000 seconds is 365 days.<br><br>* If you specify the time unit as **Minute**, the range of values you can enter is 0 \- 5256000. 5,256,000 minutes is 365 days.<br><br>* If you specify the time unit as **Hour**, the range of values you can enter is 0 \- 8760. 8,760 hours is 365 days.<br><br>* If you specify the time unit as **Day**, the range of values you can enter is 0 \- 365.<br><br><br>A Cache TTL of 0 instructs the browser that the file expires immediately, requiring revalidation for each subsequent request. |
