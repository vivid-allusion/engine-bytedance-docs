---
title: "Multimodal retrieval"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Multimodal_retrieval"
---

<span id="025ecd24"></span>
## Scenario description

In scenarios involving multimodal data, especially those containing both text and images or videos, business scenarios often require multidimensional retrieval of data:


1. For label types, quickly filter and search the label fields based on label values to obtain precise search results.

2. For text types, perform full\-text search on text fields based on certain keywords to find the most similar text descriptions.

3. For image and text types, first perform embedding operations on the field to obtain new vector fields, then use vector search to find the closest fields.


These three retrieval models are sometimes independent, meaning only one retrieval model is used, while in other scenarios, all three methods are used simultaneously to obtain the most similar results. This requires our data solution to meet the following requirements:


1. The storage solution must have distributed capabilities, allowing horizontal scaling as data volume increases.

2. The storage solution must support label search, full\-text search, and vector search capabilities, ideally with a single engine supporting all three methods.


<span id="2f4a33b2"></span>
## Current solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55babd54cd604ce7acd0b8f8b8e55a25~tplv-goo7wpa0wc-image.image) </span>

In the current solution, image data is generally stored separately in object storage, while label and text data are stored in the database.

Data for full\-text indexing is generally stored in ES, and vector data is typically stored in a dedicated vector database.

ES can perform label search and full\-text search, while the vector database handles vector search and label search.

If three\-way retrieval is required, both ES and the vector database must be queried simultaneously.

<span id="852b14b6"></span>
## Lance solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e49469cad318413c8d3c0f55d4f3ee2a~tplv-goo7wpa0wc-image.image) </span>

Multimodal data and labels are stored together in the Lance dataset. Full\-text indexes are built directly on the text fields in Lance. Vector fields can also be stored directly in Lance, and multiple vector indexing algorithms are available, enabling fast vector search.

<span id="848c6d1f"></span>
## Solution comparison


|**Dimension** |**Current solution** |**Lance solution** |
|---|---|---|
|Data cost |* Indexes are stored using ES or vector databases, which are more suited for real\-time scenarios and result in very high storage costs. |* All data is stored in the lake, with data stored on object storage, resulting in relatively low costs. |
|Data processing |* Indexes use ES and VectorDB, typically accessed via their own SDKs, with distributed capabilities built into the engine.<br><br>* Data is accessed using the object storage SDK. |* A unified SDK is used for access, supporting both the pylance standalone SDK and distributed frameworks such as spark and ray. |
|Scalability |* Using a data warehouse architecture, scalability is prone to bottlenecks. |* Using a data lake architecture enables greater scalability. |
|Usability |* Multiple copies of data require handling data consistency across multiple systems.<br><br>* Data and metadata are separated, requiring additional processing when operating on data. |* All data is maintained in a single Lance dataset, enabling minimal maintenance. |
