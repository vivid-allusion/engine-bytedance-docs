---
title: "Identity management overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/agentkit-identity-management-overview"
---

This topic introduces the capabilities, core add\-ons, issues solved, and responsibilities of user identity management in AgentKit.

## What is user identity management

User identity management is a core capability of AgentKit for agents and applications. It answers three questions: **who can use your application**, **how they log in**, and **how their account and identity data are centrally managed**.

The user identity management module centralizes the scattered questions of "who the users are, whether they can access the application, and how they log in" across business systems. Applications can get registration, login, password recovery, third\-party account integration, token issuance, and user lifecycle management capabilities without building their own account systems. Administrators can complete all configurations for user pools, clients, users, external login sources, and authentication in the AgentKit console.

## What issues does it address

* **Slow application integration**: Through the standard OIDC protocol and preconfigured runtime endpoints, applications can quickly complete authentication integration.

* **Duplicate account systems**: A unified user pool stores identities shared by multiple applications, preventing each application from building its own account system.

* **Difficult external login integration**: The system supports connection types such as OIDC, OAuth, SAML, WeCom, and Token Exchange. Therefore, you can enable enterprise or third\-party login with a single configuration.

* **Uncontrollable authentication and security**: You can centrally configure login methods, registration policies, messaging services, and token validation rules, and audit authentication behavior through CloudTrail.

## Overview of the identity system

The entire identity management system uses the **user pool** as its boundary and container, the **client** as the integrated application, the **user** as the managed identity subject, and the **identity provider** (IdP) as an additional login source. The **authentication configuration** determines how users pass verification to enter the system. These four components work together around the user pool to issue tokens for applications to validate and support troubleshooting through audit logs.

## Core add\-ons and responsibilities

|Component |Responsibilities |Key **identifiers/configurations** |**References** |
|---|---|---|---|
|User pool |The container and boundary for managing user identities, determining login, registration, account recovery, and branding experience. |* User pool ID, TRN, and OIDC discovery endpoint.<br><br>* Login attributes and registration attributes, which cannot be modified after creation. |[User pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) |
|Client |An application integrated with the user pool that contains the trust and token configuration. |Client ID, client secret, authorization callback URL, and ID token validity period. |[Client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en) |
|User |A managed identity entity that can carry identifiers and profile data and be linked to an external identity. |* Username, email address, mobile number, verification status, and user status.<br><br>* Department, user group, and custom attributes. |[User](https://docs.byteplus.com/en/docs/agentkit/create-user?lang=en) |
|IdP |Provides third\-party login sources and associates external identities with users in the user pool. |Connection type (OIDC/OAuth/SAML/WeCom/Token Exchange), attribute mapping, and account provisioning policy. |[Login sources](https://docs.byteplus.com/en/docs/agentkit/add-an-external-identity-provider?lang=en) |
|Authentication |Centralizes the "login method + registration method + message channel + device code" and determines how a single login is completed. |Login method, registration method, messaging service (SMS/email), and device code flow. |[Authentication](https://docs.byteplus.com/en/docs/agentkit/configure-authentication-information?lang=en) |

## Quick reference for key terms

|**Terms** |**Explanation** |
|---|---|
|User pool |The logical container for managing user identities and the boundary for authentication experience and resource ownership. |
|Client |The application integrated with the user pool, identifying itself via the Client ID/ Client Secret. |
|IdP |The trusted external identity system that provides third\-party login sources. |
|OIDC discovery endpoint |An endpoint that exposes runtime metadata such as authorization, token, and JWKS information and serves as the basis for application integration. |
|Attribute mapping |Rules for writing fields returned by an external IdP to user attributes in the user pool. |
|Account provisioning policy (ProviderOptions) |Controls how external identities are linked to, used to create, or used to update local users. |
|Messaging service |SMS and email delivery channels for login with verification codes, registration confirmation, and password recovery. |
|Device code flow |The OAuth flow in which a device with limited input capability completes login on another device using a short code. |
|UserPool Token / Agent Token |The OIDC/JWT identity tokens issued for end users and workloads respectively. |

## Boundaries and precautions

* The **login attributes** and **registration attributes** of a user pool cannot be modified after the user pool is created. Confirm your business requirements before creating the user pool.

* Password login is forcibly enabled by the system and cannot be disabled, ensuring a fallback login method is always available. SMS code login is enabled by default, and email address login is disabled by default.

* Deleting a user pool is irreversible. Before deleting it, you must first remove all associated clients and users. After the user pool is deleted, newly issued tokens become invalid immediately, and already\-issued tokens remain usable until they expire.

* Client Secret is sensitive information. Keep it confidential to prevent disclosure. For token validation, obtain the JWKS from the OIDC discovery endpoint and reject the none algorithm.

* Headless authentication and the device code flow require the target client to have the corresponding capabilities (such as DeviceFlowEnabled) and the required scopes. Complete the client configuration first.
