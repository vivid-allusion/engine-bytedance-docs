---
title: "Create a custom model"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_a_custom_model"
---

ContextSearch includes common models by default and supports creating custom models. This topic describes how to create a custom model.

<span id="MJQRAq9f"></span>
## Prerequisites

You need to prepare the model file before creating a custom model. You can store the model file in a TOS bucket in advance or upload a local model file directly when creating the custom model.

<span id="jyFdzPXj"></span>
## Notice

Reading model files from a TOS bucket requires the current account to have read permission for the bucket, at least GetObject permission. Uploading a local model file stores it in a specified TOS bucket, requiring the current account to have write permission for the bucket, at least PutObject permission.

<span id="jyFdzPXj"></span>
## Create model


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. On the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> Model and reasoning \> Model management**, click the **Custom model** tab, then click **Create model**.

4. In the **Create model** panel, configure the following parameters, then click **OK**.



|**Parameter** |**Description** |
|---|---|
|Affiliated project |Project the model belongs to. Cannot switch when creating a model. To switch, close the panel and modify it from the top navigation bar. |
|Model name |Customize the model name.<br><br><br>* First character only supports letters or underscores (_).<br><br>* Can include letters, digits, and special characters: only English periods (.), underscores (_), hyphens (\-), and slashes (/) are supported, length between 1 and 128 characters.<br><br>* Can contain at most one slash (/) character. |
|Model type |Select model type.<br><br><br>* Text ** ** Embedding: a method that converts text into numeric vectors understandable by computers, capturing the semantic information of the text.<br><br>* Rerank: a technique to reorder search results based on relevance, placing the most relevant results first so users can quickly find the information they need.<br><br>* Image Embedding: converts images into low\-dimensional vector representations for processing, analysis, and comparison in various machine learning tasks.<br><br>* Sparse Embedding: a technique for handling high\-dimensional sparse data by mapping sparse features to a low\-dimensional space, saving storage space and improving computing efficiency.<br><br>* Multi\-Modal Embedding: a vectorization technology supporting text, image, and mixed text\-image inputs, suitable for text\-to\-image, image\-to\-image, and mixed search scenarios.<br><br>* Custom: Combining OpenSearch's hybrid retrieve with large model generation results yields results with more semantic coherence and information accuracy.<br><br>* ASR: Converts audio to text with very high accuracy, supporting multi\-language and multi\-dialect speech recognition, suitable for meeting transcriptions, video subtitles, content review, and quality inspection. |
|Model description (optional) |Set the model description, with a maximum length of 256 characters. |
|Model file |Choose how to configure the model file.<br><br><br>* Object Storage file: select the target folder in the Object Storage bucket, indicating the model file has been saved in the bucket in advance.<br><br>* Upload local files: select model files or folders locally, then upload them to the target folder in the Object Storage Bucket. When uploading files, only model files named `model.zip` are supported, with a size limit of 2 GiB.<br><br><br>Notice<br><br><br>* If the current account lacks read permission for the corresponding bucket (at least GetObject permission), it cannot access the file list in the bucket.<br><br>* If the current account lacks write permission for the corresponding bucket (at least PutObject permission), it cannot store model files in the Object Storage Bucket.<br><br><br>Ensure the current account has read and write permissions for the TOS bucket. |
|Select bucket |Select an object storage bucket to store model files from the dropdown list. If no available TOS bucket exists, click **Create bucket** to go to the object storage console and create one. |
|Object Storage Folder |Location to store model files, either to read model files from this folder or to upload local model files to this folder. |
|Select file |Select **File** or **Folder**. This parameter is only visible when **Model file** is set to **Upload local files**. |
|Upload |Click the upload area to select files or folders to upload, or drag files or folders to the upload area. |
