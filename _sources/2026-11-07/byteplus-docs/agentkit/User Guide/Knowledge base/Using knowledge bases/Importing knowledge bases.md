---
title: "Importing knowledge bases"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases"
---

**Importing a knowledge base** associates a Viking Knowledge base created in BytePlus **VikingDB** with the AgentKit console in one click, allowing an agent in the agent runtime to directly use the retrieval, recall, and Q&A capabilities of the knowledge base. After import, the knowledge base is still hosted by VikingDB, where its documents, chunks, and vector indexes are maintained and billed. AgentKit accesses the knowledge base through the association without duplicate storage or incurring additional charges.

This topic describes how to import the Viking Knowledge Base.

<span id="USp81DIw"></span>
## Usage notes

Supports cross\-region import of Viking knowledge bases from the China (Hong Kong) region.

<span id="2DTlGQVG"></span>
## Knowledge base fees

Fees are charged based on the billing method that you select when creating a knowledge base. Knowledge bases offer two billing methods: **pay\-as\-you\-go (postpaid)**  and **prepaid**. You can select only one billing method for each knowledge base.


* **Pay\-as\-you\-go (postpaid)** : You use resources before paying for them. Fees are included on your bill and can be settled after it is issued. A pay\-as\-you\-go knowledge base may incur **compute resource fees, storage resource fees, and model call fees**.

* **Prepaid**: You pay before using resources, and fees are settled by order. Payment is deducted when you place the order, and no corresponding usage bills are generated afterward.


For specific billing rules, billing items, and pricing, see [Knowledge base billing](https://docs.byteplus.com/en/docs/RAG_Cloud/Knowledge_Base_Billing).

<span id="HPJBszFR"></span>
## Prerequisites

A Viking knowledge base has been created, and files have been uploaded to the vector database. For details, see  [Creating knowledge bases](https://docs.byteplus.com/en/docs/RAG_Cloud/Create_a_knowledge_base).

<span id="AXRPmjaf"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Knowledge Base".

3. Click the "Import knowledge base" button.

4. In the pop\-up window, select "Viking".

5. Select the knowledge bases to be imported, and click "Import".


<span id="vHE6l8BA"></span>
## What to do next

After the import is complete, you can perform the following operations on this knowledge base in AgentKit:


* Test the recall effectiveness on the [Knowledge retrieval](https://docs.byteplus.com/en/docs/agentkit/Knowledge_retrieval) page.

* Conduct direct interactive Q&A with the LLM based on this knowledge base on the [Knowledge Q&A](https://docs.byteplus.com/en/docs/agentkit/Knowledge_qa_testing) page.

* Verify the imported document content and chunking structure on the [View original documents](https://docs.byteplus.com/en/docs/agentkit/Viewing_original_documents) and [View chunk details](https://docs.byteplus.com/en/docs/agentkit/Viewing_chunk_details) pages.

* [Integrate the knowledge base into an agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent) in the agent runtime so that the agent can retrieve knowledge at runtime.

* [Disassociate](https://docs.byteplus.com/en/docs/agentkit/Deleting_knowledge_bases) **.**
