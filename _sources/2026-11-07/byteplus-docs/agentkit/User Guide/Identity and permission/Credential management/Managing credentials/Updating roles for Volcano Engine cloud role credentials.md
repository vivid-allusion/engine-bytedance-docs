---
title: "Updating roles for Volcano Engine cloud role credentials"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/updating-roles-for-volcano-engine-cloud-role-credentials"
---

Updating the role **adjusts the IAM role used by a BytePlus cloud role credential**. After the update, the system uses the new role to obtain STS temporary credentials. These credentials allow access to cloud resources according to the new role's permissions. The following jointly determine the newly issued credentials' access: the new role's permissions, dynamic permission policy, and cloud\-service permissions. They determine which cloud resources the credentials can access and which operations they can perform.

If the new role does not have the permissions required by the business, calls to TOS, ModelArk, or related tools may fail. Before proceeding, confirm that the new role has the correct trust relationships and permission policies configured. [Learn more](https://docs.byteplus.com/en/docs/IAM/PolicyOverview?lang=en)

## Limits

Whether the role can be updated directly depends on the role configuration method currently used by the credential.

|**Configuration method** |**Whether direct update is supported** |**Description** |
|---|---|---|
|Default role |Supported |The credential uses a fixed role. Use  **"Change role"**  to replace the role directly. |
|Rule\-based matching |Not supported |Identity claims and matching rules determine the role. Use "[Edit credential](https://docs.byteplus.com/en/docs/agentkit/editing-credentials?lang=en)" to adjust the matching rules and corresponding roles. |
|Caller\-specified |Not supported |The caller specifies the role from the allowlist. Use ["Edit credential"](https://docs.byteplus.com/en/docs/agentkit/editing-credentials?lang=en) to adjust the role allowlist. |
|Hybrid mode |Not supported |The caller or rule\-matching results determine the role. Use "[Edit credential](https://docs.byteplus.com/en/docs/agentkit/editing-credentials?lang=en)" to adjust the role allowlist, matching rules, or default role. |

## Application scenarios

* **Adjust default access permissions**

   When the permission scope of the default role no longer meets business requirements, replace it with an IAM role that has more appropriate permissions.

* **Reduce role permissions**

   When the original role has an overly broad permission scope, replace it with a new role that follows the principle of least privilege. This reduces the risk of unauthorized access.

* **Handle role changes or retirement**

   When the original IAM role is about to be deactivated, deleted, or have its trust relationships modified, switch to a new available role in advance. This prevents disruption to agent access to cloud resources.

* **Adjust dynamic role assignment logic**

   When the credential uses rule\-based matching, caller\-specified, or hybrid mode, adjust the role allowlist, matching rules, and fallback role by editing the credential. Do not update the role directly.

## Prerequisites

The target [IAM role](https://docs.byteplus.com/en/docs/IAM/RoleManagement#%E6%96%B0%E5%BB%BA%E8%A7%92%E8%89%B2) has been created.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Identity and Permission  **\>**  Credential management".

3. In the "Actions" column of the target credential, click the "Change role" button.

4. Confirm that the credential name and current role are correct. In the "New role" section, click the current role name.

5. Click the IAM role drop\-down list, select the target role, and click "Confirm".

6. Confirm that the role information to be updated is correct, and click "Confirm change" to complete the operation.

## What to do next

After the role is changed, initiate a cloud resource call to confirm that the system can obtain STS temporary credentials using the new role. Verify that the new role's permission scope meets business expectations.

1. **Obtain temporary credentials using the new role**

   Initiate a call through the target agent that requires access to cloud resources. This causes the system to obtain STS temporary credentials using the new role. We recommend that you use a new request or session for verification. This avoids reusing old credentials cached in business processes, running instances, or previous sessions. To verify through an agent runtime, refer to [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).

2. **Verify the new role's permissions**

   > **warning**

   > Verifying the new role's permissions only confirms that business calls succeed. It does not prove that the new role correctly restricts unnecessary permissions.

   After obtaining the new credentials, verify the following:

   * **Allow results**: Use the new credentials to perform operations required by the business. Confirm that the target cloud resources are accessible.

   * **Deny results**: Attempt to access resources outside the permission scope or perform unauthorized operations. Confirm that the requests are denied as expected.

   * **Call trace**: Check responses, runtime logs, and error messages. Confirm that calls use the new role and that the dynamic permission policy resolves and applies as expected.

   * **Business impact**: Check agents, scheduled tasks, and downstream services that depend on this credential. Confirm that no call failures occur due to insufficient permissions in the new role.

3. **Handle old temporary credentials**

   * **Confirm when the old credentials expire**: Check the `Expiration` field returned with the temporary credentials. Record the old credentials' latest expiration time. For field description and sample response.

   * **Stop using old credentials**: Stop distributing old credentials to new requests, scheduled tasks, and background jobs. Clear credential caches in business processes, running instances, and sessions. When reinitiating requests, ensure the system uses the new role to obtain new STS temporary credentials.

   * **Adjust old role permissions**: Before old credentials expire naturally, **check whether other services, agents, scheduled tasks, or cloud resource call chains still use the old IAM role**. Assess business risks to determine whether to update the permission policies attached to the old role. Remove permissions for operations or resources that the business no longer requires. For specific operations, refer to [Other operations for configuring IAM policies](https://docs.byteplus.com/en/docs/TorchObjectStorage/ConfiguringIAMpolicies?lang=en#8a43f59c).

   * **Restrict permissions on the cloud resource side**: The target cloud service might support resource policies, access control lists, network access controls, or other service\-side restrictions. If so, simultaneously revoke the old role's access to target resources. For configuration details, see the permission management documentation of the corresponding cloud service.

   * **Verify that old credentials are unavailable**: Use the old credentials to initiate a read\-only test on the target resource. Confirm that the request is denied. At the same time, use the new credentials to verify that operations required by the business can still be performed. To verify through an agent, run an online test in the agent runtime. For specific operations, refer to [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).
