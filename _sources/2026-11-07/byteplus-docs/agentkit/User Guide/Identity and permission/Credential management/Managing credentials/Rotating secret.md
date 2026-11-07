---
title: "Rotating secret"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/rotating-secret"
---

Secret rotation is used to update the API Key or OAuth client secret managed by AgentKit. You can perform secret rotation when the existing secret is about to expire, is suspected to have been leaked, or needs to be updated regularly according to security policies. After rotation, AgentKit immediately replaces the old value with the new value. The old value will not be retained and cannot be restored. The credential’s existing agent associations are not affected. Subsequent outbound calls will use the new client secret.

## Recommended scenarios

* **Update secrets regularly**

   We recommend rotating client secrets periodically to shorten the usage duration of long\-lived secrets.

* **Mitigate suspected compromise risks**

   If the existing client secret may have been leaked, mistakenly committed to a code repository, or appeared in logs or configuration files, generate a new secret and complete rotation as soon as possible.

* **Sync secret changes from third\-party platforms**

   After a third\-party service provider generates a new client secret, you need to synchronously update the secret managed in AgentKit to ensure that the agent can access the target service normally.

* **Adjust secret permissions or validity period**

   When the permission scope, applicable environment, or validity period of the existing secret no longer meets business requirements, you can create a client secret that meets the new requirements and replace the existing one through rotation.

## Limits

Support for secret rotation varies by credential type:

|Credential type |Whether secret replacement is supported |Description |
|---|---|---|
|**API Key** |Supported |After secret rotation is complete, the new client secret will immediately overwrite the old value. The existing agent associations for this credential remain unchanged. |
|**OAuth connection** |Partially supported |OAuth connections with provider types **Feishu**, **Coze**, **Github**, and **Custom** support secret rotation. After the rotation takes effect, subsequent OAuth authorization flows and token retrieval requests will use the new client secret.<br><br>> **tip**<br><br><br>> OAuth connections with provider type **User pool** do not support secret rotation. Their client secrets are managed by the user pool client. Go to the corresponding user pool client to handle them. For details, see [Edit client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en#3y5H0J09).<br> |
|**BytePlus cloud role** |Not supported |BytePlus cloud role credentials do not rely on an API Key or OAuth client secret and do not have a secret carrier, so secret rotation is not supported. |

## Prerequisites

* **Obtain a valid new secret**

   Generate a new value on the corresponding third\-party platform based on the credential type:

   * **API Key**: **An available API Key has been obtained from the target service provider**, and it is confirmed that the secret has the permissions required for the agent to call the target service. We recommend confirming the secret’s applicable environments, validity period, call quota, access scope, and whether restrictions such as an IP allowlist exist, to avoid call failures due to insufficient permissions or environment mismatch after creation.

   * **OAuth connection**: Generate a new Client Secret for the current OAuth application on the identity provider’s developer platform or OAuth application management page. Creation methods and credential names may vary across providers. Refer to the table below:

      |**Provider type** |**Preparations** |**Related documents** |
      |---|---|---|
      |GitHub |Create an OAuth App, configure the Homepage URL and Authorization callback URL, and obtain the Client Secret. |[Creating an OAuth app](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/creating-an-oauth-app) |
      |Feishu |Create or open a Feishu application, and obtain the App Secret in "Basic Info \> Credentials & Basic Info". The App Secret corresponds to the client secret. |[How to obtain the App ID and App Secret of an application](https://open.larkoffice.com/document/server-docs/im-v1/faq#534e3009) |
      |Coze |Create an OAuth application and obtain the Client Secret.<br><br>> When creating the OAuth application, enter the callback URL actually used by the current AgentKit OAuth flow. |[Create an OAuth application and obtain client credentials](https://docs.coze.cn/developer_guides_oauth_code#3fba3e8e) |
      |Custom |Go to the developer platform of the target identity provider to create an OAuth client, and configure the callback URL, permission scope, and other OAuth parameters according to the official documentation. |Refer to the official documentation of the target identity provider. |

* **Confirm permission, quota, and applicable environments**

   Confirm that the client secret has the API permissions and call quota required for the agent to call the target service, and that it matches the current business environment, such as the test environment or production environment, to avoid call failures due to insufficient permissions, quota limits, or environment mismatch.

* **Check access restrictions**

   Confirm whether the target service is configured with an IP allowlist, region restrictions, source domains, or other authentication restrictions. If source IP restrictions exist, first confirm the egress IP actually used by AgentKit to initiate outbound requests, and add it to the allowlist of the target service. For network configuration details, see [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).

   > After replacement, we recommend initiating a low\-risk [test call](https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts?_vtm_=a106466.b106468.0_0.0_0.0.14095_7613594367911118351&lang=en) through the target agent to confirm that the network connection is normal and that the request is not blocked by allowlist settings, region restriction, or other security policies.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity and Permission  **\>**  Credential management".

3. In the "Actions" column of the target credential, click the "Rotate secret" button.

4. Confirm that the name of the credential to be rotated is correct, and paste the new secret obtained from the third\-party service provider into the “New API Key” input box.

5. After confirming that the new secret is correct, click “Confirm rotation” to complete the operation.

## Subsequent steps

The credential rotation operation within AgentKit only updates the secret value stored on this platform. It does not automatically revoke the old secret on the third\-party service platform. After verifying that calls with the new secret work normally and updating the platform\-managed value, you can perform the following operations as needed:

* **API Key type credentials**

   The platform does not automatically disable or delete the original API Key in the third\-party service. You can go to the third\-party service console to disable or delete the secret, and verify that the old secret can no longer be used.

* **OAuth connection type credentials**

   The platform does not guarantee that access tokens, refresh tokens, or user permissions already issued by the identity provider become invalid simultaneously. To immediately terminate access, revoke tokens and cancel authorization on the identity provider side. If necessary, disable or delete the corresponding OAuth client.
