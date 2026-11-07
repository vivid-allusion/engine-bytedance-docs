---
title: "Creating permission policy spaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-permission-policy-space"
---

A permission policy space is a logical container for managing permission policies in AgentKit. You can create separate permission policy spaces for different projects or business scenarios, such as expense reimbursement, to isolate and categorize policies. This topic describes the capabilities available in permission policy spaces and how to create a permission policy space.

## Feature overview

A permission policy space is a container for permission policies and the sole location for managing permission definitions. Within a permission policy space, you can maintain a set of authorization principals (who), access targets (such as tools, agents, or knowledge bases), and allow/deny policies.

* By default, the system maintains a default permission policy space for each project. Newly created access rules are generally added to this default space automatically, so you do not need to create a space manually in most scenarios.

* If you need isolation by business line, environment (production/test), or gateway instance, you can create a separate permission policy space.

> **warning**

> Do not create a separate permission policy space for each rule. **A space** defines a coarse\-grained policy boundary, whereas**access rules**define fine\-grained authorization.

## Considerations

* **Deny by default**: If a permission policy space contains no allow rules, all requests are denied by default. Creating a permission policy space alone does not change authorization behavior. Access rules must be published within the space before they take effect.

* **Do not modify the default system space**: The system automatically maintains the default permission policy space for each project. Do not manually add business rules to the default space to achieve isolation.

* **Deleting a space is a high\-risk operation**: Deleting a permission policy space also deletes all policies within it. Deletion is blocked once the space is [referenced by the gateway Identity authentication plugin](https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description?lang=en). Before deleting the space, make sure that no gateway service or agent depends on it.

* **Determine the space name once**: The permission policy space name serves as the business key for downstream references. Gateway plugins reference the space by its permission policy space ID, and renaming the space invalidates existing references.

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity & Permission  **\>**  Policy management".

3. On the "Policy management" page, click the "Create permission policy space" button.

4. Configure the permission policy space parameters.

   |Parameter​ |Description |
   |---|---|
   |Space name |Set a custom name for the permission policy space based on the naming rules displayed on the page.<br><br>After creation, the permission policy space name serves as a downstream business key and is used in strong references from components such as the gateway Identity authentication plugin. Renaming the space invalidates many downstream references. **We recommend that you determine the space name once**. |
   |Project |Select the project that the permission policy space belongs to. You can also click "Create new projects" to create a project. The project determines the scope of bill splitting and IAM authorization. Choosing the wrong project leads to high migration costs later. |
   |Tag |Click "Add tag" and enter key\-value pairs to configure tags for the permission policy space, so that you can later filter by business line or environment in the list. |

5. Click the "Confirm" button to create the permission policy space.

## What to do next

After creating a permission policy space, you can start defining permission rules within it or associating it with a gateway:

* [Create an access rule](https://docs.byteplus.com/en/docs/agentkit/creating-access-rules?lang=en): You can create access rules within the permission policy space to define user access permissions to resources.

* [Associate the gateway authentication plugin](https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_plugin_configuration_description?lang=en): When the gateway needs to perform authentication on inbound requests, select this permission policy space in the Identity authentication gateway plugin. This determines which gateway resource enforces the policies of this space.
