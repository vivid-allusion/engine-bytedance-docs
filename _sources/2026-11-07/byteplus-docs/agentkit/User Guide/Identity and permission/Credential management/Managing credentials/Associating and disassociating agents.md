---
title: "Associating and disassociating agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/associating-and-disassociating-agents"
---

After a credential is associated with a target agent, the agent can reference the credential at runtime to access external services. Associating and disassociating control the usage scope of a credential. Associating authorizes an agent to use the credential. Disassociating revokes that authorization before the agent goes offline, permissions are adjusted, or the credential is deleted.

**We recommend that you follow the principle of least privilege. Associate only agents with genuine business requirements**. Before disassociating an agent, confirm that the agent has stopped using the credential or has switched to another one. This prevents disruption to outbound calls in progress.

> **warning**

> Only credentials of the **API Key** and **OAuth connection** types support agent association. BytePlus cloud role credentials control usage scope through identity sources and role assignment rules, and do not support agent association.

## Application scenarios

|Actions |Scenarios |
|---|---|
|Associate an agent |* **Authorize a target agent to use a new credential**<br><br>   After you create an API Key or OAuth connection credential, you can associate a target agent with the credential if needed. The agent can then use the credential to access external services. The agent can reference the credential at runtime only after the agent is associated with the credential.<br><br>* **Adjust the authorization scope of a credential**<br><br>   When business scope, call chains, or permission requirements change, add or remove associations to update which agents are authorized to use the credential. |
|Disassociate an agent |* **Agent goes offline or no longer needs to access the target service**<br><br>   When an agent is offline or no longer needs to access the third\-party service for the credential, promptly remove the association. This reduces unnecessary credential authorization scope.<br><br>* **Clean up associations before deleting a credential**<br><br>   If a credential is associated with agents, remove all associations before deleting it. After cleanup is complete, follow the on\-page prompts to delete the credential. This prevents disruption to running agent calls. |

## Prerequisites

To associate a credential with an agent, ensure that the target agent has been created in advance and its status is normal. For more information, refer to [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en).

## Procedure

### Associate an agent

Associating an agent grants the specified agent permission to use the current credential. The association is linked to the unique identifier of the target agent. After the agent is associated with the credential, it can retrieve keys or tokens according to the credential configuration at runtime. The agent uses them to access the corresponding third\-party APIs or downstream services.

> **tip**

> We recommend that you follow the principle of least privilege. Associate the credential only with agents that have a genuine access requirement.

* > **Do not rely solely on the agent name to identify the association target**: Agent names are not unique, and multiple agents may share the same name.

* > **Agent publishing or version upgrade:** The existing credential association is generally retained. You do not need to re\-associate the credential for each version.

* > **Deleting and recreating an agent runtime**: If the new runtime still belongs to the original agent, the credential association remains unchanged.

* > **Agent recreation scenario**: If you recreate an agent and its unique identifier changes, you must associate the credential with the new agent.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Identity and Permission  **\>**  Credential management".

3. In the "Actions" column of the target credential, click the "Associate" button to go to the page for associating resources.

4. Click "Associate with more agents".

5. Click the drop\-down list, select the target agent, and then click the "Confirm" button to complete the association.

### Disassociate an agent

Disassociating an agent revokes the selected agent's authorization to use the current credential. After disassociation, the agent can no longer reference this credential. **All third\-party API calls and downstream service calls that depend on this credential may fail. Proceed with caution**.

> **warning**

* > Before disassociation, confirm that the related services have stopped using this credential or have switched to another available credential.

* > Disassociating **only prevents the agent from retrieving this credential through the platform after disassociation**. It does not automatically revoke or immediately invalidate credentials that have already been obtained. Whether keys, tokens, or temporary credentials obtained before disassociation remain usable depends on their expiration time and your service's caching mechanism. It also depends on the revocation rules of the third\-party service or cloud platform. [Learn more](https://docs.byteplus.com/en/docs/agentkit/deleting-credentials?lang=en#tZlIVnhw)

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Identity and Permission  **\>**  Credential management".

3. In the "Actions" column of the target credential, click the "Associate" button to go to the page for associating resources.

4. In the "Actions" column of the row for the target agent, click the "Disassociate" button.

5. Confirm that the agent to be disassociated is correct and click the "Confirm" button to complete the disassociation.

#### Subsequent steps

After dissociation is complete, we recommend that you use the  **"online test"**  feature of the agent runtime to initiate a controlled call. Verify that the target agent can no longer retrieve the credential through the previous association. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console?lang=en)
