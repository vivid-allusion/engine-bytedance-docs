---
title: "OpenAPI Management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-manage-sealsuite-openapi-access-key"
---

SealSuite provides a comprehensive set of OpenAPIs that allow you to deeply integrate your existing enterprise IT systems for automated management. This guide covers the essential first steps for developers, explaining how to use the Open Platform, create and manage the Access Keys required for authentication, and audit API call logs for security and compliance.

<span id="9d00b5cb"></span>
# SealSuite Open Platform

To support your development efforts, SealSuite provides a centralized developer hub — the **Open Platform**.

<span id="c7cef048"></span>
## Platform Overview

The SealSuite Open Platform is a comprehensive resource center featuring API documentation, integration guides, event subscriptions, and changelogs. It provides enterprise developers and partners with an online, real\-time resource portal to facilitate efficient and secure system integration.

Key resources available on the platform:


* **Capabilities Overview:**  Explore available APIs and events across authentication, organizational structure, endpoint management, and security controls.

* **Integration Guides:**  Master the standard flows for obtaining access tokens, constructing API requests, and subscribing to Webhook events.

* **API Reference:**  Consult detailed technical specifications for every API, including request parameters, response structures, and code samples.

* **Changelog:**  Stay informed about new features, breaking changes, and deprecations in each version.


<span id="783b5cc0"></span>
## How to Access


1. Log in to the Admin Console.

2. Click your Avatar in the top navigation bar and select **Open Platform**.

3. The platform homepage will open in a new browser tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26c32f30edf14b7bb67acb32c5b58d5c~tplv-goo7wpa0wc-image.image) </span>


<span id="9b28c26c"></span>
# Managing Access Key

An **Access Key** is the core credential used to authenticate your identity and authorize permissions when calling the SealSuite OpenAPI. Before using the API, you must create an Access Key in the Admin Console to grant API access to specific employees or scopes.

<span id="03b64d25"></span>
## Creating an Access Key


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **Integration** \> **API**.

3. In the upper right corner of the **API** page, click **Create Access Key**.

4. In the **Create Access Key** dialog box, complete the following configurations and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1996e75a23854ff1a646f3efca993370~tplv-goo7wpa0wc-image.image) </span>

   The description of configuration items is as follows:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Group Permission** |Set the scope of users who can use the current Access Key, which can be either **All** or **Custom** departments.<br><br><br>* **All**: All employees within the enterprise can use this Access Key to call OpenAPI.<br><br>* **Custom**: In the **Search department** drop\-down list, you can add multiple departments. Afterward, only employees within the specified departments can use this Access Key to call OpenAPI. |
   |**Select from below permissions** |SealSuite OpenAPI is divided into a total of 68 permissions based on functional modules. You can configure the API permission scope for the access key based on your requirements. |
   |**Used for** |Enter a custom description to identify the purpose of the access key. |
   |**Expiration date** |Set the validity period of the current Access Key.<br><br><br>* **Never expires**: The Access Key remains valid permanently after it is created.<br><br>* **Custom date**: The Access Key will be disabled on the selected date. After it expires, new OpenAPI call requests will be rejected. To extend the validity period, see [Modify the Access Key Expiration Date](https://docs.byteplus.com/docs/sealsuite/docs-manage-sealsuite-openapi-access-key#d284e161). |
   |**Access Key Rate Limit** |Set an overall frequency limit for API calls made with this access key. The default value is 100 QPS. |
   |**API Usage Limit** |Set a frequency limit for calls to a single API made with this access key. The default value is 20 QPS. |
   |**IP allowlist** |Set the IP address allowlist for API requests. The supported formats are:<br><br><br>* IP range such as 192.0.2.1\-192.0.2.2.<br><br>* CIDR such as 192.0.2.0/24 or 203.0.113.0.<br><br><br>Use commas or spaces between multiple IP addresses. |
   

5. After creating the access key, obtain the **Access Key ID** and **Secret Access Key** from the list.

   * Ensure that the Access Key status is enabled. For detailed information, please refer to [Enabling or disabling Access Key](https://docs.byteplus.com/docs/sealsuite/docs-manage-sealsuite-openapi-access-key#d7717a7a).

   * Click **Show** to view **Secret Access Key** in the **Access Key Details** dialog box. You can directly copy the Access Key ID or Access Key Secret in the dialog box.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f409c862c75a4e37b5700495a8440ac0~tplv-goo7wpa0wc-image.image) </span>


<span id="d7717a7a"></span>
## Enabling or disabling Access Key

The created Access Key supports manual disabling. After disabling, users cannot use the Access Key to call OpenAPI. It can be re\-enabled later as needed.

On the **API** page, locate the specified Access Key, click **Enable** or **Block** in the **Action** column.


* **Block**: When the Access Key is enabled, you can choose to disable it as needed. After disabling, users cannot use the Access Key to call OpenAPI anymore.

* **Enable**: When the Access Key is disabled, you can choose to enable it as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04a526945bf046a598d8ccee4f943cf5~tplv-goo7wpa0wc-image.image) </span>


