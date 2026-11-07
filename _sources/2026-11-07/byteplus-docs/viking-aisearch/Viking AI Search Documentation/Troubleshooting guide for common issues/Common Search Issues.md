---
title: "Common Search Issues"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Multimodal_search_scenarios"
---

*To experience more Viking AI Search capabilities, visit: * [Viking AI Search, the integrated intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)


---



If your document or image searches are returning empty results, this guide can help. It explains how to diagnose and resolve common issues, such as incorrect field configurations or failed image indexing, to ensure your search functions as expected.

<span id="aefb1e93"></span>
# Troubleshooting empty search results

<span id="4fa7a9c0"></span>
## Empty document search results


1. In the console, check that the fields for document search and image search are configured correctly. Ensure that "Searchable (Document)" is checked for at least one Text field, and adjust its search weight according to your business needs.

2. Check if the filter condition parameters are correct. For details, see [Filter](https://docs.byteplus.com/docs/393/92284#aead416b).


<span id="55c91ffb"></span>
## Empty image search results


|**Items to check** |**Troubleshooting logic and recommendations** |
|---|---|
|Confirm that the image search feature is enabled |Log in to the AI search service console, navigate to the corresponding instance, and in the left navigation pane, select the \*\*Configuration \-\> Field configuration\*\* page. Find the corresponding Image field and check the "Searchable (Image)" option. If this option is not checked, the image embedding will not be stored. Only the text derived from the image will be indexed for searching. You do not need to re\-upload data. On the configuration page, click "Edit schema" and then Submit.<br><br> |
|Check if the image index was created successfully |Check the \*\*Valid items\*\* for the associated \*\*item dataset\*\* to see if the number meets expectations. This number indicates whether the image index was created successfully. For items that were not indexed successfully, go to the \*\*Dataset details\*\* of the \*\*item dataset\*\* and check the \*\*Item\*\* for error messages, such as failed image retrieval or incorrect image format. Common reasons for image index failure include:<br><br><br>* \*\*Validation failed\*\*: The image does not meet the preprocessing rules. An error code beginning with "Image" will be recorded in the Mongo status table.<br><br>* Image inaccessible: The image URL has access issues, such as timeouts or CDN blocks, which are recorded as error code 10010<br><br>* Ark TPM/RPM limit exceeded: May cause indexing to fail (low probability; a retry mechanism is available) |


&nbsp;


---



*To learn more about the capabilities of Viking AI Search, see * [Viking AI Search, an integrated intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)
