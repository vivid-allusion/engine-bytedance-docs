---
title: "What is Agent Identity"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/What_is_Agent_Identity"
---

The agent identity and access management platform is a one\-stop identity and access management platform, specifically designed for AI Agents and tool applications. It aims to address identity authentication, access control, and secure credential management across the entire chain from users, to agents, to backend tools (`User -> Agent -> Tool`).

Whether building an internal enterprise assistant or developing AI applications for external services, Agent Identity helps you establish a clear, reliable, and easy\-to\-manage security system, ensuring that every operation is secure, controllable, and auditable.

<span id="9c71b726"></span>
## How it works


* **Inbound authorization (Inbound Auth)** : You can create inbound authorizations on the agent identity and access management platform to authenticate and authorize callers to access Agents or gateways. You can use the user identity management component as an external identity provider or directly create an API Key within the associated service for callers to use.

* **Outbound authorization (Outbound Auth)** : You can also host outbound credentials (supporting API keys or OAuth clients) on the agent identity and access management platform, allowing Agents and gateways to use these credentials to access downstream resources.


<span id="3ef7af4f"></span>
## Core values

<span id="54b1b7ba"></span>
### **Unified identity authentication**

It unifies the management of identities for users (such as enterprise employees and external customers) and service tools (such as AI Agents, automation scripts, and microservices) that are scattered across different locations. It seamlessly integrates with your existing enterprise identity providers (IdP) through standard protocols such as OIDC and SAML to achieve single sign\-on (SSO), and assigns a unique digital identity (Workload Identity) to each Agent and tool.

<span id="ea2f8338"></span>
### **Secure credential management**

It eliminates the risks of hardcoding sensitive information such as `API Key` and `OAuth Client Secret` in code or configuration. Agent Identity provides a centralized credential vault, integrates with the Key Management Service (KMS) for high\-strength encrypted storage of all credentials, and can automatically inject credentials into Agents when needed, enabling secure and convenient access to third\-party services.

<span id="37a5d3b0"></span>
### **Granular access control**

In complex business scenarios, you can precisely define "who, under what conditions, can use which Agent to perform what actions on which tool." We use the industry\-leading Cedar policy language, enabling you to write permission policies that are both expressive and easy to understand, such as: "Only employees of the `Finance Department`, during working days, are allowed to use the `Reimbursement Agent` to call the `Payment Tool`'s `Create Payment` interface."

<span id="0126ed36"></span>
### **Seamless integration for developers**

This feature completely decouples permission check logic from business code through the permission gateway. With simple configuration on the gateway, permission policies are automatically applied to API requests passing through, without modifying the code of Agents or tools, greatly reducing integration costs and maintenance complexity.

<span id="b10a8894"></span>
## Key modules

The agent identity and permission management platform consists of the following four major modules, which work together to form a complete identity and permission solution:

<span id="bc4fa9f9"></span>
### **User identity management**

It simplifies enterprise identity integration through standardized protocols, centralizes control of user identity entry points, and reduces the complexity of multi\-system authentication. Supports user pool management, enterprise IdP (such as SAML/OIDC), and third\-party identity federation, providing user registration, login, and lifecycle management capabilities.

<span id="9a3fd0d9"></span>
### **Agent identity management**

It assigns a standardized, unique digital identity (TRN) to each computational task of a service tool and allows you to attach rich attribute tags (such as department, environment) as the basis for permission policy evaluation.

<span id="145d8349"></span>
### **Credential vault**

This module provides a secure credential vault for centralized encrypted storage and management of `API Key` or `OAuth` client credentials required to access third\-party services, eliminating the risk of plaintext credential leakage and ensuring secure access to third\-party services.

<span id="9ffe5270"></span>
### **Permission control**

Based on the Cedar policy language dynamic authorization engine and combined with the "permission policy space" and "permission gateway", this module enables fine\-grained permission control and automated verification for the complete `User -> Agent -> Tool` invocation chain.
