---
title: "Configuring custom identity provider login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Configuring_custom_identity_provider_login"
---

Custom Providers allow you to configure any third\-party identity service that supports the standard OAuth 2.0 or OIDC protocols as a login provider for Supabase Auth. This topic explains how to create and manage custom Auth providers in the Supabase console.

## Background

Supabase Auth has built\-in support for common login providers such as WeChat, WeCom, CAS, DingTalk, and Feishu. If your business uses other identity services (such as Authing, Auth0, Firebase Auth), you can integrate any third\-party provider supporting OAuth 2.0 or OIDC protocols using the Custom Providers function, without waiting for official support.

Custom Providers support two protocol types:

* **OIDC**: OpenID Connect protocol, supporting automatic discovery mode, which automatically obtains OAuth endpoint configuration through the Issuer URL.

* **OAuth2**: OAuth 2.0 protocol, requiring manual entry of authorization endpoint, token endpoint, user info endpoint, and other configurations.

Related concepts: for detailed principles and best practices, refer to the official Supabase documentation on [Custom OAuth/OIDC Providers](https://supabase.com/docs/guides/auth/custom-oauth-providers).

## Prerequisites

* A workspace using the Supabase engine is created, and its status is Running. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace?lang=en).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console?lang=en).

* The application is created on the third\-party identity authentication platform, and the following information can be obtained:

   * Client ID and Client Secret

   * Issuer URL (OIDC automatic discovery mode) or OAuth endpoint address (manual configuration mode)

   * Required scopes (such as openid, email, profile)

* The Supabase callback URL is added to the callback address whitelist in the application configuration of the third\-party identity authentication platform.

## Managing custom Auth providers in Supabase console

### Feature overview

The Sign In / Providers page in Supabase console adds a Custom Providers management area below the Auth providers list. This area includes the following features:

* **Search box**: Search configured custom providers by name or identifier.

* **Provider type filter**: Filter by protocol type, options are OIDC and OAuth2.

* **Status filter**: Filter by enable status, options are Enabled and Disabled.

*  **+ New Provider button**: Create a new custom Auth provider.

### Creating a custom Auth provider

1. Logging in to the Supabase console.

2. Select **Authentication** in the left navigation bar.

3. Enter the **Sign In / Providers** page.

4. In the **Custom Providers** section, click  **+ New Provider**.

