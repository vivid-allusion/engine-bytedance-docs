---
title: "Creating Volcano Engine cloud role credentials"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/creating-volcano-engine-cloud-role-credentials"
---

A BytePlus cloud role credential maps a user or agent identity in AgentKit to a BytePlus cloud role. It exchanges the mapped identity for STS temporary credentials when accessing cloud resources such as TOS and ModelArk. When creating a credential, you can select default role, rule\-based matching, caller\-specified, or hybrid mode. This supports scenarios including unified authorization, identity attribute\-based authorization, and controlled role switching.

This topic describes how to create a BytePlus cloud role credential in the AgentKit console. It also describes how to configure the identity source, cloud role assignment method, and associated project based on your business requirements.

## Recommended scenarios

* **Agent access to BytePlus cloud resources**

   When an agent needs to access TOS, ModelArk, or other resources that support BytePlus cloud role\-based authorization, create a BytePlus cloud role credential. The credential exchanges the agent's identity for STS temporary credentials to complete authentication.

* **Using temporary credentials instead of long\-term fixed keys**

   If you do not want to store long\-term Access Keys in code or configuration files, use a BytePlus cloud role credential to obtain STS temporary credentials on demand. This reduces the risk of fixed key leakage and long\-term exposure.

## Prerequisites

* #### Prepare an IAM role and authorization configuration

   * **Prepare an IAM role**

      Prepare an [IAM role](https://docs.byteplus.com/en/docs/IAM/RoleManagement#%E6%96%B0%E5%BB%BA%E8%A7%92%E8%89%B2) that can access cloud resources. Grant it only the permissions required by your business, following the **principle of least privilege**.

   * **Prepare operator permissions**

      The target IAM role must have the permissions required to access cloud resources. In addition, operators who perform role creation, policy attachment, or trust policy updates must also have the required IAM and AgentKit permissions. For details on required permissions and how to grant them, see [Granting AgentKit permissions to IAM users](https://docs.byteplus.com/en/docs/agentkit/Granting_AgentKit_permissions_to_IAM_users?lang=en).

* #### Create a user pool (optional)

   If you select **User pool** as the identity type, first create the target [user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en). When configuring the BytePlus cloud role credential, select the target user pool and associate the corresponding client. This configuration is used to identify and authenticate callers.

* #### Create an agent identity pool (optional)

   If you select **Agent identity pool** as the identity type, first create the target [agent identity pool](https://docs.byteplus.com/en/docs/agentkit/create-agent-identity-pool?lang=en). When configuring the BytePlus cloud role credential, select the target agent identity pool as the source scope for workload identities.

## Procedure

### Step 1: Select a BytePlus cloud role

A BytePlus cloud role credential exchanges an agent identity for STS temporary credentials. It is used to access BytePlus cloud resources such as TOS and ModelArk.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity and Permission  **\>**  Credential management".

3. Go to the "Credential management" page and click the "Create credential" button.

4. On the "Select type" page, select "BytePlus cloud role".

5. Confirm that the selected information is correct and click "Next".

### Step 2: Configure basic information and identity source for the cloud role

Refer to the table below to configure the basic information and identity source parameters. The identity source determines which type of principal information the system uses for role matching and STS temporary credential exchange. Select the appropriate option based on the actual calling principal.

|Parameter​ |Description |
|---|---|
|**Basic information** ||
|Name |A custom credential name used to identify the credential in the credential list and subsequent calls. We recommend a name that reflects the business, purpose, and environment, such as tos\-reader\-prod or ark\-runtime\-test. Avoid ambiguous or duplicate names. |
|Cloud service provider |Confirm that "Cloud service provider" is set to "BytePlus".<br><br>This field is fixed to "**BytePlus**" and cannot be modified manually. It indicates that the credential is used to obtain STS temporary credentials associated with a BytePlus cloud role. |
|**Identity source** ||
|Identity type |Specify the principal identity source used to obtain the cloud role. The following options are supported:<br><br><br>* **User pool**: Uses user identities and their claims from the user pool for role assignment. This option is suitable for controlling cloud resource access by user, department, user group, or other user attributes.<br><br>* **Agent identity pool**: Uses agent or workload identities for role assignment. This option is suitable for scenarios where an agent accesses BytePlus cloud resources using its own identity. |
|User pool |Select the target user pool that provides user identity information. When configuring rule\-based matching, you can use claims from the user pool identity token to map different users to the corresponding cloud roles.<br><br>> **tip**<br><br><br>> This parameter is required only when "Identity type" is set to "**User pool**".<br> |
|Client |Select the client under the target user pool. The client verifies and identifies the caller. Client options are linked to the user pool. Before a user pool is selected, this field is not configurable and displays "Select a user pool first".<br><br>> **tip**<br><br><br>> This parameter is required only when "Identity type" is set to "**User pool**".<br> |
|Agent identity pool |Select the target identity pool that provides agent or workload identities. The field displays "Select a workload pool". Subsequent requests use the principal identities in this pool for role assignment and temporary credential exchange.<br><br>> **tip**<br><br><br>> This parameter is required when "Identity type" is set to "**Agent identity pool**".<br> |

### Step 3: Configure cloud role permissions

Select one of four modes based on your permission model and role assignment method: "**Default role", "Rule\-based matching", "Caller\-specified", or "Hybrid mode**". The selected mode determines how the system identifies the corresponding IAM role for each request during STS temporary credential exchange.

* **Default role**: Always uses a preset IAM role to handle requests.

* **Rule\-based matching**: Automatically matches an IAM role based on attributes carried in the request, using custom rules.

* **Caller\-specified**: The caller explicitly declares the IAM role to use in the request.

* **Hybrid mode**: Combines multiple selection strategies and selects an IAM role based on priority.

**Default role**

This mode is easy to configure. All requests that meet the identity source requirements use the same role. If different users or agents require the same permissions to access cloud resources, select "**Default role**". All requests then use the specified IAM role to obtain temporary credentials.

> **tip**

> We recommend granting the minimum necessary permissions to the default role. This prevents all calling principals from sharing a role with excessive permissions.

1. In "Configuration method", select "Default role".

2. In "Default role", click "Click to configure". Select an existing IAM role, or enter a name and press Enter to create a new role.

   * **If using an existing IAM role**: Confirm the target role has the permission policies required to access business resources. If the role lacks the required permissions, find the target permission policy in the IAM console. Click "Authorize" to grant the permission policy to the role. For more information, see [Authorization instructions in permission policy overview](https://docs.byteplus.com/en/docs/IAM/PolicyOverview).

      After you select a role, the console checks its trust policy. The policy must allow the ID service to assume the role.

      > * **Trusted entity**: ID service.

      > * **Allowed action**: `sts:AssumeRole`. This allows the ID service to assume the role and obtain temporary credentials.

      * If the required trust configuration is already included, proceed directly.

      * If the required trust configuration is missing, the console displays the "**Confirm updating role trust policy**" dialog box. After confirmation, the platform retains the existing trust configuration. It appends a trust entry allowing the ID service to perform `sts:AssumeRole`. Existing configurations are not overwritten.

   * **If creating a new IAM role on the current page**: Enter the role name on the "**Configure cloud permissions**" page and press Enter. Then select the required permission policies. After confirmation, the platform creates the role, attaches the policies, and writes the necessary trust configuration.

      > **tip**

      > Permission policies attached to the role determine its base resource permissions. A "dynamic permission policy" further restricts the effective permissions within that scope during a call. It does not replace the role's base resource authorization.

3. (Optional) Configure a dynamic permission policy to inject an IAM policy at call time and further restrict the effective permissions of the role. Use `${claim_name}` to reference claims in the OIDC token.

   > The policy content must be valid IAM Policy JSON.

4. Confirm that the cloud permission configurations are correct and click "Confirm".

**Rule-based matching**

Select **Rule\-based matching** when different departments, user groups, or users require different cloud resource access permissions. The system dynamically maps requests to the corresponding cloud IAM role based on claims in the user pool or agent identity pool.

> Rule\-based matching uses claim information in the OIDC token to select the IAM role dynamically. The system evaluates rules in priority order (as displayed on the page). Once a rule is matched, the system uses the role associated with that rule to obtain STS temporary credentials.

1. In "Configuration method", select "Rule\-based matching".

2. Configure the priority, claim name, operator, match value, and role for each matching rule:

   * **Priority**: A lower number indicates higher priority. The system evaluates rules from top to bottom. Once a request matches a rule, evaluation stops, and the system uses the role associated with that rule to obtain STS temporary credentials.

   * **Claim name**: Enter the name of the claim field in the OIDC token to evaluate.

   * **Operator**: Select the comparison operator, such as equals or contains.

   * **Match value**: Set the target value that the claim field must match.

   * **Use role**: Specify the cloud IAM role to use when the rule is matched. After configuration, you can delete individual rules.

   > **tip**

   > A default rule entry is provided. Click "Add rule" to add more rules. A maximum of 24 rules can be configured per group.

3. (Optional) Enable "Use default role" as a fallback policy.

   * **Enable**: If no rules are matched, the system uses a fallback role to obtain STS temporary credentials to ensure business continuity.

   * **Disable**: If no rules are matched, the call is denied, and no cloud resource access is granted.

**Caller-specified**

When callers need to select the target IAM role based on different business scenarios, select **Caller\-specified**. This mode uses a **role allowlist** to restrict the roles a caller can select. It prevents unauthorized or overprivileged IAM roles from being used.

> **tip**

> Callers can specify only IAM roles in the allowlist. The system rejects any role not in the allowlist. This prevents callers from bypassing the platform's permission controls.

1. In "Configuration method", select "Caller\-specified".

2. In the role allowlist, click "Add role" to add cloud roles that callers are allowed to specify.

   > **tip**

   * > The role allowlist supports a maximum of **24** roles. If a caller specifies a role not in the allowlist, the system does not use that role to obtain temporary credentials.

   * > We recommend adding only the roles required by your business. Avoid adding administrative or overly permissive IAM roles.

3. (Optional) Configure a dynamic permission policy for the selected IAM role as needed. The policy is specified as **an IAM Policy JSON**. At runtime, it is passed as the Policy parameter to STS to further restrict the permissions of the selected IAM role. This enables least\-privilege control. Use this capability when you need to refine access by user, department, project, or request context under the same role.

   > The dynamic permission policy can reference claims in the identity token. At request time, each claim reference is replaced with its actual value. This further restricts the selected role's permissions. Before configuration, confirm that the token contains the required claims and that the resulting policy is valid IAM Policy JSON.

4. Confirm the role allowlist and cloud permissions configuration and click "Confirm".

**Hybrid mode**

Hybrid mode supports both **caller\-specified roles** and **rule\-based role matching**. It is suitable for scenarios with complex role selection logic. For example, some requests require the caller to specify an IAM role. Other requests automatically match a role based on claims in the identity token.

> **tip**

> The system selects a role in the following order:

* > **The caller specifies a role**: The system first checks whether the specified role is in the role allowlist.

   * > If the role is in the allowlist, the system uses it to request STS temporary credentials.

   * > If the role is not in the allowlist, the system denies the request. Claim rule matching is not performed, and no fallback to the default role occurs. The caller must use a role in the allowlist, or an administrator must review and update the allowlist.

* > **The caller does not specify a role**: The system evaluates claim\-matching rules in configuration order. When a rule is matched, the system uses the IAM role corresponding to the first matched rule to request STS temporary credentials.

* > **No rules are matched**:

   * > "Use default role" enabled: Use the configured default role.

   * > "Use default role" not enabled: Deny the request.

1. In "Configuration method", select "Hybrid mode".

2. Configure the role allowlist to restrict the roles a caller can explicitly specify. For details, see the **Caller\-specified** tab.

3. Configure claim matching rules to automatically assign roles to requests that do not specify a role. For details, see the **Rule\-based matching** tab.

4. Configure "Use default role" as a fallback policy based on business needs:

   > The default role applies only when the caller does not specify a role and no rules are matched. If the caller specifies a role that is not in the allowlist, the default role is not used as a fallback.

   * **Enable**: When the caller does not specify a role and no claim\-matching rules are matched, the system uses the default role as the fallback.

   * **Disable**: When the caller does not specify a role and no rules are matched, the request is denied.

### Step 4: Configure resource management

In the "**Resource management**" section, select the credential's project. The system initially selects "default". You can switch projects or create one as needed.

> A **project** is a collection of resources. You can add the credential to a specified **project** and centrally manage it at the project level. This enables resource isolation and data security controls. For more information, see [Project management](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).

* A resource can belong to only one project. To change the project of a credential, click the "Project" drop\-down list and select the target project.

* After a project is selected, the credential is accessible only to users who have permissions for that project.

* If the existing projects do not meet your business needs, you can click "Create project" to create one. After you create the project, return to this page and select the new project.

### Step 5: Submit and confirm the result

1. Check the name, identity source, configuration method, role, and project.

2. After confirming that all information is correct, click "Create".

3. When you reach the "Completed" stage, verify that the credential was created and view its details as needed.
