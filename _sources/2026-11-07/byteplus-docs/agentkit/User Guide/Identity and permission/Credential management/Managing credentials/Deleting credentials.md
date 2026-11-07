---
title: "Deleting credentials"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/deleting-credentials"
---

You can delete a credential when it is no longer in use, has been replaced by another credential, or must be deactivated to meet security requirements.

After deletion, the credential asset and its platform\-managed configuration are permanently removed from AgentKit. The associated agents can no longer use the original credential name or references to retrieve the API Key, obtain OAuth tokens, or request STS temporary credentials. **Deletion cannot be undone. Proceed with caution.**

## Prerequisites

Before you delete a credential, complete the following checks.

* **Confirm that the credential has no business dependencies**

   Confirm that the target credential is no longer used by any production agent, test task, or other business process. If the credential is still being used by business workloads, deleting it may cause authentication failures, OAuth authorization interruptions, or errors when accessing cloud resources.

* **Disassociate all agents (optional)**

   When an association exists, the system does not allow a credential to be deleted. If an API Key or OAuth connection credential is associated with agents, first disassociate all agents.

   > **tip**

   > BytePlus cloud role credentials cannot be associated with agents, so disassociation is not required.

* **Retain necessary audit information**

   If you might later need to trace credential purpose, association, or historical configurations, we recommend that you record necessary information such as the credential name, type, provider, associated project, and last updated time before deletion. Do not store sensitive values such as API Key or Client Secret in your records.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity and Permission ** \>**  Credential management".

3. In the "Actions" column of the target credential, click the "Delete" button.

4. After you confirm that the deletion information is correct, click the "Delete" button again to complete the operation.

## What to do next

Deleting an AgentKit credential does not automatically revoke credentials that have been issued by third\-party services or cloud platforms. Keys, tokens, or temporary credentials that have already been obtained may remain valid. You can perform the following operations as needed:

* **API Key type credentials**

   The platform does not automatically disable or delete the original API Key in the third\-party service. Go to the third\-party service console to disable or delete the key, and verify that the old key can no longer be used.

* **OAuth connection type credentials**

   The platform does not guarantee that access tokens, refresh tokens, or user authorizations already issued by the identity provider (IdP) are immediately invalidated. To terminate access immediately, revoke the token and cancel the authorization on the IdP side. If necessary, disable or delete the corresponding OAuth client.

* **BytePlus cloud roles**

   The platform does not delete IAM roles or permission policies, nor does it actively revoke STS temporary credentials that have been issued. To tighten permissions immediately, adjust the IAM role or the access control settings on the target cloud resource, and verify that the old credentials can no longer be used to access the resource.