|**Configuration item** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Tip** |
|---|---|---|---|---|
|Provider Identifier<br><br> |identifier |string |Yes |Unique identifier of the provider. The prefix is fixed as `custom:`, and the input part only supports lowercase letters, numbers, and hyphens (\-). For example, entering `authing` results in the full identifier `custom:authing`. This identifier is used as the provider parameter during application calls. |
|Display Name |name |string |Yes |Provider display name, shown in the NAME column of the provider list. |
|Configuration Method |provider_type |string |Yes |Configuration method, options:<br><br><br>* **Auto\-discovery** (recommended): Automatically retrieve OAuth endpoint configurations via Issuer URL. When this mode is selected, the OAuth Endpoints section shows Issuer URL and Discovery URL fields, suitable for standard OIDC providers. Fill in the Issuer URL during configuration. The system automatically accesses the standard Discovery path to retrieve endpoint configurations upon saving.<br><br><br>> **tip**<br><br><br>> If the provider uses a non\-standard Discovery path, enter the full path in the Discovery URL field; if left empty, the standard Discovery path is used.<br><br><br><br>* **Manual configuration**: Manually enter OAuth endpoint information. When this mode is selected, the OAuth Endpoints section displays issuer URL, authorization URL, token URL, userinfo URL, and JWKS URI fields, suitable for non\-standard OAuth 2.0 providers or providers whose endpoints cannot be automatically obtained via Discovery. |
|Issuer URL |issuer |string |Yes |Base URL of the OAuth provider. Required when choosing auto\-discovery mode. The system automatically executes discovery and obtains endpoint configuration upon saving. |
|Discovery URL |discovery_url |string |No (Auto\-discovery mode) |OIDC Discovery endpoint address. Leave empty to use the standard path `{issuer}/.well-known/openid-configuration`. Fill in only if the provider uses a non\-standard discovery path. |
|Authorization URL |authorization_url |string |Yes (Manual configuration mode) |Displayed only when Manual configuration is selected. OAuth authorization endpoint address used to redirect to the third\-party identity authentication platform to complete user authorization. Example: `https://auth.company.com/oauth/authorize`. |
|Token URL |token_url |string |Yes (Manual configuration mode) |Displayed only when Manual configuration is selected. OAuth Token endpoint Address for exchanging the authorization code for an Access Token. Example: `https://auth.company.com/oauth/token`. |
|Userinfo URL |userinfo_url |string |Yes (manual configuration mode) |Only visible when Manual configuration is selected. User information endpoint address used to obtain third\-party account user information. Example: `https://auth.company.com/oauth/userinfo`. |
|JWKS URI |jwks_uri |string |Required (Manual configuration mode) |Displayed only when Manual configuration is selected. JWKS address used for ID token verification. Example: `https://auth.company.com/.well-known/jwks.json`. |
|Client ID |client_id |string |Yes |Client ID obtained when creating an application on the third\-party identity authentication platform. |
|Client Secret |client_secret |string |Yes |Client Secret obtained when creating an application on a third\-party identity authentication platform. |
|Scopes |scopes |string[] |No |OAuth authorization scope, multiple values separated by commas. Common values: openid, email, profile. For standard OAuth 2.0 services, it must include at least openid. |
|Allow users without email |email_optional |bool |No |Whether to allow login without the provider returning an Email address. Default is disabled. After enabling, users can register and log in even without an Email. |
|Callback URL |— |string |— |Read\-only field, automatically generated by the system. Formatted as: `https://{workspace-domain}/auth/v1/callback`. You need to add this address to the callback URL whitelist in the application configuration of the third\-party identity authentication platform. |

### Edit custom auth provider

1. On the **Sign In / Providers** page, find the target provider in the **Custom Providers** section.

2. Click the more actions menu (⋮) to the right of the target provider, select **Update**, and enter the **Update Custom Auth Provider** page.

3. Modify the provider configuration as needed. The edit page fields are the same as when creating, but the provider identifier and configuration method cannot be changed.

4. Click **Update provider** to save changes. To abandon changes, click **Cancel**.

### Disable custom Auth Provider

1. **Find the target Provider in the Custom Providers list.**

2. Click the more Actions menu (⋮) on the right of the target Provider, then select **Disable**.

3. After verifying the information in the confirmation dialog, click **Confirm disable**. To cancel the operation, click **Cancel**.

> **warning**

> After disabling, users cannot log in through this Provider. Existing sessions remain unaffected, but new login requests will fail until the Provider is re\-enabled. Before disabling, ensure users logged in via this Provider and applications relying on it have handled the situation accordingly.

### Delete custom Auth Provider

1. **Find the target Provider in the Custom Providers list.**

2. Click the more Actions menu (⋮) on the right of the target Provider and select **Delete**.

3. Confirm the information in the confirmation popup, then click **Confirm delete**. To cancel the operation, click **Cancel**.

> **warning**

> Delete operations are irreversible. To restore a deleted custom Auth Provider, recreate it. Before deleting, confirm the impact on users signed in with this Provider and ensure no applications use this Provider.

## Manage custom Auth Provider through Admin API

### Create custom Auth Provider

API: `POST /auth/v1/admin/custom-providers`

* oidc complete parameter example:

