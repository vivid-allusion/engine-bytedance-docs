---
title: "Getting started with BytePlus Live API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getting-started-with-byteplus-live-api"
---

BytePlus Live APIs are HTTP\-based RESTful APIs that use signature algorithms for authentication. API request and response bodies are formatted in JSON. This topic walks you through the process of calling BytePlus Live APIs.


1. Understanding limits and quotas

2. Signing up for an account

3. Completing authentication

4. Making your first call


<span id="understanding-limits-and-quotas"></span>
## Understanding limits and quotas

Each API has a call frequency limit of 120 requests per minute per account ID (unless otherwise specified).

<span id="signing-up-for-an-account"></span>
## Signing up for an account

Before calling the BytePlus Live APIs, sign up for an account by following the instructions in [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

You can call APIs using your BytePlus account or an IAM user with specific permissions. For example, to call [UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) using an IAM user to add or update a host account, the IAM user must have the **Marketing toolkits** \> **Edit** permission. For more information on how to add an IAM user, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="completing-authentication"></span>
## Completing authentication

BytePlus Live API authentication signs API requests to verify your identity and prevent them from being maliciously intercepted in transit. For more information, see [API authentication](https://docs.byteplus.com/docs/byteplus-livesaas/docs-API-authentication).

For API authentication, use the Access Key ID and Secret Access Key of the account making the call (either your BytePlus account or an IAM user).

<span id="making-your-first-call"></span>
## Making your first call

BytePlus Live APIs require specific request structures. For more information, refer to [API HTTP request](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-http-request).
