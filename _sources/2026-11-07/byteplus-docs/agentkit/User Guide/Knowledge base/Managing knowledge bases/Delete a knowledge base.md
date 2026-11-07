---
title: "Delete a knowledge base"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_knowledge_bases"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deletion only removes the association between the knowledge base and AgentKit. It does not actually delete the resources on the corresponding platform. If you have already integrated the knowledge base into an agent, after disassociation, the agent will no longer be able to call this knowledge base. Please evaluate the impact on your business before proceeding.</div>


<span id="WcWYysTt"></span>
## Delete a knowledge base


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Knowledge Base".

3. Click "Delete" in the "Actions" column of the target knowledge base to complete the operation.

4.  **(Optional)**  If you have associated the knowledge base with an agent runtime via the **component association** method, the system will prompt you when deleting the knowledge base: "This resource has been associated with the following agent runtimes. Please go to the associated component page of the agent runtime to disassociate it first before deleting." Now, you can follow the steps below to disassociate the knowledge base from the agent runtime.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Notes   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After disassociating the knowledge base from the agent runtime, the change takes effect immediately. The agent will no longer be able to call this knowledge base. Please evaluate the impact on your business before proceeding.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Disassociating the knowledge base from the AgentKit agent runtime does not actually delete the original knowledge base resources.   </div>
   

   1. Click the name of the agent runtime to navigate to the associated component page.

   2. In the knowledge base section, click "Edit".

   3. In the pop\-up window, click "Delete", then click "Confirm".

   4. Return to the knowledge base page, click "Delete" in the Actions column of the target knowledge base to disassociate the knowledge base from AgentKit.


&nbsp;
