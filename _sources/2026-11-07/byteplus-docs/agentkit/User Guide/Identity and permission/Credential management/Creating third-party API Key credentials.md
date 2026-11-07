---
title: "Creating third-party API Key credentials"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/creating-third-party-api-key-credentials"
---

API Key credentials are used to host static access keys issued by third\-party services, which prevents you from hardcoding keys into business code, container images, or local configuration files.

This topic describes how to create an API Key credential in the AgentKit console and configure its credential name, API Key value, key storage method, encryption method, and other settings. This allows the agent to securely use the credential to access third\-party services.

> **tip**

> After you create a credential in the console, ordinary HTTP requests do not automatically include the API Key. Before using the credential, you must also complete outbound proxy or SDK integration. Configure the association between the credential and the agent, as well as the permissions to retrieve and use the credential.

* > **Outbound proxy integration:**Applies to scenarios where downstream APIs are accessed through an MCP service, gateway, or unified proxy. [Learn more](https://docs.byteplus.com/en/docs/agentkit/credential-overview?lang=en#008tylU7)

* > **SDK or API integration:** Applies to scenarios where agent business code directly calls third\-party APIs. [Learn more](https://docs.byteplus.com/en/docs/agentkit/credential-overview?lang=en#008tylU7)

## Application scenarios

* **Access external services that use static key authentication**

   An agent may need to call a third\-party model, search service, database service, or business API that uses a static API Key for authentication. In this case, you can create an API Key credential. The platform injects the key based on your configuration when the agent initiates an outbound request. This enables the agent to authenticate with the target service.

* **Avoid maintaining plaintext keys in code**

   You may not want to store plaintext API Keys in agent code, code repositories, images, configuration files, or runtime parameters. In this case, you can use an API Key credential to decouple the key from business code. This prevents sensitive information from being propagated with code or accidentally committed.

* **Centrally store, encrypt, and manage credentials**

   If your business has requirements for key security, auditing, or lifecycle management, you can encrypt credentials with a KMS primary key. Alternatively, you can use a credential hosting service to centrally store and manage credentials. This reduces the risk of key leakage and makes it easier to update and rotate credentials later.

* **Control the scope of use by project and agent**

   If the same credential must be managed by business project, environment, or resource ownership, you can configure the project to which the credential belongs. You can also associate the credential with specific agents and limit which agents can reference it, preventing unrelated agents from using the credential.

## Prerequisites

* **Obtain a valid API Key**

   You have **obtained a valid API Key from the target service provider**. You have also confirmed that the key has the permissions required for the agent to call the target service. We recommend that you also confirm the key's applicable environments, validity period, call quota, access scope, and whether restrictions such as an IP allowlist exist. This helps avoid call failures caused by insufficient permissions or environment mismatch after creation.

* **Prepare KMS key resources (optional)**

   If you choose to use a "custom primary key" for encryption when creating credentials, first create a usable key ring and primary key in KMS, and ensure that the current account has permission to use the primary key for encrypting and decrypting credentials. For details, see [Getting started with key management](https://docs.byteplus.com/en/docs/KeyManagementSystem/KeyManagementQuickStart?lang=en).

   > **tip**

   > If you do not need to manage keys yourself, you can use the system default key. The platform manages the encryption configuration to reduce extra preparation work.

* **Create the target agent (optional)**

   If you want to complete the association immediately during credential creation, create the[ target agent](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en) that will use this credential in advance. After the association, the target agent can reference this credential to make outbound calls at runtime.

   > **tip**

   > If you are not sure which agent to associate, you can create the credential first and [associate it](https://docs.byteplus.com/en/docs/agentkit/associating-and-disassociating-agents?lang=en)with an agent later.

## Procedure

### Step 1: Select a credential type

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity and Permission  **\>**  Credential management".

3. Click "Create credential". On the "Select type" page, select "API Key".

4. Click the "Next" button.

### Step 2: Configure credential parameters

1. Configure credential parameters based on the table below.

   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |API Key name |Enter a custom name for the credential. We recommend that you use a name that identifies the provider, purpose, and environment. |
   |API Key value |Enter the actual key value that you obtained from the third\-party service.<br><br>> **warning**<br><br><br>> Do not record, paste, or display the full API Key in any of the following: tickets, chat messages, runtime logs, screenshots, code repositories, configuration files, or public documents. Otherwise, the key may be leaked during collaboration, troubleshooting, or code distribution.<br> |
   |Agent identity pool (optional) |The resource pool used to manage agent identities in the current account. You can use the pool to isolate API Key credentials for different businesses or environments.<br><br><br>* AgentKit provides a default agent identity pool named` default`. If you have no requirements for business isolation, environment isolation, or independent permission management, you can use this default identity pool.<br><br>* If you need to manage credentials separately by business, team, or environment, [create an agent identity pool](https://docs.byteplus.com/en/docs/agentkit/create-agent-identity-pool?lang=en) first. Then, select the new identity pool on the current page. |
   |Encryption method |Select a secure storage method for the API Key based on your credential management requirements. The following options are supported:<br><br><br>* **KMS encryption (platform storage)** <br><br>   When the credential is written, the system encrypts it with the selected KMS primary key and stores it in the platform only as ciphertext. This option applies to scenarios where credentials must be protected by the system default key or a custom primary key.<br><br>* **Credential hosting (hosted storage)** <br><br>   Credentials are stored and managed centrally by the credential hosting service. This option is applicable to scenarios where credentials and their lifecycles need to be managed centrally. |
   |Primary key source |When the encryption method is set to ** KMS encryption (platform storage)** , the primary key source is required.<br><br><br>* **System default key**<br><br>   Managed by the platform and ready to use out of the box, with no additional configuration required. Suitable for quick access and common usage scenarios.<br><br>* **Custom primary key**<br><br>   Use your own KMS primary key to encrypt credentials. After selecting this option, select "KMS key ring" and "KMS primary key" in sequence. Suitable for scenarios with independent key management, audit, or compliance requirements.<br><br>   > **tip**<br>   <br><br>   * > For information on how to get the KMS key ring and KMS primary key, see[Prerequisites](https://docs.byteplus.com/en/docs/347/124317#kLrcpfBU).<br>   <br><br>   * > When using a custom KMS primary key, avoid disabling, deleting, or modifying key permissions arbitrarily, as this may affect credential decryption and agent calls.<br>    |
   |Set API Key passing method (optional) |Specifies where the API Key is injected when the agent sends an API request. Select an option based on the target service's authentication requirements:<br><br><br>* **Header (recommended)** <br><br>   Send the API Key as an HTTP request header. Compared with the Query method, the key is less likely to appear in URLs, access logs, or browser history. We recommend that you use this method.<br><br>   * **Parameter name**: Enter the query parameter name and the request header name, for example, `Authorization` or `X-API-Key`.<br><br>   * **Prefix**<br><br>      * The fixed prefix to add before the API Key. The system concatenates the request header value as "Prefix + API Key". It does not automatically add spaces or URL\-encode spaces in the request header.<br><br>      * If the target service requires Bearer authentication, enter "Bearer " in **Prefix**. Bearer must be followed by **one half\-width space**. This is to avoid difficulty recognizing trailing spaces in the interface.<br><br>   **Configuration example:** <br><br>   * **Example 1: With a prefix**<br><br>      * Parameter name: `Authorization`<br><br>      * Prefix: `Bearer` (followed by one half\-width space)<br><br>      * Final request header example: `Authorization: Bearer <API_KEY>`.<br><br>   * **Example 2: Without a prefix**<br><br>      * Parameter name: `X-API-Key`<br><br>      * Prefix: None<br><br>      * Final request header example: `X-API-Key: <API_KEY>`.<br><br>* **Query**<br><br>   Send the API Key as a URL query parameter. The specified query parameter is appended to the request URL, and the API Key is passed to the target service as the parameter value. This method is typically used for some legacy APIs, lightweight open APIs, or third\-party services that explicitly require identity authentication via URL parameters.<br><br>   > **warning**<br>   <br><br>   > Use **Query**only if the target service explicitly requires Query. Make sure that the URL is not recorded in logs, monitoring systems, or browser history to avoid key leakage.<br>   <br><br>   * **Parameter name**: Enter the query parameter name required by the target service, for example, `api_key`, `access_key`, `access_token`.<br><br>      > The parameter name is subject to the third\-party API documentation or integration specifications.      <br>      <br><br>   * **Prefix**: Optional. The prefix of the API Key, for example, Bearer. If the third party requires a fixed identifier to be prepended to the key, enter the identifier as required and retain the trailing space in the prefix. When a request is sent, the prefix and the API Key are concatenated and passed as the parameter value.<br><br>   **Configuration example**<br><br>   * **Example 1: Without a prefix**<br><br>      * Parameter name: `api_key`<br><br>      * Prefix: None<br><br>      * Final request URL example: `https://api.example.com/v1/resource?api_key=<API_KEY>`.<br><br>   * **Example 2: With a prefix**<br><br>      * Parameter name: `access_token`<br><br>      * Prefix: `Bearer`<br><br>      * Final request URL example: `https://api.example.com/v1/resource?access_token=Bearer%20<API_KEY>`. |
   |**Resource management** ||
   |Associated project |Specifies the project that the credential belongs to. By default, the system selects `default (the default project)`. You can also switch to another project or create a project as needed.<br><br>> The project is used to manage the resource ownership and console management permissions of the credential. It is not used as the basis for authorizing the agent to retrieve the credential at runtime. Whether the agent can retrieve the credential also depends on the association between the credential and the agent, the caller identity, and related permission settings. For more information, see [Project management](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).<br><br><br><br>* A resource can belong to only one project. When you create a credential, click the "Project" drop\-down list and select the target project. After the credential is created, its console management permissions are governed by the permission settings of the project. Only users with the required project permissions can view or manage the credential in the console.<br><br>* If the existing projects do not meet business requirements, you can click **Create project**. After the project is created, return to the current page, refresh the project list, and select the new project. |

2. After confirming that the parameter configuration is correct, click the "Create and continue" button to go to the ** Associate with agent ** page.

### Step 3: Associate with an agent (optional)

After you associate the credential with an agent, the agent can reference this credential to make outbound calls at runtime. To follow the principle of least privilege, we recommend ** associating only agents that actually need to make calls. This avoids expanding the scope of credential usage.**

> **tip**

> If you cannot determine which agents need to be authorized, you can skip this step, complete credential creation first, and then go to the credential details page later to add associations. For related operations, see [Associating and disassociating agents](https://docs.byteplus.com/en/docs/agentkit/associating-and-disassociating-agents?lang=en).

1. Select the target agent that needs to use this credential from the agent list.

2. After confirming that the selected agent is correct, click "Next".

   > If you do not want to associate an agent for now, do not select any agent and directly click "Next" to proceed.

### Step 4: Confirm the creation result

The page displays **Credential created**, indicating that the system has saved the credential. Before ending the creation process, confirm that the credential name displayed on the page matches your expectations. An incorrect name may affect subsequent lookups and usage.

1. Confirm that the credential name matches the credential that you just created.

2. To check the credential type, associated project, associated resources, or other configuration information, click "View credential details" to go to the details page.

3. After confirming that everything is correct, click "Complete" to end the creation process.

## FAQ

### How do I choose between the system default key and a custom primary key?

If you want quick integration and have no independent key management requirements, select the system default key. If your business requires self\-managed keys or independent auditing, or must meet specific compliance requirements, select a custom primary key.

### Do I need to associate an agent when I create a credential?

No. After the credential is saved, you can go directly to the next step and associate an agent later on the credential details page.

### What do I do if a credential is created but calls still fail?

Check whether the key is valid, whether the agent is associated, whether the passing method is correct, and whether the KMS primary key and identity pool permissions meet the requirements. If necessary, check the authentication error details on the target service.

### Can I use the project and agent identity pool to manage the resource ownership of a credential?

The project and agent identity pool are ownership and isolation identifiers for a credential. They mark the business scope of the credential and record the context in which the credential is created and used.

> **tip**

> The project and agent identity pool are only used to describe resource ownership and isolation scope and are not the basis for runtime authorization decisions. Configuring a project or identity pool does not mean that unified authorization is automatically granted. You cannot determine whether the agent is allowed to use the credential at runtime based on these two fields alone. Whether the agent can retrieve the credential at runtime also depends on settings such as the credential status, association, and runtime retrieval authorization.

### If I select a project or agent identity pool, does that guarantee that the agent can use the credential at runtime?

No. The project and agent identity pool can only reflect the ownership scope or isolation context of the credential. They cannot be used alone as the basis for determining runtime availability. Whether the credential is actually available also depends on the credential association, credential status, type matching, and runtime authorization settings.

### Are credential management permissions and the permissions that allow an agent to retrieve the credential at runtime the same type of permissions?

No. They are authorization capabilities at different levels. They are independent of each other and must be configured separately.

The two are related, but neither can replace the other. Having credential management permissions does not mean that the corresponding agent can retrieve the credential at runtime. Conversely, the fact that the agent can retrieve the credential at runtime does not mean that the operator has management permissions for the credential.

* **Credential management permissions**

   Controls operation permissions in the console. These permissions define who can view, create, edit, delete, and maintain credential assets and generally correspond to IAM permissions for console management.

* **Agent runtime credential retrieval permissions**

   Controls usage permissions in the runtime execution phase. The permissions define whether a specified agent is allowed to read and use the credential when executing tasks and calling downstream services.
