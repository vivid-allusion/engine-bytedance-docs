---
title: "UA Restrictions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ua-restrictions"
---

To control which users can access your domain, you can configure User\-Agent (UA) restrictions in BytePlus CDN. This guide explains how to set up an allowlist or a blocklist to permit or deny requests based on their User\-Agent header.

<span id="what-is-user-agent"></span>
## What is User\-Agent

The User\-Agent request header contains information such as the operating system version, CPU type, and browser version of the client initiating the request. Web servers can return different pages based on the values of the "User\-Agent" header.

In CDN, you can use the value of the User\-Agent field to allow or prevent specific users from accessing your domain name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To find common User\-Agent values, search online for "User\-Agent list".</div>


<span id="0ac78b21"></span>
### Empty User\-Agent

An empty User\-Agent refers to an HTTP request that does not include a User\-Agent header.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A request with <code>User-Agent: null</code> is not considered a request with an empty User\-Agent.</div>


<span id="restrictions-priority"></span>
## Restrictions Priority

CDN access restriction features have different priorities. When CDN processes user requests, these restrictions are applied in order of priority. Refer to [Access Restrictions Priority](https://docs.byteplus.com/en/docs/byteplus-cdn/access-control-priorities_en).

<span id="steps"></span>
## Steps


1. Open the **UA Restrictions** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Refer to the following configuration instructions.

4. After configuring, click **Save**.


<span id="configuration-instructions"></span>
### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Filter |The configuration has the following options:<br><br><br>* **Allowlist**: Only requests with a User\-Agent header matching an entry in this list can access your domain name.<br><br>* **Blocklist**: Any request with a User\-Agent header matching an entry in this list are blocked from accessing your domain name.<br><br><br>If a request's User\-Agent header matches the blocklist or does not match the allowlist, the CDN will deny the request and return a 403 response status code. |
|User\-Agent Strings |Enter one or more User\-Agent strings. The length of this configuration must not exceed 30,000 characters. You can enter up to 1,000 User\-Agents. Your User\-Agent entries should comply with the following requirements:<br><br><br>* You can use the wildcard (\*) to represent any number of characters, but `*` can only appear at the beginning or end of a User\-Agent string.<br><br>* User\-Agent cannot contain `**`.<br><br>* Multiple User\-Agents are separated by a vertical bar (`\|`), or one User\-Agent per line. For example: `*curl* \| Mozilla*` .<br><br>* User\-Agent cannot consist solely of whitespace. |
|Requests with Empty User\-Agent |Specifies how the CDN handles requests that have an [Empty User-Agent](https://docs.byteplus.com/en/docs/18/6560#empty-user-agent).<br><br><br>* If **Filter** is set to **Blocklist**, this option is **Allow Requests with Empty User\-Agent**.<br><br>* If **Filter** is set to **Allowlist**, this option is **Deny Requests with Empty User\-Agent**. |
|Ignore Case |Indicates whether the User\-Agent list is case\-sensitive when used to filter requests. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a21a5a1c4ca64a2886595a2fd217bfa7~tplv-goo7wpa0wc-image.image) </span>
