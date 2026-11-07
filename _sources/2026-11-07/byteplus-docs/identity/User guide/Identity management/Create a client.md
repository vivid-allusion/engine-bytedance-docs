---
title: "Create a client"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Create_a_client"
---

A client refers to an application that needs to integrate with the Intelligent Identity and Access Management Platform for user authentication. Whether it is a web application, single\-page application (SPA), mobile application, or machine\-to\-machine (M2M) backend service, you must create a client for it to obtain the **Client ID** and **Client Secret** required to initiate the authentication process.

<span id="f04dd2ba"></span>
## Core value


* **Unified identity integration**: Centrally manage authentication configurations for applications to avoid redundant development of login logic.

* **Secure boundary control**: Restrict access using callback URL allowlists, token validity periods, and more to prevent malicious requests from forging identities.

* **Multi\-scenario adaptation**: Supports various types such as web applications, single\-page applications (SPA), mobile applications, and machine\-to\-machine (M2M) services, covering different authentication requirements.


<span id="3e9bb34f"></span>
## Prerequisites

You have created a user pool; for related operations, refer to [Create a user pool](https://docs.byteplus.com/docs/identity/89611).

<span id="e787e0d4"></span>
## Steps


1. Log in to BytePlus Agent Identity Console.

2. In the left navigation bar, select **Identity Management \> User Pool**.

3. Click the target user pool name to enter the details page for the specified user pool.

4. Switch to the **Client** tab and click **Create client**.

5. Configure the relevant parameters for the client.

   
   |Configuration items |Note |Example |
   |---|---|---|
   |**Client name** |Required. Set a descriptive name for your application client, such as `my-company-portal`. |Enterprise portal web application |
   |**Client type** |Required. Select your application type:<br><br><br>* **Web application**: Traditional server\-side website applications (such as Java, PHP).<br><br>* **Single\-page application (SPA)** : Applications with a decoupled front end and back end (such as React, Vue).<br><br>* **Mobile application**: Native applications installed on mobile phones or tablets (such as iOS, Android app).<br><br>* **M2M (Machine\-to\-Machine)** : Backend service calls without user interaction (such as scheduled tasks, microservices). |Web application |
   |**Authorization callback URL** |* Required (except for M2M type).<br><br>* After the user successfully logs in and authorizes, the platform will redirect the user to this URL and attach the authorization code or token. The client must receive and process the authorization result at this address.<br><br>* Batch input is supported, one per line, and must start with `http://` or `https://`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">If not configured or configured incorrectly, authorization will fail. Ensure it matches the actual domain name of the application.</div><br> |`https://app.example.com/callback` |
   

6. Click **OK**.

   The system will generate a **Client ID** and **Client Secret** for you. You need to configure these two parameters in your application, which serve as the client's identity identifier and secret.

   * **Client ID:**  The unique identifier for the client, used to identify the client application in authentication requests.

   * **Client Secret**: The secret for the client, used to verify the client identity in authentication requests.


<span id="3b522d86"></span>
## Other operations

<span id="2cc2b54e"></span>
### View and edit clients


* **View**: In the client list, click any client name to enter its details page. The details page displays information about the client, such as Client ID, Client Secret, callback URL, and more.

* **Edit**: In the operations column of the client list, click **Edit** to modify the relevant information for the current client.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Client type, as well as the automatically generated Client ID</strong> and <strong>Client Secret</strong> cannot be changed after creation.   </div>
   

   
   |Configuration item |Description |Example |
   |---|---|---|
   |**Logout redirect URL** |Optional. List of URLs to which the user can be redirected after logging out. |`https://app.example.com/logout` |
   |**Cross\-origin request source** |* Optional. Frontend domain names allowed to initiate OAuth login requests, restricting cross\-origin request sources.<br><br>* Wildcard `*` is supported. |`https://*.example.com` |
   |**CORS allowed domains** |Optional. Domain names allowed to obtain tokens via AJAX, to resolve frontend cross\-origin request restrictions. |`https://api.example.com` |
   |**ID Token validity period** |Optional. Set the validity period of the ID Token (unit: seconds). The default is 36000 seconds (10 hours). |36000 |
   


<span id="3ed9e3aa"></span>
### **Delete client**

In the operations column of the client list, click **Delete**. This will permanently remove the client and its configuration.
