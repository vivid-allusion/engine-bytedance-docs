---
title: "Exporting all statements"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/exporting-all-statements"
---

The "Export all policy statements" feature lets you export the Cedar policy statements for all access rules in the current region and project. The statements are exported to a `.cedar` file. You can use the file to review policies offline, audit permissions, back up rules, and compare differences between versions.

## Recommended scenarios

* **Preserve a baseline before permission changes**

   Before adding, modifying, or deleting access rules, export and save the current policy statements to record the permission state before the change for later tracing and comparison.

* **Prepare for a security review or compliance audit**

   When you are conducting a security review, compliance audit, or permission review, export the complete original policy statements as audit evidence and a reference for permission configuration.

* **Compare the impact of rule changes**

   Export the statements before and after a policy adjustment. Compare the exported content to identify rule changes and assess the affected users, resources, and operations.

* **Save a statement snapshot before changes**

   Before you migrate policy configurations, rebuild an environment, or make bulk changes, you can export the Cedar policy statements for documentation, policy comparison, and reference when manually reconstructing policies.

   > The exported file contains only the policy statements and does not include complete environment information. When restoring the configuration later, separately verify the identities, membership relationships, resource IDs, and other dependency configurations. **The exported file cannot serve as a complete environment backup.**

* **Preserve historical configurations before deleting rules**

   Before deleting an access rule, we recommend exporting the related policy statements to preserve the original configuration record and ensure that the rule history remains traceable if the rule is deleted by mistake.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity & Permission  **\>**  Policy management".

3. Click the name of the target permission policy space.

4. Click the "Export all statements" button to complete the operation.

## Export content description

After the export is complete, the system generates a ** Cedar policy file ** with the` .cedar `extension. The default file name is `access-rules.cedar`. The exported file contains the Cedar policy statements that correspond to the access rules. Each statement consists of the following parts:

> A `.cedar` file is a plain\-text file that you can open in a text editor.

|**Field** |**Description** |
|---|---|
|`permit / forbid` |Indicates whether the policy effect is permit or forbid. |
|`principal` |Indicates the users, departments, or user groups to which the rule applies. |
|`action` |Indicates operation types such as service calls and internal ticket creation. |
|`resource` |Indicates the target agent, MCP server, or tool. |
|`Condition expression` |Indicates resource attributes, call chains, or other additional conditions. |
