---
title: "(Beta) Use Documents as Knowledge Base"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/document_knowledge_base"
---

To enhance your Conversational Search Assistant, you can use existing platform documentation as a knowledge source. This feature allows the Agent to combine unstructured document data, such as service policies or brand information, with structured product data to provide more comprehensive answers. 

This guide explains the value of this capability and shows you how to import a document dataset, use it in conversations, and interpret the citation data in the API response.


* **E\-commerce (Service & Policy):**  By importing **Membership Policies** or **After\-Sales Service Guides**, the Agent can answer user inquiries regarding discount eligibility, return windows, or warranty coverage during the shopping process.

* **E\-commerce (Expertise & Branding):**  By introducing **Vertical Industry Knowledge**, you can help the Agent better interpret user needs and generate more accurate search queries. Examples include:

   * **Brand Heritage:**  Sharing the history and philosophy of a luxury brand.

   * **Efficacy & Usage:**  Explaining the active ingredients in skincare or technical specs in hardware.

   * **Pairing & Styling:**  Providing professional advice on how to match apparel or supplement routines.


We currently offer free access to the beta version of document data Q&A, which you can use by importing a [Document Dataset](https://docs.byteplus.com/docs/393/Document_Dataset).

<span id="827731f3"></span>
# Import Document dataset

You can directly import and link a document dataset in the application interface and upload your document data. For detailed steps, see: [Document Dataset](https://docs.byteplus.com/docs/393/Document_Dataset).

<span id="e5bc4bd7"></span>
# Use document data in conversations

After linking the document dataset with the application, the Conversational Search Assistant can use the document dataset as a knowledge source, supporting viewing and referencing knowledge content in the documents during each Q&A session.

Citations are used to output referenced content during the streamed response process. You can view the cited document data in the console experience interface and click to see the original document text.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ba6d9f81e7bd422c9595591850599016) </span>

&nbsp;

<span id="730210cf"></span>
# Streaming output citation tag

During streaming output, the system automatically inserts citation tags (citation) into the output content to reference the source of the cited document. The output example is as follows:

```JSON
{
    "request_id": "328b48f8-bdfa-42a1-b1ba-7bc57f9a14e1",
    "result": {
    "content": "",
    "citation": [
        {
            "_id": "31828f343447a80ca5e6c644f1f0ee90",
            "dataset_id": "169073633",
            "type": "document",
            "display_fields": {
                "dataset_type": "document",
                "doc_id": "31828f343447a80ca5e6c644f1f0ee90",
                "doc_name": "The Ultimate Guide to Necklace Layering: How to Mix and Match for a Unique Fashion Statement.pdf",
                "doc_path": "bff/unstructured_data/2103536866/31828f343447a80ca5e6c644f1f0ee90",
                "doc_type": "pdf",
                "text": "[Original excerpt from the referenced document]"
             }
         }
    ]
}
```


See the return parameter details: [Get Streaming Response](https://docs.byteplus.com/docs/viking-aisearch/92249#ee78e5dc)
