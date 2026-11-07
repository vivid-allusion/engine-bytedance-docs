---
title: "Specify scalar filters in retrieval"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Specify_scalar_filters_in_retrieval"
---

<span id="specify-scalar-filters-in-retrieval"></span>
# Specify scalar filters in retrieval

This topic describes how to test the hybrid retrieval feature. You can configure **Search vector**, **Limit (Top\-k)** , **Subindex**, and **Scalar field** to view the retrieval result.

In hybrid retrieval, vector retrieval is performed to search for similar vectors, while scalar retrieval is performed to filter the retrieved vectors by scalar values.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A retrieval test is supported when the execution status of the index is <strong>Ready</strong>. You cannot perform a retrieval test when the execution status of the index is <strong>Initializing</strong> or <strong>Failed</strong>.</div>


* <div data-tips="true" data-tips-type="warning">If you configure the <strong>Scalar field</strong> parameter, hybrid retrieval will be performed. Otherwise, vector retrieval will be performed. In this topic, this parameter is configured.</div>


* <div data-tips="true" data-tips-type="warning">If you configure the <strong>Search vector</strong> parameter, the system retrieves K vectors similar to the input vector. If you do not configure the <strong>Search vector</strong> parameter, the system retrieves K vectors similar to a zero vector [0,0,0,0......] by default.</div>



<span id="0902ac3c"></span>
# Procedure


1. Go to the **Retrieval test** tab using any of the following methods:

   1. Method 1: On the left navigation pane, click **Indexes** to open the **Indexes** page. Find the target index in the list and click **Retrieval test** in the **Actions** column.

   2. Method 2: On the left navigation pane, click **Indexes** to open the **Indexes** page. Find the target index in the list and click its name to go to the basic information tab of the index. Then, click the **Retrieval test** tab.

2. On the **Retrieval test** tab, configure the **Search vector**, **Limit (Top\-k)** , **Subindex**, and **Scalar field** parameters.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b9e6e0ea8bc4e4cbf80600188670dea~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Description** |
|---|---|
|Search vector |You can enter a string of JSON arrays in the text box. The dimension count was specified when you created the collection. This parameter is **optional**.<br><br><br>* If you configure the **Search vector** parameter, the system retrieves K vectors similar to the input vector.<br><br>* If you do not configure the **Search vector** parameter, the system retrieves K vectors similar to a zero vector [0,0,0,0......] by default. |
|||
|||
|Limit (Top\-k) |You can enter the top\-k value to specify the number of returned results. The default value is 100. This parameter is **required**. |
|Subindex |You can select a subindex from the dropdown list. A subindex is the field value corresponding to the field name that you selected from the **Subindex partitioning field** dropdown list on the **Create index** page. This parameter is **required**.<br><br><br>* If you do not specify the **subindex partitioning field**, the default subindex is used.<br><br>* Use this parameter when you want to divide a collection into multiple partitions and search for data within a certain partition or subindex. For example, you can divide a collection into subindexes by country ID and then search for data by a specific subindex without needing to set filters. This way, search performance can be improved. |
|||
|||
|Scalar field |You must specify scalar filter conditions for hybrid retrieval.<br><br><br>* If you did not specify the **Scalar field** parameter when creating the index on the **Create index** page, search results are not filtered, and no field is available in the **Scalar field** dropdown list in the retrieval test stage.<br><br>* If you specified the **Scalar field** parameter when creating the index on the **Create index** page, you can now select a scalar field from the **Scalar field** dropdown list, and specify the filter condition.<br><br>* The following **filter conditions** are supported: inclusion, exclusion, greater than, less than, greater than or equal to, and less than or equal to. The following **logical operators** are supported: AND and OR. |
|||
|||
|||



3. Click **Search** in the lower\-left corner to view the search results. By default, retrieved vectors are sorted by score in ascending order.
