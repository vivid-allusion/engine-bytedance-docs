---
title: "Create a knowledge base"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/create_a_knowledge_base"
---

To create a new knowledge base for your RAG applications, you can follow the steps in this guide. This document provides detailed instructions on the creation process, explaining each parameter from basic information and data types to advanced settings like embedding models and indexing algorithms, ensuring you can successfully set up a knowledge base and import your documents.

<span id="9153265c"></span>
# Procedure


1. Click "Create knowledge base" in the upper right corner of the knowledge base list page to open the knowledge base creation page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d20b7e2ae1db4a16b40bbe8279ed4446~tplv-goo7wpa0wc-image.image) </span>


2. Set related parameters on the **Create knowledge base** page, as described in the following table.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/329237702c484bedb6c7f0bb02b9af41~tplv-goo7wpa0wc-image.image) </span>


3. Fill in the relevant parameters on the **Create knowledge base** page. The specific parameters are as follows.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf8871d7529242b6ba218a51a2c1fcd5~tplv-goo7wpa0wc-image.image) </span>


|**Configuration category** |**Parameter name** |Required |**Parameter description** |
|---|---|---|---|
|Basic information |Name |**Required** |Specify the name of the knowledge base to be created.<br><br><br>* Only English letters, numbers, and underscores (_) can be used, and the name must start with an English letter and cannot be empty.<br><br>* Length requirement: [1, 64]<br><br>* The knowledge base name must be unique. |
||Description |**Required** |Customize the description of the knowledge base.<br><br><br>* Length requirement: [0, 500]<br><br>* For example: A knowledge base for the legal industry is created, with the description "Legal document knowledge, including 'Amendment XII to the Criminal Law of the People's Republic of China', 'Civil Code of the People's Republic of China', and other statutes, as well as recent judicial documents." |
||Data type |**Required** |The data type of the knowledge base.<br><br><br>* Unstructured data (hybrid data): Suitable for data with different file structures, such as articles, reports, books, and so on. These documents usually have rich content and complex layouts, requiring the platform to parse and segment them. Supported document formats: pdf, ppt, txt, markdown, doc, xlsx, csv, jsonl, faq<br><br>* Structured data: Suitable for data with identical file structures, such as Q&A, user data, product data, and so on. These documents usually have clear and standardized structures and do not require platform segmentation. Supported document formats: csv, xlsx, jsonl, faq.xlsx |
|Configure knowledge base |Text embedding model |**Required** |You can select other models based on your business needs.<br><br>The characteristics and usage recommendations for each model are as follows:<br><br><br>* **Short\-text high\-precision + keyword model**: This model combines the advantages of the Short\-text high\-precision model and the versatile edition, integrating semantic retrieval and keyword matching. It is ideal for short\-text processing.<br><br>* **Multilingual model**: This model supports multiple languages and cross\-language retrieval and integrates semantic retrieval and keyword matching, with an input window of up to 8,000 tokens. It is suitable for long\-text processing.<br><br>* **Short\-text high\-precision model**: This model supports only Chinese and purely semantic retrieval. It is suitable for short\-text processing. |
||Multimodality embedding model |**Required** |* **Skylark\-embedding\-vision\-250328+ keyword model**: The mixed vector model is a multi\-model combination scheme based on dense vectors and sparse vectors, which provides better retrieval performance<br><br>* **Skylark\-embedding\-vision\-250328** : A visual vector model that can simultaneously vectorize text and images, understand the content of images, and supports only dense vectors. |
||Vector dimension |**Required** |Controls the dimensionality of the vectors generated when mapping raw text, images, and other data into high\-dimensional space. The higher the value, the higher the retrieval accuracy. If the data volume is extremely large and performance requirements are very high, consider dimensionality reduction to improve retrieval efficiency. |
||Slicing method |**Required** |Configuration is supported only when the data type is "unstructured data".<br><br>Supports default slicing rules and custom slicing rules<br><br><br>* Default slicing rules: Uses the platform's default slicing rules.<br><br>* Custom slicing rules: Allows you to set custom text delimiters and text fragment merging strategies. |
||Default slicing rules / Maximum slice length |**Required** |Configuration is supported only when the data type is "unstructured data" and the slicing method is "default slicing rules".<br><br>The maximum length of a single text fragment after parsing and slicing. Please ensure that the maximum slice length is slightly less than the maximum input length of the embedding model; otherwise, any text exceeding the limit will be discarded by the model. |
||Default slicing rules / Merge short text fragments |Optional |Configuration is supported only when the data type is "unstructured data" and the slicing method is "default slicing rules".<br><br>Configure whether to merge short text fragments; merged fragments will be limited to not exceeding the maximum slice length. |
||Default slicing rules / Image OCR |Optional |Configuration is supported only when the data type is "unstructured data" and the slicing method is "default slicing rules".<br><br>Configure whether to enable image OCR capability. When enabled, text recognition is supported for images in pdf and docx documents to assist with retrieval. |
||Custom slicing rules / Delimiter symbol |**Required** |Configuration is supported only when the data type is "unstructured data" and the slicing method is "custom slicing rules".<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a separator is set, the maximum slice length limit and short text merging strategy will not take effect, and images cannot be parsed. Tables will be processed as regular text paragraphs.</div><br> |
||CPU quota |**Required** |The CPU quota consumed by index retrieval; 1 CPU core allows approximately 100 QPS. If retrieval consumes more CPU than the quota, the index will be rate limited. The format must be a positive integer. |
|Field configuration |Upload document |Optional |Configuration is only supported when the data type is "structured data".<br><br>You can upload a sample document for determining the table structure. Subsequent knowledge base documents must comply with this structure specification and support csv, xlsx, and jsonl formats. |
||Table structure |**Required** |Configuration is only supported when the data type is "structured data".<br><br>Used for field validation during subsequent document import. |
|Advanced configuration |Indexing algorithm |**Required** |Indexing algorithm, default is HNSW\-Hybrid. Enumeration values: HNSW\-Hybrid, HNSW, FLAT.<br><br><br>* HNSW: Full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional spaces, which is a graph\-based index. HNSW reduces the number of nodes accessed during the search process by constructing a multi\-layer network, enabling fast and efficient nearest neighbor search. It is suitable for large\-scale datasets and scenarios with high retrieval performance requirements.<br><br>* HNSW\-Hybrid: HNSW algorithm supporting hybrid indexing. The hybrid indexing algorithm can index both dense and sparse vectors in the dataset, and returns results that take into account the similarity of both types during retrieval. Suitable for scenarios requiring high search efficiency and simultaneous retrieval of sparse and dense vectors.<br><br>* FLAT: Brute\-force indexing. During search, all vectors in the vector database are traversed and compared with the target vector by calculating distances. The query speed is relatively slow, but FLAT can provide a 100% recall rate. It is suitable for small\-scale datasets and scenarios with high retrieval accuracy requirements.<br><br><br>Different embedding models have different indexing algorithm configurations:<br><br><br>* Short text high precision + Keyword model: supports HNSW\-Hybrid<br><br>* Multilingual model: supports HNSW\-Hybrid, HNSW, and FLAT<br><br>* Short\-text high\-precision model: supports HNSW and FLAT<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Multilingual models generate both dense and sparse vectors, which are respectively suitable for semantic retrieval and keyword retrieval. The default HNSW\-Hybrid algorithm can handle both dense and sparse vectors, balancing semantic similarity and literal matching to deliver better retrieval results.</div><br><br><br><div data-tips="true" data-tips-type="warning">You can also use the HNSW or FLAT algorithm with multilingual models. In this case, the index will only include the dense vectors produced by the model, meaning only semantic retrieval is supported.</div><br> |
||Quantization method |**Required** |A compression method for vectors in the index that can reduce the complexity of similarity calculations. For high\-dimensional and large\-scale vectors, quantization can effectively reduce storage and computation costs. Default is Int8. Enumeration values: Int8, Float, Fix16.<br><br><br>* Int8: Compresses a 4\-byte float into a single byte to achieve memory and computation latency benefits, resulting in slight precision loss. For example, cosine distance may yield values greater than 1. By sacrificing some retrieval accuracy, retrieval performance is improved and resource costs are reduced.<br><br>* Float: Full precision, no compression or quantization applied.<br><br>* Fix16: Compresses a 4\-byte float into two bytes to achieve memory and computation latency benefits, resulting in slight precision loss. By sacrificing some retrieval accuracy, retrieval performance is improved and resource costs are reduced. |
||Tag / Add field |Not required |Click the "Add tag" button under the field list to add a custom tag. These tags can be used to filter documents during online retrieval. |
||Tag / Tag name |**Required** |Enter the field name. This cannot be empty, and names must not be duplicated. The length must be between [1, 128]. |
||Tag / Tag type |**Required** |Select the field type from the dropdown list. Available values: bool, list, int64, float32. |
||Tag / Tag options |Not required |When the selected type is list, you can specify option values, which can be directly selected when tagging documents later. |
||Tag / Delete |Optional |Click to delete the current tag. |



4. After completing the form, click "Create knowledge base" on the right. The interface will display "Knowledge base created successfully". To import documents immediately, click "Import now" in the pop\-up window. To import later, select "Do not import for now".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2e7071edbe6418090a5cbf65278184a~tplv-goo7wpa0wc-image.image) </span>


5. Document import supports four methods: local upload, TOS import, importing Feishu documents, and public download links. Refer to [Knowledge base quota description](https://docs.byteplus.com/docs/209/Knowledge_base_quota_description)and the frontend sample files to prepare documents for import.
