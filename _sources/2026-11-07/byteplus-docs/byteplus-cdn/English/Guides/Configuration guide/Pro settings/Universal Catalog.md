---
title: "Universal Catalog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en"
---

<span id="universal-catalog"></span>
# Universal Catalog

<span id="overview"></span>
## Overview

Universal Catalog centrally manages reusable rule lists. The following CDN features can reference a Universal Catalog:


* Most match conditions in the Rule Engine

* IP Restrictions

* Referer Restrictions

* The **Query Parameter** match condition in Custom Restrictions


Universal Catalog supports large rule lists. For example, an IP denylist can contain up to 30,000 rules.

After you update a Universal Catalog, the changes take effect immediately for domains associated with policies that reference it.

<span id="create-a-universal-catalog"></span>
## Create a Universal Catalog

<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN console](https://console.byteplus.com/cdn).

2. In the navigation pane, choose **Advanced Settings** \> **Universal Catalog**.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260907091942-1043409360161.png) </span>

3. Click **Create**.

4. Enter a name, then select a **Resource Type** and **Project**.

   * The name can contain Chinese characters, letters, numbers, and underscores (`_`). It must contain 3 to 45 characters. Each Chinese character counts as three characters.

5. Configure rules for the selected resource type:

   * [IP Restrictions](https://docs.byteplus.com/en/docs/18/36264#ip-restrictions)

   * [Referer Restrictions](https://docs.byteplus.com/en/docs/18/36264#referer-restrictions)

   * [General Lists](https://docs.byteplus.com/en/docs/18/36264#general-lists)

6. Click **Create**. You can later click **Edit** on the details page to update rules, or select the Universal Catalog on a configuration page that supports it.


<span id="ip-restrictions"></span>
### IP Restrictions

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260910110614-220153353121.png) </span>


|Setting |Description |
|---|---|
|Resource Type |Select one of the following options:<br><br><br>* **IP Allowlist**: CDN allows a request only when its source IP address matches a rule.<br><br>* **IP Denylist**: CDN rejects a request when its source IP address matches a rule. |
|Rules |Enter IP addresses or CIDR blocks. IPv4 and IPv6 formats are supported. You can enter up to 30,000 rules. Separate multiple rules with semicolons (`;`) or enter each rule on a new line. You can also upload a `.txt` file that contains the rules. Duplicate rules are automatically removed and do not count toward the limit. |
|Client IP Source |Specifies the source that CDN uses to determine the client IP address.<br><br>&nbsp;<br><br>The following options are available:<br><br><br>* **Default**: CDN uses the actual connection IP to determine the client IP address. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br>* **Custom**: Select one or more sources from the actual connection IP, the `X-Forwarded-For` header, and the `X-Real-IP` header to determine the client IP address. If CDN cannot obtain an IP address from a selected header, it uses the actual connection IP.<br><br>   * For an IP denylist, CDN rejects the request if any IP address obtained from the selected sources matches a rule.<br><br>   * For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match rules. |


<span id="referer-restrictions"></span>
### Referer Restrictions

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260910110649-560271205907.png) </span>


|Setting |Description |
|---|---|
|Resource Type |Select one of the following options:<br><br><br>* **Referer Allowlist**: CDN allows a request only when its `Referer` header matches a rule.<br><br>* **Referer Denylist**: CDN rejects a request when its `Referer` header matches a rule. |
|Rules |Enter domain names, IP addresses, or CIDR blocks to match the hostname in a request's `Referer` header. URLs are not supported. IPv4 and IPv6 formats are supported for IP addresses and CIDR blocks. Wildcard domain names are supported. You can enter up to 4,000 rules. Separate multiple rules with semicolons (`;`) or enter each rule on a new line. You can also upload a `.txt` file that contains the rules. Duplicate rules are automatically removed and do not count toward the limit. |
|Ignore Case |Specifies whether the rules are case\-sensitive. |
|Requests with an empty Referer |An empty Referer means that the `Referer` header is missing or has an empty value.<br><br>&nbsp;<br><br>The console displays one of the following options based on the selected resource type:<br><br><br>* When **Referer Allowlist** is selected, **Block requests with an empty Referer** is displayed. When selected, CDN rejects requests with an empty Referer. When cleared, CDN allows requests with an empty Referer.<br><br>* When **Referer Denylist** is selected, **Allow requests with an empty Referer** is displayed. When selected, CDN allows requests with an empty Referer. When cleared, CDN rejects requests with an empty Referer. |


<span id="general-lists"></span>
### General Lists

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260907092306-914207998717.png) </span>

A General List is neither an allowlist nor a denylist. It determines whether a value is in a list. For example, in [Custom Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/custom-restrictions_en), you can use a **Query Parameter** match condition to determine whether the value of a specified query parameter belongs to a General List.


|Setting |Description |
|---|---|
|Match Type |Specifies how rules are matched. You cannot change this setting after you create the General List.<br><br>&nbsp;<br><br>The following options are available:<br><br><br>* **Exact Match**: Matches a value against strings in the rules.<br><br>* **Regex Match**: Matches a value against regular expressions in the rules.<br><br>* **IP Match**: Matches an IP address against IP addresses or CIDR blocks in the rules. |
|Rules |Enter each rule on a separate line, or upload a `.txt` file that contains the rules. Duplicate rules are automatically removed and do not count toward the limit.<br><br>&nbsp;<br><br>Enter content and observe the following limits for the selected match type:<br><br><br>* **Exact Match**: Enter strings. You can use the wildcard character `*` to represent any characters, but it can appear only at the beginning or end of a string. You can enter up to 4,000 rules with a total length of up to 200,000 characters.<br><br>* **Regex Match**: Enter regular expressions. You can enter up to 30,000 rules with a total length of up to 200,000 characters.<br><br>* **IP Match**: Enter IP addresses or CIDR blocks. You can enter up to 30,000 rules. |


<span id="update-a-universal-catalog"></span>
## Update a Universal Catalog

You can update rules by using one of the following update modes:


* **Replace All**: Replaces all existing rules with the rules you enter.

* **Add Rules**: Adds the rules you enter to the existing rules.

* **Remove Rules**: Removes the rules you enter from the existing rules.


For a General List, you cannot change the **Match Type** after creation.

After you update a Universal Catalog, the changes take effect immediately for domains associated with policies that reference it.

<span id="steps"></span>
### Steps


1. In the navigation pane, choose **Advanced Settings** \> **Universal Catalog**.

2. Find the Universal Catalog that you want to update and click **Edit**.

3. On the **Configuration Details** page, select an **Update Mode**, enter rules, and then click **Save Changes**.


The following example shows the page for updating an IP denylist.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260907092533-14470699646.png) </span>

<span id="export-universal-catalog-content"></span>
## Export Universal Catalog content

You can export rules and the associated domain list from a Universal Catalog. Files are exported in `.txt` format.


|Content |File name format |
|---|---|
|Rules |`CDN_<catalog-name>_Rule_<export-time>` |
|Associated domain list |`CDN_<catalog-name>_Domain_<export-time>` |


`<export-time>` uses the `YYYYMMDDHHMMSS` format. For example: `CDN_test_Rule_20230518114139`.

<span id="steps"></span>
### Steps


1. On the **Universal Catalog** page, find the target Universal Catalog and click **Edit**.

2. Above the **Rules** section on the **Configuration Details** page, click **Export** to export rules.

3. Above the **Associated Domains** section, click **Export** to export the associated domain list.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260907092629-868056248833.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260907092710-850178735999.png) </span>
