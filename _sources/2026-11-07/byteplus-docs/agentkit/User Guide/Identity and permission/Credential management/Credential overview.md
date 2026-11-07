---
title: "Credential overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/credential-overview"
---

When an agent calls external services or downstream APIs as a client, it typically requires identity credentials. These include API Keys, OAuth client information, or cloud resource access roles. To avoid hardcoding sensitive information in code, images, configuration files, or runtime parameters, AgentKit provides identity credential hosting. It centrally stores and manages credentials for agent outbound access.

With identity credential hosting, you can securely host outbound credentials on the platform for agents that call external systems. Agent runtimes can retrieve credentials as needed. The platform reads and injects credentials and enforces permission boundaries. This reduces the risks of key leakage, misuse, and fragmented maintenance.

## Supported credential types

You can currently host the following three types of credentials:

* **API Key**

   Suitable for fixed keys provided by third\-party services. Agents can reference the key by credential name and inject it into outbound requests as needed. [Learn more](https://docs.byteplus.com/en/docs/agentkit/creating-third-party-api-key-credentials?lang=en)

* **OAuth Client**

   Suitable for accessing external services through OAuth2 authorization. For example, obtaining short\-term access tokens on behalf of a user or agent. [Learn more](https://docs.byteplus.com/en/docs/agentkit/creating-oauth-connection-credentials?lang=en)

* **BytePlus cloud role**

   Suitable for agents accessing BytePlus cloud resources such as TOS and ModelArk. The platform uses an agent's identity to obtain temporary STS credentials, avoiding long\-term fixed keys. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Policyspaceandauthenticationpoints?lang=en)

## Sensitive credential information: Storage and usage methods

### Storage methods

To protect credential security, sensitive information such as API Keys and client secrets is saved based on the selected method.

* **KMS encryption (platform storage)**

   When you select "KMS encryption (platform storage)", the platform encrypts the credential using the selected KMS master key and stores the resulting ciphertext.

* **Credential hosting (hosted storage)**

   When you select "Credential hosting (hosted storage)", the credential hosting service saves and manages the credentials. The platform retains only the credential reference and the metadata required for management.

### Usage method

In credential hosting mode, agents use credential configurations to access outbound credentials. You do not need to hardcode API Keys or client secrets in code, images, or configuration files. In credential hosting mode, there are two credential retrieval paths:

* **Outbound proxy scenario**

   A standalone proxy component retrieves credentials from the credential hosting service and injects them into request headers or parameters at the proxy layer. Plaintext credentials are visible only to the proxy process and are not passed to the agent's application runtime. This is suitable for accessing downstream APIs via MCP services, gateways, or a unified proxy. For more information, see [Create an MCP service and configure inbound and outbound authentication](https://docs.byteplus.com/en/docs/agentkit/Integrating_existing_REST_API_OpenAPI_as_MCP_tools?lang=en#9AEDRYUd).

* **SDK integration scenario**

   In the SDK integration scenario, the agent application retrieves credentials from the credential hosting service through an integrated SDK or a credential retrieval API. When credentials are retrieved, their plaintext enters the agent application's memory. The application must not write them to logs, error messages, monitoring data, or other persistent storage. For retrieval APIs and the complete process, see [Credential hosting service user guide](https://docs.byteplus.com/en/docs/agent_identity/credential-hosting-service-user-guide?lang=en).

   > Before using credential hosting, complete the SDK or API integration and configure credential retrieval authorization. Agents can use configured outbound credentials without hardcoding API Keys or client secrets in code, images, or configuration files. [Learn more](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en)
