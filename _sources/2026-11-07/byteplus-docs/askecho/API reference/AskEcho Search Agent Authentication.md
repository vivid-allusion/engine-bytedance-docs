---
title: "AskEcho Search Agent Authentication"
product: "Byteplus AskEcho"
product_code: "askecho"
source: "https://docs.byteplus.com/en/docs/askecho/AskEcho_Search_Agent_Authentication"
---

<span id="yceJ8p7G"></span>
# Authentication

Two authentication methods are supported: **API Key access** and **Byteplus IAM access**. **Each method uses a different URL.** 

&nbsp;

<span id="v60JQrzl"></span>
## API Key Access (Recommended)


1. **Obtain an API Key**

* Log in to the console and navigate to **Manage \> API Keys**.

* Click **Create Key**.

* Enter an API Key name in the dialog box and click **Create Key**.

> Note: Keep your API Key secure. It is strongly recommended not to hardcode the key directly in your application code.


2. **Signature Construction**


The API Key authentication method requires adding an Authorization header in the HTTP request as follows:

```JSON
Authorization: Bearer <API_KEY>
```


**Notes**: If you are using API Key access, the API timeout is **30 seconds**.

&nbsp;

&nbsp;

<span id="5UzYojub"></span>
## Byteplus IAM Access

This access method is based on AK/SK authentication from BytePlus IAM, with a unified `ServiceName = volc_torchlight_api`.


1. The logic for interface signature verification and request public parameters follows the unified specifications provided on the official BytePlus website. For details, see: [About the request signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-signature)

2. After account permissions are enabled, you can obtain the AccessKey for signature verification. For details, see: [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey)

3. Signature process demo: [Example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-example)


&nbsp;

**Notes:** 


* If you are using the main account  **(strongly not recommended)**  for access, you can skip this step and ignore this prerequisite.

* If it is a sub\-account for access, you must log in to the console and enable interface access permissions first; otherwise, error `100013: AccessDenied` will occur.


&nbsp;

**Steps to enable interface access permissions:** 


1. Log in to the console using the main account on the Byteplus console.

2. Click on your user avatar to enter the "**IAM**"menu, and click a sub\-account to access the permission management page in the ["User" menu](https://console.byteplus.com/iam/identitymanage/user).


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0e6e0be44ebc790f89fc1abaf03c6167.png" width="2938px" /></div>


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_177a786c8424ead9d0e3a559698e4c38.png" width="2938px" /></div>



3. Switch to the "**Policy**" tab, click the "**Authorize**" button, enter **`TorchlightApiFullAccess`** in the search bar, and select it for confirmation.

4. If multiple sub\-accounts are accessing the platform, you must configure the corresponding permissions for each sub\-account.


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5f4b8accdff8565253e7d62016c4235d.png" width="2938px" /></div>


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5b106453e9e956376e28f87a141fe460.png" width="2938px" /></div>



5. When using this access method, the request body size must not exceed **8 MB**, and the API timeout is **30 seconds**.
