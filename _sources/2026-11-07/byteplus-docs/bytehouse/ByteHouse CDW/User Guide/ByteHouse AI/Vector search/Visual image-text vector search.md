---
title: "Visual image-text vector search"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/visual-image-text-vector-search"
---

ByteHouse Cloud Data Warehouse supports visual image\-text vector search. This tutorial describes how to use the image\-text vector visual search feature in the ByteHouse Cloud Data Warehouse console.

<span id="a0720148"></span>
# Background information

The image\-text vector visual search feature supports multimodal vector search for text, images, and mixed image\-text data. By converting text or images into vectors and calculating similarity, it enables efficient retrieval. This feature provides a visual operation interface, supporting the creation, management, and retrieval testing of search objects. It is suitable for scenarios in various fields such as financial compliance, e\-commerce recommendation, intelligent driving, and gaming, where efficient retrieval of unstructured data is required. It significantly improves retrieval efficiency and adapts to complex business requirements.

In addition to performing vector search through the console, ByteHouse Cloud Data Warehouse also supports writing and retrieving image\-text vectors via SQL and Python scripts. For detailed operations, see the following documentation:


* [Perform vector search using SQL](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL)

* [Perform vector search using Python API](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-python-api)


<span id="b718e1ad"></span>
# Usage restrictions


* This feature is in Beta. Please submit a ticket or contact the ByteHouse team to obtain allowlist access.

* Please ensure that the ByteHouse engine you are using is version v2.3.3 or above. You can log in to the ByteHouse Cloud Data Warehouse Edition console, click the top **Tenant management**, and view your engine version on the **Basic information** page.


<span id="2b74f4a2"></span>
# Preparation


* Enable the vector search feature. For details, see [Enable vector search](https://docs.byteplus.com/docs/bytehouse/vector-retrieval).

* Create a vector table. For operation details, see [Perform vector search using SQL](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL).


<span id="53850ed5"></span>
# Steps


1. Create a search object. In the ByteHouse Cloud Data Warehouse console, click the top **Data Query**, then click **Create search object** to create the target object for vector search.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7058687d106c43baa62bcb850fd91ab6~tplv-goo7wpa0wc-image.image) </span>

2. On the create search object page, enter the basic information and select the search configuration.

   1. Enter basic information. You can customize the search name and description to facilitate subsequent management.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09391ebf4bee4cc6ade25f2998951496~tplv-goo7wpa0wc-image.image) </span>

   2. Select the search configuration.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/684b582508fd447e8d79f46906b981c0~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Description |
      |---|---|
      |Search field |Select the database, table, and field to be searched from the dropdown list to specify the target data object for vector search. |
      |Vector model |Select the vector model to use for the search from the dropdown list. Currently, ByteHouse supports the doubao\-embedding\-vision model. This model is designed for scenarios involving multimodal content vector search, such as text, images, and videos. It supports both Chinese and English text, with a maximum input of 128K. |
      |Virtual warehouse |Select the virtual warehouse to execute the vector search and specify the compute resources for vector search. |
      |Filter field |Set as a basic field in the data table that can be used as a filter criterion. |
      

   After creation, the search object will be displayed in the list, where you can perform subsequent operations such as search testing, editing, or deletion.

3. Click the **Query test** button in the row of the search object, and configure the search parameters on the search test page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b928d96be6254fdaae1276f89df7c65f~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Description |
   |---|---|
   |Search type |Supports three search methods: text search, image search, and text + image search.<br><br><br>* **Text search**: Supports plain text input (up to 500 characters) and pasting text.<br><br>* **Image search**: Images support JPG, PNG, and WEBP formats, and must not exceed 10 MB in size.<br><br>* **Text** + **Image search**: Supports inputting both text and image simultaneously. |
   |Number of results (TOP K) |The maximum number of rows displayed in the search results. The parameter can be set in the range of 1 to 200. |
   |Similarity score |Used to control search latency and accuracy. The parameter can be set in the range of 1 to 100.<br><br>Increasing the parameter value will improve the recall rate but will relatively reduce search performance: the lower the score, the more results are recalled, but the search accuracy is lower; the higher the score, the more precise the recall, but fewer results are returned. |
   |Result display fields |Fields displayed in the search results; by default, the first five fields of the data table are shown. |
   |Search filtering |Configure search filter criteria to further narrow the result range based on vector search and improve query accuracy.<br><br><br>1. From the dropdown list, select the scalar filter field that was set when creating the search object.<br><br>2. Select the filter rule, which can be set to "Include" or "Exclude", and enter the corresponding keywords in the input box.<br><br>3. (Optional) To set multiple filter criteria, click **Add** to add a new condition row, and configure the relationship between multiple conditions by clicking the "And" or "Or" button in front of each filter configuration.<br><br><br>After executing the search, the system will return results based on the filter criteria. |
   

4. After configuring the search, click **Query**. ByteHouse will display the results that meet your criteria on the right side of the search results page according to your settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/237ee8f956a045ba977336428ce1d554~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) After creation, you can click the **Edit** button in the row of the search object in the search object list to edit the description, virtual warehouse, and filter fields of the search object.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17dc0a7ad5684be18216da922c55aa23~tplv-goo7wpa0wc-image.image) </span>

6. (Optional) If you no longer need the search object, you can click the **Delete** button in the row of the search object in the search object list to delete the search object.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c622b1f75ce45329afbc514ff46f51b~tplv-goo7wpa0wc-image.image) </span>
