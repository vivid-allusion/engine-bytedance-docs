---
title: "Manage API Key"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Manage_API_Key"
---

The data\-plane service APIs of **BytePlus Viking AI Search** support API key authentication. These APIs include application APIs for search, chat, and recommendation, as well as dataset APIs for data upload, deletion, and query operations.

<span id="9d1de12c"></span>
# Overview

BytePlus AI Search supports API key authentication for data\-plane service APIs. Data\-plane APIs include dataset APIs for uploading, deleting, and querying data, as well as application APIs for search, chat, and recommendation.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">BytePlus Universal API Keys</div>


<div data-tips="true" data-tips-type="default">Starting <strong>July 14, 2026</strong>, BytePlus AI Search will use <strong>BytePlus Universal API Keys</strong> for new API key authentication. During the migration and compatibility period, existing legacy AI Search API keys will continue to work. After you complete the migration, we recommend deleting legacy keys to reduce security risks.</div>


&nbsp;

The new API key experience supports two types of API keys:


* **BytePlus Universal API Key**: Recommended for new users and new workloads. This type of API key is created and managed through BytePlus unified API key management and can be used for the latest data import and API calling scenarios.

* **Legacy AI Search API Key**: Provided for compatibility with existing workloads. If your business has already integrated with legacy AI Search API keys, you can continue using them during the compatibility period. However, **we recommend migrating to BytePlus Universal API Keys as soon as possible. ** 


&nbsp;

API keys grant access to service APIs. Do not store API keys in frontend code, mobile clients, public repositories, logs, or support ticket screenshots. We recommend storing and using API keys only in secure server\-side environments, such as environment variables or a secrets management service.

<span id="979cbfe9"></span>
## API Key Types


|**Type** |**Recommended for** |**Description** |
|---|---|---|
|BytePlus General API Key |New users, new workloads, and new integrations |Recommended<br><br>Suitable for the latest data import and API calling scenarios. |
|Legacy AI Search API Key |Existing workloads that already use the legacy authentication method |Supported for compatibility with existing calls. <br><br>We recommend evaluating and migrating to BytePlus universal API Keys. |


<span id="d1fa98c4"></span>
# Create an API Key

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">BytePlus Universal API Keys</div>


<div data-tips="true" data-tips-type="default">Starting <strong>July 14, 2026</strong>, BytePlus AI Search will use <strong>BytePlus Universal API Keys</strong> for new API key authentication. During the migration and compatibility period, existing legacy AI Search API keys will continue to work. After you complete the migration, we recommend deleting legacy keys to reduce security risks.</div>



&nbsp;

1. Go to the **BytePlus AI Search** console.

2. In the left navigation pane, choose **API Key Management**.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ebbb637d15a44e899ea024aa6f061eb0) </span>


3. Click **Create BytePlus Universal API Key**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e75a2628ce948339a64e82ab0f94e05" width="500px" /></div>



4. Enter an API key name, and click **OK**.

5. Complete identity verification.

6. After verification, the newly created API key is displayed.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/89a73a079abe417a824fc42e5c4b10d5" width="500px" /></div>



&nbsp;

7. Save the API key securely after it is created. For security reasons, the full key value is usually displayed only once.

8. Rotate and delete keys regularly. After closing the dialog, go to the BytePlus IAM service to view the full key (https://console.byteplus.com/iam/keymanage).


&nbsp;

<span id="185096f5"></span>
# BytePlus Universal API Keys

<span id="80af8a31"></span>
## View Universal API Keys

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">You can also view BytePlus Universal API Keys directly in the BytePlus IAM service: https://console.byteplus.com/iam/keymanage</div>


&nbsp;

To view BytePlus Universal API Keys from the BytePlus AI Search console:


1. Go to the **BytePlus AI Search** console.

2. In the left navigation pane, choose **API Key Management**.

3. The platform displays all legacy AI Search API keys created under the current account.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ebbb637d15a44e899ea024aa6f061eb0) </span>


4. To view BytePlus General API Keys, click **View BytePlus Universal API Keys**.

