---
title: "Retrieve vectors"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Retrieve_vectors"
---

<span id="retrieve-vectors"></span>
# Retrieve vectors

This topic describes how to test the vector retrieval feature. You can configure **Search vector**, **Limit (Top\-k)** , and **Subindex** to view the retrieval result.

The vector retrieval feature retrieves vectors by calculating the similarity between vectors based on a vector space model. Vector retrieval can efficiently retrieve K vectors in a given vector collection that are similar to the target vector by building a more time\- and space\-efficient data structure based on a measurement such as inner product and Euclidean distance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A retrieval test is supported when the execution status of the index is <strong>Ready</strong>. You cannot perform a retrieval test when the execution status of the index is <strong>Initializing</strong> or <strong>Failed</strong>.</div>


* <div data-tips="true" data-tips-type="warning">If you configure the <strong>Scalar field</strong> parameter, hybrid retrieval will be performed. Otherwise, vector retrieval will be performed.</div>


* <div data-tips="true" data-tips-type="warning">If you configure the <strong>Search vector</strong> parameter, the system retrieves K vectors similar to the input vector. If you do not configure the <strong>Search vector</strong> parameter, the system retrieves K vectors similar to a zero vector [0,0,0,0......] by default. For a hybrid index, if you do not configure the search vector parameter, the system retrieves both dense and sparse vectors similar to a zero vector.</div>



<span id="f0756aed"></span>
# Procedure


1. Go to the **Retrieval test** tab using any of the following methods:

   1. Method 1: On the left navigation pane, click **Indexes** to open the **Indexes** page. Find the target index in the list and click **Retrieval test** in the **Actions** column.

   2. Method 2: On the left navigation pane, click **Indexes** to open the **Indexes** page. Find the target index in the list and click its name to go to the basic information tab of the index. Then, click the **Retrieval test** tab.

2. On the **Retrieval test** tab, configure the **Search vector**, **Limit (Top\-k)** , and **Subindex** parameters. For a hybrid index that contains both dense and sparse vectors, the dense_weight parameter is provided to control the weight of the dense vectors in hybrid retrieval, and you need to enter both dense and sparse vectors for retrieval. If the index corresponds to a collection associated with an embedding model, you can input text or image\-text pairs in the text boxes for end\-to\-end text retrieval.


The following figure displays the configuration for **a retrieval test with a hybrid index**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80b5cbbf4f114040ab73a6ce0807e8b2~tplv-goo7wpa0wc-image.image) </span>

The following figure displays the configuration for **a retrieval test with dense vectors only**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92a689557f7e4ac9a5d8ea1c47aead47~tplv-goo7wpa0wc-image.image) </span>

The following figure displays the configuration for **a text retrieval test**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5605de697674221923b98e0f3f009ce~tplv-goo7wpa0wc-image.image) </span>

The following figure displays the configuration for **a multimodal retrieval test**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae65387c3bde470ba15541d12dbbcdaa~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Description** |
|---|---|
|Search vector |You can enter a string representing a JSON array in the text box. The dimension count was specified when you created the collection. This parameter applies to collections that contain vector data, and is **optional**.<br><br><br>* If you configure the **Search vector** parameter, the system retrieves K vectors similar to the input vector.<br><br>* If you do not configure the **Search vector** parameter, the system retrieves K vectors similar to a zero vector [0,0,0,0......] by default.<br><br>* For a hybrid index, you need to enter equal numbers of dense and sparse vectors. Dense and sparse vectors with the same subscript represent the same object. |
|||
|||
|||
|Search text |You can enter plain text for retrieval. This parameter applies to a collection that contains data to be vectorized and for which you have selected the Text scenario. |
|Search text/image |You can input **plain text**, **images**, or **text and images** for retrieval. This parameter applies to a collection that contains data to be vectorized and for which you have selected the Multimodal scenario. |
|Limit (Top\-k) |You can enter the top\-k value to specify the number of results to return. The default value is 100. This parameter is **required**. |
|dense_weight |* This parameter is displayed only for an **HNSW_Hybrid** index. It specifies the weight of the dense vectors in hybrid retrieval. The value range is [0.2, 1].<br><br>* As the value approaches 1, the system prioritizes semantic retrieval, and as the value approaches 0, the system prioritizes keyword retrieval. |
|||
|Subindex |You can select a subindex from the dropdown list. A subindex is the field value corresponding to the field name that you selected from the **Subindex partitioning field** dropdown list on the **Create index** page. This parameter is **required**.<br><br><br>* If you do not specify the **subindex partitioning field**, the default subindex is used.<br><br>* Use this parameter when you want to divide a collection into multiple partitions and search for data within a certain partition or subindex. For example, you can divide a collection into subindexes by country ID and then search for data by a specific subindex without needing to set filters. This way, search performance can be improved. |
|||
|||
|Scalar field |You can specify scalar filter conditions. For more information, refer to [Specify scalar filters in retrieval](https://docs.byteplus.com/en/docs/VikingDB/Specify_scalar_filters_in_retrieval). |



3. Click **Search** in the lower\-left corner to view the search results.
