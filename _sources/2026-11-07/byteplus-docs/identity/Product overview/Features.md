---
title: "Features"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Features"
---

The agent identity and permission management platform mainly provides the following three core functions, offering comprehensive identity and permission management capabilities:

<span id="8f0cedf0"></span>
## **User identity management**


* **Core positioning**: Serves as a unified entry point for user and enterprise identities, supporting identity authentication and federated login in various scenarios.

* **Core functions**:

   * **User pool management**: You can create isolated user pools and configure login methods (email, mobile number, or username), password policies (such as complexity requirements and expiration time), and multi\-factor authentication (MFA) for each user pool.

   * **Enterprise\-level integration**: Supports integration with enterprise identity providers (IdP) via OIDC/OAuth2.0 protocols to enable single sign\-on (SSO).

   * **User lifecycle management**: You can batch import or delete users, modify their basic attributes, or synchronize user profiles based on information from external identity providers (such as department or role).


<span id="8766245f"></span>
## **Credential hosting**


* **Core positioning**: Hosts credentials for external services using encryption to prevent security risks caused by plaintext credential leaks.

* **Core functions**:

   * **Support for multiple credential types**: Supports storing various types of credentials, such as OAuth2 client credentials (Client ID/Secret) and API keys. All credentials are stored with strong encryption through a key management service.


<span id="51a511b0"></span>
## **Permission control**


* **Core positioning**: A dynamic authorization engine based on attributes and context, enabling end\-to\-end permission control from "User" to "Agent" and then to "Tool".

* **Core functions**:

   * **Policy definition**: You can write fine\-grained authorization policies using the Cedar language, for example: `permit User::"alice" to invoke Workload::"agent-001" where resource.dept == "ai-lab"`. Policies support conditional matching based on subject, resource, and action.

   * **Real\-time decision and audit**: At runtime, the system evaluates each authorization request in real time (for example, when an Agent invokes a tool), and immediately returns a decision result of `ALLOW` or `DENY`, along with detailed information about the policy used for the decision.


Through the collaborative operation of these modules, the agent identity and permission management platform has built an integrated identity security system for human, machine, and service identities. This system can meet identity and permission management requirements across all scenarios, from user login to agents calling tools.