5. You will be redirected to the BytePlus IAM page.


&nbsp;

<span id="a6aba658"></span>
## Disable BytePlus Universal API Key

To disable a BytePlus General API Key, go to the BytePlus IAM key management page: https://console.byteplus.com/iam/keymanage

&nbsp;

<span id="8c0b7d78"></span>
## Delete BytePlus Universal API Key

To delete a BytePlus General API Key, go to the BytePlus IAM key management page: https://console.byteplus.com/iam/keymanage

&nbsp;

<span id="58422923"></span>
# Legacy AI Search API Keys

<span id="938c7cdf"></span>
## Migrate Legacy AI Search API Keys

If your business still uses legacy AI Search API keys, you can view existing keys on the **API Key Management** page in the BytePlus AI Search console and use them as needed.

We strongly recommend migrating to **BytePlus Universal API Keys** as soon as possible.

<span id="0e83b075"></span>
## Migrate from Legacy AI Search API Keys to BytePlus Universal API Keys


1. Create a new BytePlus General API Key.

2. In your test environment, replace the API key in the request header with the new BytePlus Universal API Key.

3. Verify core APIs, including data upload, data deletion, data query, search, chat, and recommendation.

4. Confirm that application logs, monitoring, and alerts are working as expected.

5. Gradually switch production traffic to the new API key.

6. After confirming that there are no issues, stop using the legacy AI Search API key and delete it.


&nbsp;

<span id="14c01836"></span>
## View Legacy AI Search API Keys


1. Go to the **BytePlus AI Search** console.

2. In the left navigation pane, choose **API Keys**.

3. The platform displays all legacy AI Search API keys created under the current account.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ae7cfc3cf6e646aba9cedf3d86b0d3b1) </span>


&nbsp;

4. To view BytePlus General API Keys, click **View BytePlus ** **Univesal** ** API Keys** and go to the BytePlus IAM page.


<span id="60b16195"></span>
## Disable an API Key

An API key can be in one of the following states:


* **Active**: The API key can be used for API authentication. A newly created API key is active by default.

* **Disabled**: The API key cannot be used for authentication. If you use a disabled API key for authentication, the API returns HTTP status code `401`, indicating authentication failure.


If you detect abnormal traffic from a service that uses BytePlus AI Search, or if you suspect that an API key has been leaked, you can temporarily disable the API key in the console. After confirming that there is no risk, you can enable it again.

<span id="e99615cd"></span>
## Delete an API Key

If a service no longer uses a specific API key, you can delete the key.

Before deleting an API key, the console asks you to confirm the operation. Make sure that no online service is still using the key before deletion. Deleting an API key that is still used by production services may cause service failures.

<span id="8da15ec0"></span>
# Use an API Key in API Calls

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For more details, refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/API_Authentication">API Authentication</a></div>


When your backend service calls BytePlus Viking AI Search APIs, pass the API key in the request header.

```HTTP
Authorization: Bearer <API_KEY>
```


&nbsp;

If the API key is invalid, disabled, deleted, or does not have the required permissions, the API returns an authentication error. Check whether the API key is correct and still valid, and make sure you are using the correct service endpoint.

<span id="8f7c4fad"></span>
# FAQ

<span id="b8ff4caa"></span>
## Do I have to migrate to BytePlus Universal API Keys?

Existing workloads can continue to use legacy AI Search API keys during the compatibility period. For new workloads and new integrations, we recommend using BytePlus Universal API Keys so that you can use the unified API key management capability.

<span id="8f0cf591"></span>
## Why are there two types of API keys?

The two API key types are provided to support compatibility for existing workloads. We strongly recommend migrating to BytePlus Universal API Keys.

<span id="6ccd611f"></span>
## Will a BytePlus Universal API Key be saved after I enter it?

Follow the actual notice displayed in the console. In general, an API key entered in the data import workflow is intended only for the current sample request or workflow. Regardless of whether the page stores the key, do not expose the full API key in shared screenshots, browser extensions, or logs.
