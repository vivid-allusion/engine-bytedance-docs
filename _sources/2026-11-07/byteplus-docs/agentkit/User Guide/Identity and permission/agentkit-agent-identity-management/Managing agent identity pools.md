---
title: "Managing agent identity pools"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/view-and-manage-identity-pool"
---

This topic describes how to create an agent identity pool and how to view, edit, manage, and delete the agent identities associated with the pool.

## Agent identity pools

### View the identity pool list

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. In the "Agent identity pool" list, click the name of the target identity pool to view basic information about the default pool (named "default") and custom identity pools, as well as their associated agent identities.

   **Basic information**

The following table describes the main items in the "Basic information" section.

   |**Field** |**Description and usage** |
   |---|---|
   |ID |A short, system\-generated ID. It is mainly used to identify the agent identity pool when you submit a ticket for troubleshooting. |
   |TRN |The globally unique resource name of the agent identity pool.<br><br>> **warning**<br><br><br>> The TRN of an agent identity pool is a resource locator. You cannot use it directly as the trusted principal in an IAM trust policy. To allow agent identities in the pool to access cloud resources, assume a role based on OIDC. For details, see [AssumeRoleWithOIDC](https://docs.byteplus.com/en/docs/IAM/AssumeRoleWithOIDC).<br> |
   |Associated credentials |Associated credentials determine the set of external credentials (such as API Keys, OAuth, and cloud roles) that agents in the pool can use to access external resources. |
   |OIDC discovery URL |The OIDC Metadata URL of the agent identity pool. External systems, such as BytePlus IAM and customer\-built gateways, use this URL to obtain the Issuer, JWKS, and public keys and to verify the signature of the tokens presented by agents. When you use [AssumeRoleWithOIDC](https://docs.byteplus.com/en/docs/IAM/AssumeRoleWithOIDC?lang=en), configure this URL in the IAM identity provider. |

   **Agent identity**

Displays the agent identities associated with the identity pool and their details. For descriptions of the main fields in the "Agent identity" list, see the "Agent identities" section below.

### Edit an identity pool

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. In the "Agent identity pool" list, find the target identity pool and click "Edit" in the "Actions" column to update the description of the identity pool.

   > **tip**

   > Currently, you can update only the description and cannot update other configurations.

### Delete an identity pool

> **warning**

* > Deleting an agent identity pool is a high\-risk operation. The system does not perform cascading deletion. To delete an agent identity pool, delete all agent identities in the pool first (that is, delete the corresponding agents in Agent Runtime). Otherwise, the deletion is blocked.

* > After you delete an agent identity pool, the system immediately stops issuing new tokens. However, the system cannot guarantee that all tokens already issued become invalid immediately before they expire naturally because of mechanisms such as JWKS caching and offline signature verification at the gateway.

* > If an IAM role references the agent identity pool as a trusted OIDC Provider, delete the trust relationship in IAM first. Otherwise, the delete request is rejected.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. In the "Agent identity pool" list, find the target identity pool and click "Delete" in the "Actions" column to delete the identity pool.

## Agent identities

### View an agent identity

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. In the "Agent identity pool" list, click the name of the identity pool that contains the target agent identity.

4. On the identity pool details page, view the details of the agent identity in the "Agent identity" section.

   The following table describes the main fields in the agent identity list.

   |**Column** |**Description** |
   |---|---|
   |TRN |The globally unique resource name of the agent identity. It is used as the Principal in Cedar policies. |
   |Type |* **Agent**: A business agent.<br><br>* **Tool**: A registered tool identity. |
   |Creation source |* **AgentKit**: Automatically registered when you create an agent on AgentKit.<br><br>* **User\-created**: Registered by an external platform through the API. |

   ###

### Edit an agent identity

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. In the "Agent identity pool" list, click the name of the identity pool that contains the target agent identity.

4. On the identity pool details page, find the target agent identity in the "Agent identity" section and click "Edit" in the "Actions" column to update the agent identity configuration.

> **tip**

> You cannot update the identity name or identity type. For information about other updatable parameters, see [Creating an agent identity](https://docs.byteplus.com/en/docs/agentkit/create-agent-identity?lang=en).

### Delete an agent identity

> **warning**

* > Deleting an agent identity is usually triggered automatically when you delete the agent. After you delete the identity manually, the system can no longer issue tokens for this identity. Proceed with caution.

* > If the identity is still referenced by access rules, credentials, or IAM trust relationships, the system blocks the deletion. Remove each reference as prompted on the page and try again.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. In the "Agent identity pool" list, click the name of the identity pool that contains the target agent identity.

4. On the identity pool details page, find the target agent identity in the "Agent identity" section and click "Delete" in the "Actions" column to delete the agent identity.
