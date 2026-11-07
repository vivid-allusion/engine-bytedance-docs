---
title: "Access Key & API Key"
product: "BytePlus IAM"
product_code: "IAM"
source: "https://docs.byteplus.com/en/docs/IAM/about-access-keys"
---

<span id="api-credentials"></span>
## API Credentials

BytePlus IAM provides two types of API credentials:


* **Access Key:**  BytePlus's standard cloud API credential. Requests made with an Access Key must be signed before they are sent. This credential type provides stronger security and is generally recommended.

* **API Key:**  Some BytePlus products also support API Key authentication for data\-plane APIs. For the list of supported products, see the appendix at the end of this document. API Keys are easier to use because they can be passed as Bearer tokens, but they are less secure than signed Access Key requests. We recommend using API Keys only when exploring or testing AI products. For production environments, use Access Keys or STS temporary credentials.


<span id="operation-guide"></span>
## Operation Guide

<span id="obtain-a-main-account-key"></span>
### Obtain a Main Account Key

When you are logged in with a main account, you can go to the [API Access Key](https://console.byteplus.com/iam/keymanage/) page to create and manage API credentials, including Access Keys and API Keys.

You can also access this page from the **IAM** entry in the avatar drop\-down menu in the top navigation bar.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260709084324-8254966767.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Main account credentials are suitable for individual developers who are exploring or testing products. If you need to develop production\-grade applications or use credentials in enterprise scenarios, avoid using main account credentials.</div>


<span id="obtain-an-iam-user-key-recommended"></span>
### Obtain an IAM User Key (Recommended)

There are two ways to obtain credentials for an IAM user.

**Method 1: Create a key for the currently logged\-in IAM user.** 

If you are logged in as an IAM user, go to the [API Access Key](https://console.byteplus.com/iam/keymanage/) page to create and manage Access Keys or API Keys that belong to the current IAM user.

You can also access this page from the **IAM** entry in the avatar drop\-down menu in the top navigation bar.

**Method 2: Create an IAM user and then create a key.** 


1. Go to the [IAM User Management](https://console.byteplus.com/iam/identitymanage/user) page.

2. Click **New User** to create an IAM user, or open the details page of an existing IAM user. Then create a key on the **Key** tab.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260709084531-269409857065.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In enterprise scenarios, we do not recommend creating keys directly for the currently logged\-in IAM user. Instead, create dedicated IAM users and issue credentials based on specific use cases or applications.</div>


<div data-tips="true" data-tips-type="tip">This reduces the risk of credential exposure if the logged\-in user is deleted, for example due to employee departure, or if the user's password is compromised.</div>


<div data-tips="true" data-tips-type="tip">If you are an enterprise IAM administrator, we recommend creating dedicated users and credentials for business applications, rather than granting key creation permissions directly to business personnel.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only main accounts and IAM users can have long\-lived API credentials. IAM roles cannot have long\-lived API credentials.</div>


<span id="grant-permissions-to-api-credentials"></span>
### Grant Permissions to API Credentials

If you need to grant additional permissions to an existing Access Key or API Key, use one of the following methods.

**Main account key scenario:** 

A main account Access Key has full permissions by default, so no additional authorization is required.

A main account API Key supports permission restrictions. If permission restrictions have already been configured and you need to add product permissions, click **Modify Permissions** in the operation column of the corresponding key.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260709084613-1578230250529.png) </span>

**IAM user key scenario:** 

The permissions of an IAM user key are the same as the permissions of the IAM user that owns the key. To adjust the permissions of the key, adjust the permissions of the corresponding IAM user.


1. Go to the [IAM User Management](https://console.byteplus.com/iam/identitymanage/user) page and find the IAM user that owns the key. You can search by key ID.

2. Open the user details page and add permissions on the **Policy** tab.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260709084748-941624437575.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260709084815-1505836147704.png) </span>

<span id="disable-enable-or-delete-api-credentials"></span>
### Disable, Enable, or Delete API Credentials

You can disable an API credential from the key list, usually when the credential is leaked or needs to be rotated.

After a credential is disabled, requests using the credential become invalid. You can enable the credential again if needed.

After a credential is deleted, it becomes permanently invalid and cannot be recovered. Proceed with caution.

<span id="appendix-products-that-support-api-key-authentication"></span>
### Appendix: Products That Support API Key Authentication

Some BytePlus products, mainly AI products, support simplified data\-plane API calls through API Key authentication.

The currently supported products are listed below.


|Product |Service Code |Release Date |
|---|---|---|
|Viking AI Search |aisearch |July 15, 2026 |


*More products will be supported in the future. Stay tuned.*