```Bash
curl -X POST "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "provider_type": "oidc",
    "identifier": "custom:company",
    "name": "Company SSO",
    "client_id": "your-client-id",
    "client_secret": "your-client-secret",
    "acceptable_client_ids": [],
    "scopes": ["openid", "email", "profile"],
    "pkce_enabled": true,
    "attribute_mapping": {"email": "email", "name": "name"},
    "custom_claims_allowlist": ["groups", "org_id"],
    "authorization_params": {"prompt": "login"},
    "enabled": true,
    "email_optional": false,
    "issuer": "https://sso.example.com",
    "discovery_url": "https://sso.example.com/.well-known/openid-configuration",
    "skip_nonce_check": false
  }'
```

* oauth 2.0 complete parameter example:

```Bash
curl -X POST "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "provider_type": "oauth2",
    "identifier": "custom:company",
    "name": "Company OAuth",
    "client_id": "your-client-id",
    "client_secret": "your-client-secret",
    "acceptable_client_ids": [],
    "scopes": ["email", "profile"],
    "pkce_enabled": true,
    "attribute_mapping": {"email": "email", "name": "name"},
    "custom_claims_allowlist": ["groups", "org_id"],
    "authorization_params": {"prompt": "login"},
    "enabled": true,
    "email_optional": false,
    "authorization_url": "https://sso.example.com/oauth/authorize",
    "token_url": "https://sso.example.com/oauth/token",
    "userinfo_url": "https://sso.example.com/oauth/userinfo",
    "jwks_uri": "https://sso.example.com/.well-known/jwks.json"
  }'
```

### query customized Auth Provider

API: `GET /auth/v1/admin/custom-providers/{identifier}`

```Bash
curl -X GET "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers/custom:company" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY"
```

### query customized Auth Provider list

API: `GET /auth/v1/admin/custom-providers`

`type` can be `oidc` or `oauth2`, if not passed, all will be queried.

```Bash
curl -X GET "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers?type=oidc" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY"
```

### modify customized Auth Provider

API: `PUT /auth/v1/admin/custom-providers/{identifier}`

* oidc example:

```Bash
curl -X PUT "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers/custom:company" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Company SSO",
    "client_id": "your-client-id",
    "client_secret": "new-client-secret",
    "acceptable_client_ids": [],
    "scopes": ["openid", "email", "profile"],
    "pkce_enabled": true,
    "attribute_mapping": {"email": "email", "name": "name"},
    "custom_claims_allowlist": ["groups", "org_id"],
    "authorization_params": {"prompt": "login"},
    "enabled": true,
    "email_optional": false,
    "issuer": "https://sso.example.com",
    "discovery_url": "https://sso.example.com/.well-known/openid-configuration",
    "skip_nonce_check": false
  }'
```

* OAuth 2.0 example:

```Bash
curl -X PUT "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers/custom:company" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Company OAuth",
    "client_id": "your-client-id",
    "client_secret": "new-client-secret",
    "acceptable_client_ids": [],
    "scopes": ["email", "profile"],
    "pkce_enabled": true,
    "attribute_mapping": {"email": "email", "name": "name"},
    "custom_claims_allowlist": ["groups", "org_id"],
    "authorization_params": {"prompt": "login"},
    "enabled": true,
    "email_optional": false,
    "authorization_url": "https://sso.example.com/oauth/authorize",
    "token_url": "https://sso.example.com/oauth/token",
    "userinfo_url": "https://sso.example.com/oauth/userinfo",
    "jwks_uri": "https://sso.example.com/.well-known/jwks.json"
  }'
```

### Delete custom Auth Provider

API: `DELETE /auth/v1/admin/custom-providers/{identifier}`

```Bash
curl -X DELETE "$SUPABASE_BASE_URL/auth/v1/admin/custom-providers/custom:company" \
  -H "apikey: $SERVICE_ROLE_KEY" \
  -H "Authorization: Bearer $SERVICE_ROLE_KEY"
```

## Configure callback address on third\-party platform

When creating a custom Auth Provider, the system generates a callback URL (formatted as `https://{workspace-domain}/auth/v1/callback`). You need to configure this address in the callback URL whitelist of the third\-party identity authentication platform.
