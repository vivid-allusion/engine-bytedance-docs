---
title: "Creating agent identities"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create-agent-identity"
---

An agent identity (AEI) is the stable, authorized identity of an agent asset and is bound to the agent asset on a one\-to\-one basis. An agent identity is the sole principal for permission requests during outbound calls from the agent backend. This topic describes the steps and related parameter configurations for manually creating an agent identity, and how to manage identity pools.

## Application scenarios

In most cases, you do not need to manually create an agent identity. Each time you create an agent in AgentKit, the system automatically registers an agent identity in the default identity pool (name: default, description: default pool). When you delete the agent, the system also deletes the agent identity. This topic applies mainly to scenarios where you view or troubleshoot existing agent identities, or where an external platform explicitly registers agent identities through the API.

An agent identity's main capabilities are as follows:

* Create an independent identity for an agent, application, or service.

* Query and maintain workload identity information.

* Clean up the identity after the workload is disabled.

* Act as the principal for the workload identity information in access tokens.

## Procedure

AgentKit provides the following two methods for creating an agent identity.

**Method 1: Automatic registration during agent creation (recommended)**

1. Create and publish an agent in the [AgentKit console](https://console.byteplus.com/agentkit). [Learn more](https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit?lang=en)

2. The system automatically registers the corresponding WorkloadIdentity in the default identity pool (named "default"). No additional operations are required.

3. When you publish the agent, the authorization of the referenced tools is converted into permission policies for the WorkloadIdentity. Publishing the agent again does not create a duplicate identity, and changing the agent version does not change the WorkloadIdentity.

**Method 2: Manual creation in the console**

This method applies to external platforms (such as the VeOps CLI) or integration scenarios where you need to explicitly register an identity in the console.

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, choose "Identity and Permission" \> "Agent identity management".

3. On the "Agent identity pool" page, click the name of the target identity pool.

4. In the "Agent identity" section, click "Create agent identity".

5. Configure the identity parameters as described in the following table.

   |Parameter​ |**Description** |
   |---|---|
   |Identity name |Set a custom name for the agent identity based on the naming rules displayed on the page. The name must be unique within the account and must correspond to the agent asset on a one\-to\-one basis in the integration chain. |
   |Identity type |Agent identity type. Valid types include:<br><br><br>* **Agent**: A business agent that acts as the requester or caller in the system.<br><br>* **Tool**: A registered tool identity that acts as the callee or resource provider in the system. |
   |OAuth2 callback URL |Click "Add callback URL" to add a callback URL that is used after OAuth2 authorization for the resource is complete.<br><br>The agent identity needs to access an external resource that is protected by OAuth2, such as a third\-party service or an API that requires user login and authorization. In this case, the authorization server redirects the browser to the URL specified here after the user grants authorization. The server then includes the authorization code in the URL. The agent then exchanges this authorization code for an access token, which completes the OAuth authorization flow.<br><br>> **warning**<br><br><br><br>* > The callback URL must **exactly match** the callback URL registered in the authorization server (IdP or third\-party application backend). The protocol, domain name, port, and path must all match. Otherwise, the authorization server returns an error and rejects the request.<br><br><br>* > You can add multiple callback URLs to distinguish development, test, and production environments, or to serve multiple frontend entry points.<br> |
   |Metadata |Click "Add metadata" to attach custom key\-value pairs to the agent identity as tags or attributes.<br><br>If a key has multiple values, separate the values with a comma (`,`), for example, `env=prod,test`. |

6. Click "Create" to create the agent identity.

## Verify results

On the identity pool details page, the new identity appears in the "Agent identity" section, along with its type (Agent or Tool), creation source, TRN, and other information. You can use the TRN as a principal in a Cedar policy.
