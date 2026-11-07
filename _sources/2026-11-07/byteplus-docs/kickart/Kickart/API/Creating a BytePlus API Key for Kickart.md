---
title: "Creating a BytePlus API Key for Kickart"
product: "BytePlus Kickart"
product_code: "kickart"
source: "https://docs.byteplus.com/en/docs/kickart/byteplus_API_key"
---

&nbsp;

<span id="Us36478s"></span>
## 1. Scope

This document guides BytePlus customers through creating an API Key and using it with Kickart. The operation entry point is **Access Control → API Access Keys** in the BytePlus Console.

The BytePlus Console provides two creation methods: direct creation under the primary account, or creation under an IAM user. For production environments, we recommend using a dedicated IAM user and granting minimum permissions based on actual business requirements.

<span id="BGKb5cKF"></span>
## 2. Choosing a Creation Method


|**Scenario** |**Creation Location** |**Permission Characteristics** |**Recommendation** |
|---|---|---|---|
|Direct creation under primary account |API Access Keys page |Service\-level permission restrictions available; simpler configuration |Suitable for testing or temporary verification |
|Creation under IAM sub\-account |Under a dedicated IAM user |Permissions and usage boundaries controlled via IAM policies |**Recommended for production environments** |


**Selection Principle**: Use a dedicated IAM user and a dedicated API Key for each application, environment, or use case. This facilitates permission consolidation, credential rotation, deactivation, and auditing, and reduces the blast radius if a single key is compromised.

<span id="FmpD2fQ1"></span>
## 3. Prerequisites


* Confirm that the current account has activated the Kickart and has permission to create API Keys.

* Confirm that the target product supports API Key authentication. If the product documentation requires using an Access Key, do not mix the two credential types.

* Prepare a clear key name. We recommend including the application, environment, and purpose — for example, appname\-prod\-server. Do not include account numbers, phone numbers, email addresses, or other personal information in the name.

* Define the scope of services that need to be accessed. In production environments, select only the products or services that the business actually requires.


<span id="EnJF5B1C"></span>
## 4. Direct Creation Under the Primary Account

This method creates an API Key directly under the current account, with basic service\-level permission restrictions available.


1. Log in to the [BytePlus Console](https://console.byteplus.com/) and navigate to **Access Control**.

2. In the left navigation pane, select **API Access Keys** to enter the key list. In the API Key section, click **Create API Key**.

3. Under **Select Creation Method**, choose **Direct Creation**, then click **OK**.

4. Enter the key name. After enabling **Permission Restriction**, select only the services that the current AI application needs to access  **(for Kickart, select Kickart)** , verify the configuration, and submit to create.

5. **After successful creation, store the API Key ID and API Key Secret in a server\-side key management system or controlled environment variables. Do not store them in business code, configuration file templates, or client\-side code.Completion Check**: The key status is "Enabled"; the permission scope includes only the target service; the calling program can complete a minimal authentication test.


<span id="xKS8CF5k"></span>
## 5. Creation Under an IAM Sub\-Account

This method first creates a dedicated IAM user with minimum permissions, then creates an API Key under that user. It is suitable for production environments, multi\-application isolation, and scenarios requiring independent auditing.

<span id="lVghhhDx"></span>
### 5.1 Create a New IAM User


1. Log in to the BytePlus Console and navigate to **Access Control → User Management → Users**.

2. Click **Create User**, and enter the username, display name, and necessary remarks. We recommend one user per application or environment.

3. If the user is only used for programmatic calls and does not require human console login, do not enable unnecessary console access capabilities.

4. Complete the creation and return to the user list.


<span id="gZZYlVPL"></span>
### 5.2 Grant Minimum Permissions


1. In the user list, locate the target IAM user and click **Add Permissions**.

2. Select the IAM policy 「KickartFullAccess」, granting only the permissions needed to call the target APIs. 

3. Confirm the policy scope, resource scope, and effective subjects, then complete the authorization.


**Completion Check**: The IAM user has only the permissions required by the target product; no administrative permissions unrelated to the current application are included.

<span id="u7qgHx9Z"></span>
### 5.3 Create an API Key Under the IAM User


1. Navigate to **Access Control → API Access Keys**, and in the API Key section, click **Create API Key**.

2. Select **Create under IAM User**. The system will guide you to IAM user management.

3. Enter the target IAM user details, locate the API Key management entry, and create a key.

4. Enter the key name and submit to create.

5. **After successful creation, store the API Key ID and API Key Secret in a server\-side key management system or controlled environment variables. Do not store them in business code, configuration file templates, or client\-side code.Completion Check**: The key belongs to the expected IAM user; both the IAM policy and the API Key service scope comply with the minimum permission principle; the call test is successful.


<span id="WdAgiawu"></span>
## 6. Integrating with the Kickart


1. Review the API documentation of Kickart to confirm the API Key request header name or SDK configuration item.

2. On the server side, read the credentials from the key management system or environment variables, and initiate requests according to the product documentation.

3. Use a low\-risk test request to verify authentication. In logs, record only the request ID, timestamp, API endpoint, and error code — do not log the full API Key.

4. After successful verification, deploy to the production environment, and maintain call auditing and anomaly alerting.


**Do Not Mix Credential Types**: API Key and Access Key are different credentials.

Follow Kickart documentation to confirm whether to use API Key ID / API Key Secret or Access Key ID / Secret Access Key.

<span id="SNP8xaIi"></span>
## 7. Data Security Requirements


* Store keys only in server\-side key management systems, controlled environment variables, or equivalent\-security facilities.

* Do not write keys into Git repositories, container images, installation packages, web frontends, mobile apps, notebooks, logs, or monitoring telemetry.

* Do not display full keys in screenshots, demo videos, group chats, emails, or support tickets. When troubleshooting, provide only redacted fragments and request IDs.

* Use different IAM users and API Keys for development, testing, staging, and production environments.

* Rotate keys regularly. During rotation, deploy and verify the new key first, then deactivate the old key to avoid service disruption.

* Promptly disable or delete keys that are no longer needed when personnel leave, applications are decommissioned, or permission scopes change.

* If a suspected leak is discovered, immediately disable or rotate the key, review call records, and assess whether IAM permissions need to be adjusted.


<span id="f7psiRDX"></span>
## 8. FAQ

<span id="6UfZ75ub"></span>
### 8.1 Why does authentication still fail after creation?

First confirm that the target product supports API Key, then check the request header or SDK parameters, key status, service permission scope, and IAM policy. Do not mix the fields of API Key and Access Key.

<span id="yzOzHnjW"></span>
### 8.2 Should I use the primary account or an IAM sub\-account?

For temporary testing, direct creation is acceptable. For production environments, multi\-application, or multi\-person collaboration scenarios, use an IAM sub\-account and assign a dedicated identity with minimum permissions to each application or environment.

<span id="X49kglP6"></span>
### 8.3 Can I send the key to technical support for troubleshooting?

Do not send the full key. You can provide the request ID, call timestamp, API name, error code, and the redacted credential identifier. If the credential needs to be replaced, rotate or recreate it in the console.

<span id="hcWbJFjf"></span>
### 8.4 What should I do if a key is suspected to be leaked?

Immediately disable or rotate the affected API Key, stop further dissemination, and review recent call records and permission scopes. After confirming the new key is active, delete the old key, and investigate the source of the leak in code repositories, logs, and communication records.
