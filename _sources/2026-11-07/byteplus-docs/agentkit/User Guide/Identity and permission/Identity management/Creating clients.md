---
title: "Creating clients"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-client-side"
---

A client represents an application that needs to integrate with the AgentKit identity and permission management module for user authentication. Whether it is a web application, a single\-page application (SPA), a mobile app, or a machine\-to\-machine (M2M) service, you need to create a client for it in order to obtain the Client ID and Client Secret used to initiate the authentication flow.

## Core values

* **Unified identity integration**: Centrally manage application authentication configurations and avoid redeveloping login logic.

* **Security boundary control**: Use callback URL allowlists, token validity periods, and other restrictions to prevent malicious requests from forging identities.

* **Multi\-scenario adaptation**: Support web applications, SPAs, mobile apps, M2M services, and other types to meet different authentication requirements.

## Prerequisites

A user pool has been created. For related operations, see [Creating user pools](https://docs.byteplus.com/en/docs/agentkit/create-user-pool).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management". On the page that appears, click the name of the target user pool.

3. On the user pool details page, switch to the "Client" tab and click "Create client".

4. Specify the parameters of the client.

   |Parameter |Description |
   |---|---|
   |Client name |Specify a custom client name. |
   |Client type |Select a client type based on your application type. Valid values:<br><br><br>* **Web application**: Traditional server\-rendered website applications developed with programming languages such as Java and PHP.<br><br>* **Single\-page application**: Frontend\-backend decoupled applications built with frameworks such as React and Vue.<br><br>* **Mobile application**: Native applications installed on smartphones or tablet devices, such as iOS and Android apps.<br><br>* **M2M**: Backend service\-to\-service invocation without user interaction, such as scheduled tasks and microservices. |
   |Authorization callback URL |Enter the allowlist of callback URLs accepted by the client.<br><br><br>* After a user logs in and completes authorization, AgentKit redirects the user to this URL and attaches the authorization code or token. The client receives and processes the authorization result at this address.<br><br>* You can specify multiple URLs, one URL per row. Each URL must start with `https://`, such as `https://app.example.com/callback`.<br><br><br>> **warning**<br><br><br><br>* > You do not need to specify this parameter for some client types. Refer to the console for the required parameters.<br><br><br>* > If it is specified, make sure that it matches the actual domain of the application.<br> |
   |Enable development mode |Whether to enable development mode for the client:<br><br><br>* **Disable**: (Default) Only HTTPS is allowed, ensuring the secure configuration of AgentKit user identity management.<br><br>* **Enable**: Development mode must be enabled if you need local development or want to redirect users to protocols other than HTTPS. |

5. Click "Confirm" to create the client.

   The system generates a client ID and client secret. You can specify these two parameters in the application as the client ID and secret.

   * **Client ID**: The unique identifier of the client. It is used to identify the client application in authentication requests.

   * **Client Secret**: The secret of the client identity. It is used to verify the client identity in authentication requests.

      > **warning**

      > Client Secret is only used on trusted servers based on the corresponding client type and must not be written into frontend code or installation packages.

## Other operations

After a client is created, you can view, edit, develop, and manage the client.

**View client**

In the client list, click the name of any client to go to its details page. The details page displays client details such as the client ID, client secret, and callback URL.

**Edit clients**

In the "Actions" column of the client list, click "Edit" to modify the relevant information of the client.

> **tip**

> The client type and the automatically generated "Client ID" and "Client Secret" cannot be changed after the client is created.

|Parameter |Description |Sample value |
|---|---|---|
|**Basic information** |||
|Client name |Update the client name. |`AgentKit-Demo-Web-Client` |
|Enable development mode |Whether to enable development mode for the client:<br><br><br>* **Disable**: (Default) Only HTTPS is allowed, ensuring the secure configuration of IDENTITY.<br><br>* **Enable**: Development mode must be enabled if you need local development or want to redirect users to protocols other than HTTPS. |\- |
|**Access control and redirect configuration** |||
|Redirect URLs after logout |The list of URLs to which users can be redirected after logout.<br><br>You can enter multiple URLs, one URL per row. |`https://app.example.com/logout` |
|Cross\-origin request sources |The frontend domains allowed to initiate OAuth login requests, restricting cross\-origin request sources.<br><br>Wildcards (`*`) are supported. |`https://*.example.com` |
|Allowed CORS domains |The domains allowed to obtain tokens via asynchronous requests (AJAX), resolving frontend cross\-origin request restrictions.<br><br>You can enter multiple domains, one domain per row. |`https://api.example.com` |
|**Token validity period configuration** |||
|ID token validity period |Set the validity period of the ID token. After the token expires, the user must log in again to obtain a new one.<br><br><br>* **Unit**: seconds.<br><br>* **Default value**: 36000 seconds (10 hours) |36000 |

**Delete client**

In the "Actions" column of the client list, click "Delete". After confirming the client name in the dialog box that appears and clicking "Delete" again, the client and its configuration will be permanently deleted.

> **warning**

> Deleting a client is irreversible. Proceed with caution.

**Quick development**

AgentKit is compatible with the standard **OIDC** protocol. You can integrate using OIDC client libraries in any language (such as `authlib` for Python and `openid-client` for Node.js).

On the "Quick development" tab of the client details page, select a development platform based on your business scenario. Then, follow the development steps prompted by the console to configure client information, install dependencies, implement the login logic, and verify the development result.