<span id="257814fc"></span>
## Viewing or editing Access Key details

At the top of the **API** page, you can quickly filter Access Keys by usage, status, last used date, creation date, expiration date, and expiration status (Expired/Not Expired).

In the list below, find the specific Access Key and click **View Details** in the **Action** column to enter the **Access Key Details** page to view **General** and **Settings.** 

<span id="d284e161"></span>
### Modify the Access Key Expiration Date

Switch to the **Settings** tab and click the edit icon in the **Expiration date** section to modify the validity period of the current Access Key.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you need to change the expiration date from a <strong>Custom date</strong> to <strong>Never expires</strong>, ensure that long\-term validity is required for the employees within the permission scope to reduce the risk of credential leakage.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9f7626612d744db89ceb2fa4a8dacf7~tplv-goo7wpa0wc-image.image) </span>

<span id="19a755f0"></span>
## Deleting an Access Key

On the **API** page, locate the specified Access Key, click **Delete** in the **Action** column.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After an Access key is deleted, it can no longer be used to call the SealSuite OpenAPI, and its historical call records cannot be viewed.</div>


<span id="625ce69c"></span>
# API call log auditing

To meet security and compliance audit requirements and help administrators troubleshoot API call anomalies, SealSuite provides structured API call logs.

<span id="466af5aa"></span>
## How to access


* **Method 1: Global query**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1775bfb1cbe4fddae2bebebaa81972b~tplv-goo7wpa0wc-image.image) </span>

   1. Log in to the Admin Console.

   2. In the left navigation pane, choose **Settings** \> **Integration** \> **API**.

   3. Click **Log Query** on the right to open the log query page, where you can view all API call records at the tenant level. You can also filter logs for a specific key using the **AccessKey** filter.

* **Method 2: Per\-AccessKey query**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e97b9e9ea00d4b979bd4b377034abfb3~tplv-goo7wpa0wc-image.image) </span>

   1. Log in to the Admin Console.

   2. In the left navigation pane, choose **Settings** \> **Integration** \> **API**.

   3. Locate the target AK in the **AccessKey list** and click **View Details** in the **Action** column to open the details page.

   4. Switch to the **Log Query** tab. The system displays the logs associated with that Access Key directly.


<span id="9ba71d69"></span>
## Understanding the logs

On the log query page, you can analyze API call activity through the following modules:


* **Filter area**: Filter by core fields such as **Call time**, **Source IP**, **Request ID**, **Request URL**, **Response status**, **Error code**, and **Error message**.

* **Call volume trend**: Visualizes call volume over time. By default, it displays call volume data for the last 24 hours.

* **Log detail list**: Displays matching call records in a tabular format.

   * **View details**: Click **Details** in the **Action** column to view the complete request parameters and response results for a specific log entry.

   * **Export logs**: Click **Export List** in the upper\-right corner of the list to export the current query results as a CSV or Excel file (maximum 10,000 entries per export).


<span id="26aea20d"></span>
## Log retention

The following describes how long API call logs are retained and available for query:


* **Console query period**: In the Admin Console, you can query API call logs from the **last 30 days**.

* **System retention period**: API call logs are retained in the SealSuite backend system for **180 days** by default.

> **Note**: To meet longer\-term audit and compliance requirements, we recommend configuring the **Log Export** feature to sync API call logs in real time to your own Syslog or Elasticsearch server for long\-term retention. For detailed instructions, see [Log Export and Auditing](https://docs.byteplus.com/docs/sealsuite/docs-zk9yxy9szc).
