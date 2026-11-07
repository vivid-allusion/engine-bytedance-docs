---
title: "Creating user pools"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-user-pool"
---

A user pool is the basic boundary for AgentKit to manage user identities and the authentication experience. You can create independent user pools for different businesses, applications, or user groups, and configure login, registration, account recovery, and branding methods separately. Users, application clients, and external identity connections all belong to a specific user pool and use the authentication configuration of the user pool.

## What can a user pool manage

* **User pools**: Logical containers for managing user identities, including three major modules: user accounts, client information, and identity provider management.

* **Users**: Natural people or system accounts with a unique identity identifier, including basic attributes (such as the email address and mobile number).

* **Clients**: Applications integrated with the user pool (such as mobile apps and enterprise official websites). They must be created and managed in the user pool in advance. These applications can access the authentication services (such as login and token acquisition) provided by the user identity system only after a unique identifier (client ID) is obtained.

* **IdPs**: Support third\-party account login (such as Feishu and Google). The user pool synchronizes third\-party account information (avatar and nickname) and can connect to external identity systems such as OIDC, OAuth, SAML, and WeCom.

* **Authentication experience**: Unified configuration of login, registration, verification, account recovery, and branding.

* **Runtime information**: Provides the domain, issuer, discovery URL, and callback URL required for application integration and external identity connections.

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management".

3. On the "User pool management" page, click "Create user pool".

4. Configure user pool parameters.

   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |User pool name |Specify a custom name for the user pool. This name is part of the unique identifier of the user pool and cannot be updated after the user pool is created. This is because it is strongly referenced by clients, token issuers, and other resources. Changing the name will cause many downstream businesses to fail. |
   |**User pool attribute configuration** ||
   |Attributes for user pool login |Select the identity identifiers used when users log in to the user pool, such as the username, mobile number, and email address. For example, if you specify the username and mobile number here, users must provide both the username and the mobile number when logging in to the application.<br><br>> **warning**<br><br><br><br>* > This configuration cannot be modified after creation.<br><br><br>* > In addition to the default username, select either email address or mobile number as a required attribute. Otherwise, users cannot recover their passwords by themselves after forgetting them.<br> |
   |Attributes for user pool registration |Select the identity identifiers that a user needs to provide during registration, such as the username, mobile number, and name. For example, if you specify the username and mobile number here, users must provide both the username and the mobile number when registering for the application.<br><br>> **warning**<br><br><br>> Registration attributes include all login attributes by default and cannot be changed.<br> |
   |**Resource management** ||
   |Associated project |Assign a project to the user pool to manage O&M, authorization, and other operations of user pool resources from the project dimension. The project named **default** is selected by default. For more project\-related operations and descriptions, see [Project management](https://docs.byteplus.com/en/docs/agentkit/Managing_projects). |
   |Tag |Add tags to the user pool to facilitate resource categorization and filtering. For more tag\-related operations and descriptions, see [Tag management](https://docs.byteplus.com/en/docs/agentkit/Tag_management).<br><br><br>* Click "Add Tag" to add a key\-value pair.<br><br>* You can add up to 20 tags. |

5. Click "Confirm" to create the user pool.

   The system automatically creates a new user pool, which has a unique user pool ID, TRN, and OIDC discovery endpoint.

   * **TRN** **:**  A unified resource identifier used for cross\-service resource association.

   * **OIDC discovery endpoint**: The discovery endpoint of the OIDC protocol, which is used by OIDC clients to obtain information about the user pool. It contains all metadata on how to interact with your user pool via OIDC, such as the authorization endpoint, token endpoint, and public key information. When you want to use this user pool as an identity provider for integration with other applications or services, you usually need to provide this URL.

## What to do next

After the user pool is created, the page displays the `Created` message. You can directly associate clients with the user pool on the page and configure user information to ensure the user pool works as expected.

* [Create a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side): Click "Create Client" on the page to associate a client with the current user pool.

* [Create a user](https://docs.byteplus.com/en/docs/agentkit/create-user): Click "Create user" or "Batch import" on the page to associate users with the current user pool.

## Other operations

After a user pool is created, you can view, edit, and manage the user pool, or create a third\-party login source for the user pool.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Identity and Permission" \> "User pool management".

3. On the "User pool management" page, view, edit, and manage user pools, or create third\-party login sources for the user pools.

**View and edit user pools**

* **View**: In the user pool list, click the name of any user pool to go to its details page. The details page will display the basic information of the user pool, OIDC discovery endpoint, callback URL, and the associated clients, users, and external IdPs.

* **Edit**: In the "Actions" column that corresponds to the target user pool, click "Edit" to update the description of the user pool.

> **tip**

* > Currently, only the user pool description can be updated.

* > The login and registration attributes of the user pool, as well as other system\-generated identifiers, cannot be changed after creation.

**Create login sources**

In the "Actions" column that corresponds to the target user pool, click "Create login source" to manage the user identities of the login agent by configuring an external identity provider. For more information and operation instructions, see [Creating login sources](https://docs.byteplus.com/en/docs/agentkit/add-an-external-identity-provider).

**Delete user pools**

In the Actions column of the user pool list, click "Delete". The system prompts you for a second confirmation.

> **warning**

* > Deleting a user pool is irreversible. Before deleting a user pool, you must first remove all clients and users associated with the user pool.

* > After deletion, all data and configurations associated with this user pool will be permanently destroyed. Applications that depend on this user pool will no longer be able to perform user authentication.
