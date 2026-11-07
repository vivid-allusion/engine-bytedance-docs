---
title: "Creating agent identity pools"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-agent-identity-pool"
---

This topic describes how to create and configure an agent identity pool in AgentKit, and how agent identities are associated with credentials, policies, and IAM roles.

## Application scenarios

AgentKit provides a default agent identity pool (named "default") that is sufficient for most scenarios. Consider creating an agent identity pool only in the following scenarios:

* You need strong environment isolation. For example, create one pool for production and one for testing, with completely separate Token Issuers.

* Different business lines require independent bill splitting across different projects.

* You need a dedicated identity pool that an external platform, such as a CLI tool or a self\-built control plane, creates and hosts automatically through the API.

> **warning**

> Do not create a separate identity pool for each agent. An agent identity pool is a coarse\-grained identity boundary. One pool can host all agents on the same business line. If the default pool meets your requirements, we recommend against creating an agent identity pool.

## Considerations

* After you create an agent identity pool, its name serves as a downstream business key. We recommend against renaming it later.

* The list contains the default pool named default. You cannot delete the default pool.

* Do not change the OIDC discovery endpoint URL of a pool. If you change it, all IAM roles and gateways that trust the pool will fail signature verification.

## Prerequisites

You have created at least one agent. Otherwise, the agent identity list in the pool is empty. For details about creating an agent, see [Deploying an agent in 1 minute](https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit) and [Developing and deploying agents](https://docs.byteplus.com/en/docs/agentkit/Developing_and_deploying_agents).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. On the "Agent identity pool" page, click "Create agent identity pool".

4. Configure the agent identity pool parameters.

   |Parameters |Description |
   |---|---|
   |Identity pool name |Set a custom name for the agent identity pool based on the naming rules displayed on the page.<br><br>After creation, the pool name serves as a downstream business key that is strongly referenced by the Token Issuer, IAM trust policies, and other resources. Renaming the pool causes extensive downstream failures. **Decide on the name once**. |
   |Associated project |Select the project that the agent identity pool belongs to. You can also click "Create new projects" to create a project. The project determines the scope of bill splitting and IAM authorization. Choosing the wrong project leads to high migration costs later. |
   |Tag |Click "Add tag" and enter key\-value pairs to configure tags for the agent identity pool. Tags facilitate pool filtering in the list. |
   |Automatically create identity |* When you enable this feature, the system automatically creates an agent identity for a trusted workload the first time the workload accesses the pool.<br><br>* When you disable this feature, register the agent identity explicitly during the agent creation process or create it manually. For details, see [Creating an agent identity](https://docs.byteplus.com/en/docs/agentkit/create-agent-identity?lang=en). |

5. Click "Create" to create the agent identity pool.

## Verify results

Go back to the "Agent identity pool" list. The new agent identity pool appears with the correct information, such as its name, associated project, and tags. On the details page, you can view the system\-generated ID, TRN, and OIDC discovery endpoint URL.

## What to do next

* [Create an agent identity](https://docs.byteplus.com/en/docs/agentkit/create-agent-identity?lang=en)

* [Manage agent identity pools](https://docs.byteplus.com/en/docs/agentkit/view-and-manage-identity-pool)
