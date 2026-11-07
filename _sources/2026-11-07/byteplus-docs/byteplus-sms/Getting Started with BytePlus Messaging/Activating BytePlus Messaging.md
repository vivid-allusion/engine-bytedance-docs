---
title: "Activating BytePlus Messaging"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-activating-byteplus-sms"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you neither use APIs nor have IAM sub\-account management needs, you can skip this activation process.</div>


Activate BytePlus Messaging to gain access to logging in to the BytePlus Messaging console and using Messaging APIs.

<span id="e26a17db"></span>
### Prerequisites


1. A valid BytePlus account . For more details, please see [Signing up for BytePlus accounts](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

2. Completed BytePlus billing configuration. For more details, please see [Setting up billing](https://docs.byteplus.com/byteplus-platform/docs/setting-up-billing).



---



<span id="f0b8e5c2"></span>
### Context

You can directly activate BytePlus Messaging for the main account by accessing [Messaging Console](https://console.byteplus.com/sms). If you manage multiple BytePlus products as an admin and need precise access control, use BytePlus Identity and Access Management (IAM) policies. In the IAM dashboard, you can choose to either use an existing account to manage BytePlus Messaging or create a new user account. For more details about IAM users, see [Product Overview](https://docs.byteplus.com/zh-CN/docs/CloudIdentity/ProductOverview).


---



<span id="6ddcf02d"></span>
### Procedure

**Access IAM Dashboard**


1. Log in to the [BytePlus Console](https://console.byteplus.com/).

2. In the top\-right corner, click the user icon \> [IAM](https://console.byteplus.com/iam/identitymanage/user). The IAM dashboard will appear.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e4ddf209bf54263b6cd26b6dfc8304e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information, please see <a href="https://docs.byteplus.com/docs/byteplus-sms/permissions-management">Permission management</a>.</div>


**Account Configuration Options**

Next, select from the following two options based on your needs:

**Option 1: Use an existing user account**


1. On the left navigation pane, click **User management** \> **User**.

2. Select the existing account that you want to add policies, click **Authorize**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd1103f437f47168f32bf1124ee481e~tplv-goo7wpa0wc-image.image) </span>


3. Assign one or more policies to the user. For BytePlus Messaging, use the search bar to find relevant policies **VolcSMSFullAccess** and **VolcSMSReadOnlyAccess** by typing "sms".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b7d17f2141541deb75f9dbfd58168b6~tplv-goo7wpa0wc-image.image) </span>


4. Review user settings and click **Submit**.

5. Go to the [Messaging Console](https://console.byteplus.com/sms) and click **Sign in as IAM user**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c88fc773d4824ddba17fa0405b4b67d6~tplv-goo7wpa0wc-image.image) </span>


6. Click **Activate Messaging Service** to enable the service.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4725fdbe385449bf940a7460a24a0215~tplv-goo7wpa0wc-image.image) </span>

**Option 2: Create a new user account**


1. On the left navigation pane, click **User management** \> **User**.

2. Click **Create New User**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3c5f04573c34f42b42ed6c4db14ae8d~tplv-goo7wpa0wc-image.image) </span>


3. Fill in the blank fields (refer to the table for field definitions) and click **Next** to continue configuration.



|**Field** |**Required** |**Description** |
|---|---|---|
|Username |Yes |Enter the name used for logging in. |
|Display name |No |Enter the name displayed on the console. |
|Email |No |Enter the user’s email address. |
|Description |No |Enter a description for this new account. |
|Console access |No |Enable Console Login and assign a password to the sub\-account.<br><br>The user can log in to the BytePlus Console via the assigned password. |
|Programmatic access |No |Enable to generate Access Keys for access through API requests.<br><br>An AccessKey, including an Access Key ID (AK) and a Secret Access Key (SK), will be generated and assigned to the user. Access keys are credentials for requesting BytePlus API, granting full account access to use all BytePlus APIs. |



4. Assign one or more policies to the user, then click **Next** to proceed to the review step. For BytePlus Messaging, use the search bar to find relevant policies **VolcSMSFullAccess** and **VolcSMSReadOnlyAccess** by typing "sms".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69bf8e236a3543afb9e4a78215e6b4ab~tplv-goo7wpa0wc-image.image) </span>


5. Review the user settings, then click **Next** — the new user account will be created successfully.

6. Go to the [Messaging console](https://console.byteplus.com/sms) and click **Sign in as IAM user**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a936be6c62f4fc4859a0c594a5437f1~tplv-goo7wpa0wc-image.image) </span>


7. Click **Activate Messaging Service**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4725fdbe385449bf940a7460a24a0215~tplv-goo7wpa0wc-image.image) </span>

<span id="aa04ea01"></span>
### Result

The platform will automatically navigate to the Messaging Console, allowing you to immediately access BytePlus Messaging.
