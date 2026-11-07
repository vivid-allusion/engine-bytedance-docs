---
title: "Deleting memories"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_memories"
---

When a test task or related business finishes, and the memory is no longer used by any agent runtime, and its data does not need to be kept, you can delete the memory to free up unused resources. This topic describes how to delete a memory.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you delete a memory, all related data will be deleted. This operation is irreversible. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">If you delete an imported memory, it is not imported only. This does not actually delete the resource on the corresponding platform. To delete a memory, please go to the platform where the memory was created to proceed.</div>



<span id="N1gzcxaj"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Memory".

3. In the memory list, click "Delete" in the Actions column for the target memory.

4.  **(Optional)**  If you previously linked the memory to an agent runtime via **component association**, deleting the memory will trigger a warning: "This resource is associated with the following agent runtimes. Please ..." In that case, follow the steps below to remove the association between the memory and the agent runtime.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Notes   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Once the association is removed, the change takes effect immediately. The agent will no longer be able to access the memory, so make sure you assess the potential impact on your business before proceeding.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Disassociation only removes the link between the agent runtime and the memory. The original memory resources remain intact.   </div>
   

   1. Click the name of the agent runtime to navigate to the associated component page.

   2. In the memory section, click "Edit".

   3. In the pop\-up window, click "Delete", then click "Confirm".

   4. Return to the memory list page and click "Delete" in the Actions column for the target memory to delete it.
