---
title: "Create a user pool"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Create_a_user_pool"
---

To manage user identities for your applications, you can create a user pool. This guide provides step\-by\-step instructions for creating a user pool, which serves as a logical container for managing users, configuring login methods, defining password policies, and integrating external identity providers.

<span id="38249cf1"></span>
## **Core components**


* **User pool (User Pool):**  A logical container for managing user identities, including three main modules: user accounts, client information, and identity provider management.

* **User (User):**  A natural person or system account with a unique identity identifier, including basic attributes (email, phone number).

* **Client (Client):**  An application that connects to the user pool, which is **the end\-user application** (such as a mobile app, corporate website, and so on). It must be created and managed in the user pool in advance. After obtaining a unique identifier (**Client ID**), it can use the authentication services of the user identity system (such as login and token acquisition).

* **External identity provider (IdP):**  A service that supports third\-party account login (such as Feishu, Google, and more). The user pool will synchronize third\-party account information (such as avatar and nickname).


<span id="a4c9a973"></span>
## Prerequisites

You have enabled the Intelligent Identity and Access Management Platform service. For related operations, refer to [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

<span id="208686be"></span>
## Procedure


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Identity Management \> User Pool**.

3. Click **Create User Pool** in the upper right corner.

4. Configure the user pool parameters.

   
   |Configuration items |Note |
   |---|---|
   |**User pool name** |Required. Set a unique name for your user pool, for example, `my-app-users`. |
   |**Description** |Optional. Briefly describe the purpose of this user pool, for example, "used for managing internal and external users of the XX application." |
   |**User pool login attributes** |Select the identity identifiers that users can use to log in.<br><br><br>* Optional values: **Username**, **Mobile number**, **Email**<br><br>* Default values: **Username, mobile number**<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration cannot be modified after creation.</div><br> |
   |**User pool registration attributes** |Select the identity identifiers that users must provide during registration.<br><br><br>* Optional values: **Username**, **Mobile number, Email, full name, given name, family name, middle name, and more**<br><br>* Default values: **Username, mobile number** |
   |**Associated project** |* Select the project to which the user pool belongs, for resource isolation and management.<br><br>* You can select an existing project from the drop\-down list, or click **New Project** to create a new project. |
   |**Tags** |* Add tags to the user pool for resource classification and filtering.<br><br>* Click **Add Tag** to add a new key\-value pair.<br><br>* You can add up to 20 tags. |
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/463f1825a7044e3685096e7c464920b4) </span>

5. Click **OK**.

   The system will automatically create a new user pool for you and generate a dedicated **User Pool ID**, **TRN**, and **OIDC discovery endpoint**.

   * **TRN** **:**  A unified resource identifier used for cross\-service resource association.

   * **OIDC discovery endpoint**: The discovery endpoint of the OIDC protocol, used by OIDC protocol clients to obtain information about the user pool. It contains all metadata about how to interact with your user pool via OIDC, such as the authorization endpoint, token endpoint, public key information, and more. To integrate this user pool as an identity provider for other applications or services, you typically need to provide this URL.


<span id="a0e27545"></span>
## Subsequent actions

After creating the user pool, the page will display a `successfully created` notification. You can directly associate clients with the user pool and configure user information on the page to ensure the user pool functions properly.


* Create client: Click **create client** on the page to associate a client with the current user pool. For related operations, see [Create a client](https://docs.byteplus.com/docs/identity/89609).

* Create user: Click **create user** or **bulk import** on the page to associate users with the current user pool. For related operations, see [Create a user](https://docs.byteplus.com/docs/identity/89595).


<span id="7181ed69"></span>
## Other actions

<span id="f92c7ec3"></span>
### View and edit user pool


* **View**: In the user pool list, click the name of any user pool to enter its details page. The details page displays basic information about the user pool, OIDC discovery endpoint, callback URL, and associated clients, users, and external identity providers.

* **Edit**: In the operations column of the user pool list or at the top right of the details page, click **Edit**. Currently, only the user pool name and description can be modified.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">The login and registration attributes of the user pool, as well as other system\-generated identifiers, cannot be changed after creation.</div>


<span id="8ac2c516"></span>
### Delete user pool

In the operations column of the user pool list, click **Delete**. The system will prompt you for confirmation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>



* <div data-tips="true" data-tips-type="warning">Deleting a user pool is an irreversible operation. Before proceeding, you must first remove all associated <strong>clients</strong> and <strong>users</strong> under this user pool.</div>


* <div data-tips="true" data-tips-type="warning">After deletion, all data and configurations related to this user pool will be permanently destroyed, and applications that depend on this user pool will be unable to perform user authentication.</div>
