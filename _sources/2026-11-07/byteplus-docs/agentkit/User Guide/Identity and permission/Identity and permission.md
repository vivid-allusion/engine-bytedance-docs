---
title: "Identity and permission"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01"
---

AgentKit has integrated the user identity management and outbound credential escrow features of the [Agent Identity and Permission Management Platform](https://docs.byteplus.com/en/docs/identity/What_is_Agent_Identity). By leveraging the core capabilities of a unified identity management system, AgentKit enables its own user identity authentication and secure outbound credential escrow, further ensuring the security and compliance of identity\-related actions during on\-chain interactions.

<span id="Gzz7rgDs"></span>
## How it works


* **Inbound authentication (Inbound Auth):**  Create inbound authentication to authenticate and authorize callers to access the agent and gateway. You can use the User identity management component as an external IdP, or directly create an API Key within the attached service for callers to use.

* **Outbound authentication (Outbound Auth):**  Entrust outbound credentials (supporting API Key or OAuth client), allowing the agent and gateway to use these credentials to access downstream resources.


<span id="dm5WSxFz"></span>
## Basic concepts

This document only explains the terminology involved in the use of the AgentKit platform. For more terminology and functions of the [Agent Identity and Permission Management Platform](https://docs.byteplus.com/en/docs/identity/What_is_Agent_Identity), please refer to the [Glossary](https://docs.byteplus.com/en/docs/identity/Glossary).


|Noun |Explain |Purpose |Related documents |
|---|---|---|---|
|**User pool** |Logical container for managing user identity, including user account, authentication configuration, client information, and identity provider association. |Isolates user data across different business lines and unifies authentication policies (such as password rules, MFA configuration). |[User pool management](https://docs.byteplus.com/en/docs/identity/Create_a_user_pool) |
|**User** |A natural person or system account with a unique identity identifier, including basic attributes (email, phone number). |Participates in the authentication process as the identity principal to obtain access permissions. |[User management](https://docs.byteplus.com/en/docs/identity/Create_a_user) |
|**Client** |Application identifier for accessing the user pool, used to obtain user authorization. |Distinguishes the access scope of different applications and controls token issuance (for example, only allowing web applications to obtain refresh tokens). |[Client management](https://docs.byteplus.com/en/docs/identity/Create_a_client) |
|**IdP** |Third\-party authentication services (such as WeCom or Google) enable federated login with the user pool through OIDC/OAuth2 protocols. |Simplifies the enterprise user login process, eliminating the need for separate account registration. |[External identity provider management](https://docs.byteplus.com/en/docs/identity/Add_external_identity_providers) |
|**OIDC（OpenID Connect）**  |Authentication protocol based on OAuth2.0, with extended support for obtaining user information (such as email, avatar). |Standardizes third\-party login processes, avoiding redundant development of authentication logic. ||
|**OAuth2.0** |Authorization framework that allows third\-party applications to obtain access to user resources (without sharing passwords). |Controls the scope of resource access (such as read\-only or read\-write permissions), and supports multiple authorization flows (such as authorization code flow, M2M). ||
|**OAuth client credentials** |Stores client ID and secret for third\-party services (such as Google or GitHub Client ID/Secret). |Securely manages sensitive credentials to prevent plaintext hardcoding (for example, credentials are automatically injected when an agent calls the Google API). |[Credential management](https://docs.byteplus.com/en/docs/identity/Credential_management) |
|**API Key credentials** |An access key for third\-party services (such as Alibaba Cloud API Key), stored in plaintext, but the storage is protected by encryption. |Simplifies the authentication process for agents calling external services (for example, directly obtaining the API Key from the credential management module). ||


<span id="zL1cxFcx"></span>
## Procedure


1. [Enable the Agent Identity and Permission Management Platform and complete authorization](https://docs.byteplus.com/en/docs/identity/Enable_Agent_Identity_and_complete_authorization): Before using the Agent Identity and Permission Management Platform for the first time, you need to enable the service and complete authorization.

2. Enable authorization for the agent.

   * [Inbound authentication: Enable quick log in for your agent](https://docs.byteplus.com/en/docs/identity/Enable_fast_login_functionality_for_your_Agent): Quickly integrate standard security log in functionality for your agent through the Agent Identity and Permission Management Platform.

   * [Inbound authentication: Integrate enterprise SSO for federated log in](https://docs.byteplus.com/en/docs/identity/Integrate_enterprise_SSO_for_federated_login): Integrate with existing enterprise identity systems (such as Okta, Azure AD, Google Workspace). Once configured, enterprise employees can log in to your application directly using their existing enterprise account without re\-registration.

   * [Outbound authentication: Agent accesses BytePlus resources on behalf of the user](https://docs.byteplus.com/en/docs/identity/Agent_accesses_BytePlus_resources_on_behalf_of_the_user): To allow your agent to access BytePlus cloud resources, you can configure a dedicated IAM role for it through the Agent Identity and Permission Management Platform, enabling secure authorization for relevant service calls.

   * [Outbound authentication: Agent accesses third-party resources on behalf of the user](https://docs.byteplus.com/en/docs/identity/Agent_accesses_third-party_resources_on_behalf_of_the_user): Enables your Agent to securely access third\-party services that support OAuth 2.0 on behalf of the currently logged\-in user, such as querying Google weather, reading Feishu documents, and performing actions on GitHub repositories.
