---
title: "Create Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Create_Collection"
---

<span id="creating-a-collection"></span>
# Creating a collection

This topic describes how to create a collection to which data can be written.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can add only one vector field to each collection. If a collection already has a vector field, you cannot select the vector type for new fields.</div>


* <div data-tips="true" data-tips-type="tip">A maximum of 200 fields can be added for a collection.</div>



<span id="71bd29dc"></span>
# Procedure


1. Click **Collections** in the left navigation pane. On the page that appears, click **Create collection**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae54af2d91914904a25420604d0acc9c~tplv-goo7wpa0wc-image.image) </span>


2. Select **Vectorize data** or **Existing vector data** to start creating a collection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a841784f5124a21986ac568b62fdb9e~tplv-goo7wpa0wc-image.image) </span>


3. On the **Create collection** page, configure related parameters.


++Vectorize data ++

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a8a75c9a2aa4be4b3add729eccebd50~tplv-goo7wpa0wc-image.image) </span>

<ins>Existing vector data</ins>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca5248882bf54a21957a087a4d95e620~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Description** |
|---|---|
|Name |The name of the collection. **This parameter is required**.<br><br><br>* The name can contain letters, digits, and underscores (_). It must start with a letter.<br><br>* The name must be 1 to 128 characters in length.<br><br>* The name must be unique. |
|||
|||
|||
|Alias |The alias of the collection. **This parameter is optional.** <br><br><br>* Multiple aliases are allowed. Separate the aliases with carriage returns.<br><br>* Each alias of the same collection must be unique.<br><br>* If an alias has been mapped to an existing collection, it will be mapped to the current collection after the setting takes effect, and the mapping between the alias and the original collection will be canceled.<br><br>* The alias must be 1 to 128 characters in length. |
|||
|||
|||
|||
|Description |The description of the collection. **This parameter is optional**.<br><br><br>* The description can be up to 500 characters in length. |
|||
|Vector information |If you selected **Create a vector** before collection creation, you need to specify vector model information and configure vector fields. If you selected **Import an existing vector**, directly configure vector fields.<br><br><br>* Scenario: **Required** if you selected **Create a vector**. Valid values: Text and Multi\-modal.<br><br>* Dense vector: **Required**. Subparameters include vector dimension, field name, and vector model.<br><br>* Sparse vector: **Optional**. Subparameters include field name and vector model.<br><br>* Vector model: **Required** if you selected **Create a vector**.<br><br>* Vector dimension:<br><br>   * If you selected Import an existing vector, the dimension for a dense vector is required and must be a number. **This parameter is required**.<br><br>   * Valid values: multiples of 4 within [4, 4096].<br><br>   * No dimension is available for sparse vectors.<br><br>* Field name:<br><br>   * The name must be unique and begin with a letter. It can contain only letters, digits, and underscores (_) and must be 1 to 128 characters in length. The parameter cannot be empty. **This parameter is required**.<br><br>   * If you selected **Create a vector**, this value is the name of the vector field, which stores data vectorized by the corresponding model. The dense and sparse vector fields can share the same name, in which case the same source field is vectorized for both.<br><br>   * The value is the field name if you selected **Import an existing vector**. The field stores vector data. The dense and sparse vector fields must have different names, which means the vectorized data is stored in different fields. |
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|Fields |Other fields: Click **Add** to define new fields. **This parameter is optional.** <br><br><br>* Field name: The name must be unique and begin with a letter. It can contain only letters, digits, and underscores (_) and must be 1 to 128 characters in length. The parameter cannot be empty. **This parameter is required**.<br><br>* Field type: Select a type from the drop\-down list. The options are string, bool, list, int64, float3, text, and image. **This parameter is required**.<br><br>* Default value:<br><br>   * A default value can be specified when the field type is not text or image. The value, which defaults to \-\-, must begin with a letter and can contain only letters, digits, and underscores (_). **This parameter is required**.<br><br>* Delete icon: You can click this icon to delete a field. |
|||
|||
|||
|||
|||
|Primary key |* The primary key is used to uniquely identify a row of data. The primary key must be unique. Otherwise, the existing record with that primary key is updated.<br><br>* The primary key can be generated automatically. Alternatively, you can select a field of the string or int64 type from **Other fields** as the primary key.  **(Default)**  |
|||


> When using embedding models to create vectorized data, your uploaded data may be transmitted to BytePlus servers in Malaysia for processing. BytePlus does not store your data, including any processed data, on our servers in Malaysia.


1. Click **Create Collection** in the right corner after you have configured all required parameters. A message is displayed, indicating that the collection has been created.

2. After the collection is successfully created, a dialog box appears. You can choose to create an index for the new collection or write data to it. If you have a large amount of data, it is recommended that you write the data first.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a3ae7c2b18d4e8e9ea16a5634a1cdac~tplv-goo7wpa0wc-image.image) </span>

In the **Write data** dialog box that appears, select a writing method. The SDK integration guide corresponding to the selected writing method is displayed.

**Online synchronous writing** applies to scenarios where online service data is written to the database in real time. This method provides stream\-writing APIs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ee3e690e9364d06aa7b5c6d5a6e6f20~tplv-goo7wpa0wc-image.image) </span>
