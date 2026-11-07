---
title: "Create credentials"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Create_credentials"
---

When your agent needs to act as a client to call external or downstream APIs, it also requires identity credentials. The identity credential hosting module is designed for this purpose. It allows you to securely store these outbound credentials in the BytePlus Agent Identity, enabling agents to retrieve and use them as needed at runtime, thereby avoiding the risk of hardcoding sensitive information in code or configuration.

Currently, two types of credentials are supported for hosting: **API Key** and **OAuth Client**.

<span id="3ec65547"></span>
## **Relationship with the key management service**

To ensure security, the sensitive credentials you host here (such as API Key and Client Secret) are not stored in plaintext in the BytePlus Agent Identity. The system securely stores these credentials in the key management service (Secret Manager), while the BytePlus Agent Identity only retains their references. To follow best security practices, it is recommended to rotate credentials regularly in the key management service (Secret Manager).

<span id="9aa384a1"></span>
## Create an API Key credential

Applicable to external services that use fixed keys for authentication.


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation bar, select **Credential Management**.

3. Click **Create a Credential** and select **Create an API Key**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a216a9e6db2842ae9eb947fdde1b4eee) </span>

4. Configure the relevant parameters.

   
   |Configuration items |Description |
   |---|---|
   |**API key name** |Custom name for the API key, used to identify different API keys. |
   |**API key value** |Enter the actual key value you obtained from the third\-party service. |
   |**Parameter location** |Specify where this key should be placed when making an API request. **It is recommended to use ** **`Header`**, as it is more secure than placing it in the `Query`.<br><br><br>* **Header**: The key will be sent as part of the HTTP request header.<br><br>* **Query**: The key will be sent as a query parameter in the URL (`https://api.example.com?key=...`), which can be easily exposed if the URL is leaked. |
   |**Parameter name** |Specify the parameter name that carries the API key; it must exactly match the requirements of the external service. For example, if you select `Header`, the parameter name might be `X-Api-Key` or `Authorization`. |
   

5. Click **OK**.

   The API Key will be encrypted and stored in the key management service (Secret Manager).


<span id="3da109cf"></span>
## Create an OAuth Client credential

Applicable to downstream services that require authentication through the OAuth 2.0 flow.


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation bar, select **Credential Management**.

3. Click **Create a Credential** and select **Create an OAuth Client**.

4. Configure the relevant parameters.

   
   |Configuration items |Description |
   |---|---|
   |**Provider name** |Custom name, such as `downstream-service-oauth`. |
   |**Provider type** |Currently, both preset provider types and custom types are supported. Preset types include: Feishu, Coze, and GitHub. |
   |**Client ID / Client Secret** |Enter the client credentials you obtained when registering the agent with the downstream OAuth service. |
   |**Configuration type** |Required when the provider type is set to custom.<br><br><br>* Automatic discovery: You need to configure the OIDC configuration root URL (such as https://idp.example.com/.well\-known/openid\-configuration), and the system will automatically fetch endpoint information.<br><br>* Manual configuration: You need to manually enter the authorization server metadata, including issuer root URL, authorization endpoint, token endpoint, and response type. |
   |**Scope** |The scope of permissions requested by the client:<br><br><br>* Standard scopes: openid (required for OIDC, added by default), email, profile.<br><br>* Custom scopes: read:data, write:config (must be supported by the IdP). |
   |**Custom parameters** |Add custom parameters, in addition to the standard ones, to the authorization or token request (such as aud=https://api.example.com, tenant=123) to meet special IdP requirements. |
   |**OAuth2 flow** |This is a key configuration that determines how authorization occurs:<br><br><br>* **User delegation (USER_FEDERATION)** : Requires user involvement in authorization. On the first call, the user will be redirected to the downstream service's authorization page to log in and give consent. After successful authorization, the BytePlus Agent Identity securely manages the obtained Refresh Token, which is used to silently refresh the Access Token on behalf of the user in subsequent operations, enabling "one\-time authorization, long\-term access."<br><br>* **Machine\-to\-machine (M2M)** : No user intervention required. The agent directly uses the Client ID/Secret to obtain an Access Token from downstream services, suitable for backend calls between services. |
   |**Force reauthorization** |If selected, each time an authorization request is initiated, even if the user already has a valid session, they will be required to log in and authorize again. |
   |**Maximum expiration time** |* You can set the maximum validity period for the obtained token to enforce reauthorization and enhance security.<br><br>* Must be less than the IdP limit; after expiration, a new token must be obtained. |
   |**Workload Pool** |The unique Workload Pool name within the account is used to isolate OAuth clients in different environments (such as prod\-pool). If not specified, the default is "default." |
   


<span id="09eb7f27"></span>
## View, edit, and delete


* You can view a summary of created credentials in the list at any time. Click the identity credential name to view detailed information.

* Click **Edit** to update credential information (such as the value of the API Key, the secret of the OAuth client, and more). After the update, the system will automatically create a new version of the key in the backend key management service.

* Click **Delete** to permanently remove this managed credential. Agents using this credential will not be able to access the corresponding external service.
