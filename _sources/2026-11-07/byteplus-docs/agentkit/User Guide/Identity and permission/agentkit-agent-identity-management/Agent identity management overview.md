---
title: "Agent identity management overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/agent-identity-management-workload-pool"
---

This topic describes the core capabilities of AgentKit agent identity management and the problems that it solves. This topic helps you understand what the agent identity pool (WorkloadPool) and agent identity (WorkloadIdentity) are, and how an agent identity works with credentials, policies, and IAM roles.

> **tip**

> This topic is intended for administrators and platform integration engineers who have enabled AgentKit and need to run agents in production environments.

## Addressed issues

User management controls where users log in to agents, whereas agent identity management controls the agents themselves. When an agent calls MCP tools in the background, accesses BytePlus resources, or performs tasks on behalf of users, agent identity management defines the identity that the agent uses to authenticate and the permission policies that it follows.

Unlike the practice of configuring a long\-term API key for each agent, the AgentKit agent identity management module uses the workload identity (WorkloadIdentity) model. In this model, each agent has a stable identity in an identity pool, and the identity pool issues a short\-term token at runtime. Access policies control permissions, and no long\-term keys are generated or used at any point.

## Three layers of concepts

|**Layer** |**Definition** |**Lifecycle** |**Analogy** |
|---|---|---|---|
|Agent identity pool (WorkloadPool) |The token issuance boundary and the JWKS / Issuer boundary. It holds the signing key pair and manages a group of agent identities. |Long\-term and at the organization level. |Similar to an internal IdP project. |
|Agent identity (WorkloadIdentity) |A stable, authorized identity that is bound one\-to\-one to an agent asset and is the Principal in Cedar policies. |Long\-term. It follows the lifecycle of the agent asset. The automatically generated WorkloadIdentity is deleted along with the agent. |Similar to an identity card for an agent. |
|Temporary runtime identity (WorkloadIdentityToken) |The short\-term token (WIT/TIP) that each session or agent runtime obtains. |Short\-term. We recommend setting it to expire when the session ends. |Similar to a temporary access card. |

## Precautions and best practices

* **If the default pool meets your needs, we recommend against creating a new pool:**  All agents under the same account do not require Issuer isolation and do not involve project\-based billing, so the default pool is sufficient. The agent identity pool is a coarse\-grained enterprise\-level boundary. Do not create pools for individual agents or business lines.

* **Do not add long\-term AK/SK to agent configuration:**  Do not configure long\-term AK/SK for an agent. Instead, use short\-term tokens issued by the identity pool together with access rules, so that keys do not end up in code or configuration.

* **Do not share a TRN externally:**  A TRN is a resource locator. Use it in appropriate scenarios, such as policies, and do not share it externally through session windows, files, or other channels.

* **Do not change the OIDC discovery endpoint URL:**  Changing the OIDC discovery endpoint URL causes signature verification to fail for all IAM roles and gateways that trust it.

* **Confirm the identity list before deleting an agent:**  Check whether the WorkloadIdentity of the agent is referenced by other policies or credentials.

* **Confirm the identity pool type:**  Identities of the Tool type in the list are the identities of the registered tools, not your business agents. Choose the Principal carefully when you configure policies.
