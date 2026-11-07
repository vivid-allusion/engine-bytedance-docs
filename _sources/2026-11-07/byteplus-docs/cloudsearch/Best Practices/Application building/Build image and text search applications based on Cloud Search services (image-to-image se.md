---
title: "Build image and text search applications based on Cloud Search services (image-to-image search, text-to-image search)"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/text-based-image-search"
---

Cloud Search’s AI search supports creating Image Embedding models, which convert images into low\-dimensional vector representations for processing, analyzing, and comparing across various machine learning tasks. This article explains how to quickly build an image\-text retrieval application based on the Cloud Search Image Embedding model, supporting both image\-to\-image and text\-to\-image searches.

<span id="3cca81b0"></span>
## Background

Image\-text retrieval is widely used in popular fields such as e\-commerce, advertising, design, and search engines. Common image\-text retrieval includes image\-to\-image and text\-to\-image search, allowing users to quickly find identical or similar images from large image libraries by inputting text descriptions or uploading pictures.

The input text description and picture serve as retrieval targets; features are extracted separately from images and text, the model establishes the correlation between them, and then vector search is conducted over a large image database to return the most relevant result set. The feature extraction part uses the CLIP model, and vector retrieval uses the BytePlus Cloud Search service for fast search among massive image features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd71aa9beecc4a9c9e088b2ed34ff7fe~tplv-goo7wpa0wc-image.image) </span>

<span id="66110490"></span>
## Precautions

AI search is only supported on OpenSearch version 2.9.0 instances or later. How to create an OpenSearch instance. For more information, see [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2).

<span id="7JkcaXEL"></span>
## Prerequisites


* A TOS bucket and folder for storing pictures have been created. In this example, the bucket name is `doc-test`, the Endpoint domain node is `tos-cn-beijing.ivolces.com`, and the image storage path is `picture/image_temp`. For details, see [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [Create a folder](https://docs.byteplus.com/en/docs/tos/docs-creating-a-folder).

* The opensearch\-remote\-inference plugin has been installed. For details, see [Manage system built-in plugins](https://docs.byteplus.com/en/docs/cloudsearch/manage-built-in-plugins).


<span id="5d709025"></span>
## Deploy the text and image retrieval application

<span id="18373791"></span>
### Create an AI search service

After creating an OpenSearch instance, you can create AI search within the instance for subsequent model creation and deployment.

For instructions on creating AI search, see [Create AI search](https://docs.byteplus.com/docs/cloudsearch/Create_an_AI_search_service).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">CPU and GPU resource types are currently supported; this article chooses to use the CPU resource type. For details on each parameter, see <a href="https://docs.byteplus.com/docs/cloudsearch/Create_an_AI_search_service">Create AI search</a>.</div>


* <div data-tips="true" data-tips-type="tip">When using the CPU resource type, it is recommended to select a <code>1:4</code> resource ratio to ensure better performance of the model service application.</div>



<span id="b1622187"></span>
### Create and start the model

You can create an Image Embedding model in AI search. The Image Embedding model types support CLIP, ChineseCLIP, and their derivatives, which you can download and upload yourself.


1. Upload the Image Embedding model file to the TOS Bucket.

   1. Download the model file.

   2. Log in to the [TOS console](https://console.byteplus.com/tos) and upload the file to the bucket.

      Assume the full storage path of the model file is `tos://doc-test/ImageEmbedding/`. For detailed steps, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [Uploading objects](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).Create bucketUpload fileUpload file

2. Create model.

   1. Log in to the [Cloud Search Console](https://console.byteplus.com/es), select **AI Search** in the left navigation bar, then find and click the target service name.

   2. In the left navigation bar, select **Model management**, then choose the **My model** tab, and click **Create model**.

   3. Select to create an **Image Embedding** model, set the related model parameters, then click **OK**.

      
      |**Parameter** |**Description** |
      |---|---|
      |Model name |Customize the model name, for example, `ImageSearch-Demo`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Image Embedding model has the following two capabilities:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It supports vectorizing images and text directly and returns the vectorization results. To learn how to obtain vectorization, see <a href="https://docs.byteplus.com/docs/6465/1337864">Calling the embedding model</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Proxy OpenSearch to perform vectorization and writing operations simultaneously using a similar OpenSearch interface.</div><br> |
      |Model type |Select to create an **Image Embedding** model. |
      | Select bucket |Select an object storage bucket to store model files from the dropdown list. |
      |Model file |Select a **TOS object** to choose the model file from the specified object storage bucket. You must also set the **TOS folder** to read the existing model file from this folder. |
      |Description |set the model's description statement. |
      

3. Create and start an inference service.

   You can create an inference service, associate it with the newly built Image Embedding model, and configure network, resources, and user\-defined parameters based on business needs.

   1. Select **Inference service** in the left navigation bar, then click **Create inference service**.

   2. In the **Create inference service** panel, configure the inference service parameters, then click **OK**.

      
      |**Configuration** |**Description** |
      |---|---|
      |Service name |customize the inference service name, for example, `image-search`.<br><br><br>* First character only supports letters or underscores (_).<br><br>* Can include letters, digits, and special characters: only English periods (.), underscores (_), hyphens (\-), and backslashes (/) are supported, with a length of 1 to 128 characters.<br><br>* Can contain at most one backslash (/) character. |
      |Select model |Select the newly created Image Embedding model from the dropdown list. |
      |Availability zone |Select the availability zone where you want to deploy the inference service.<br><br><br>* If the OpenSearch instance is single availability zone, your inference service will only have one availability zone.<br><br>* If you require multi\-availability zone deployment for the inference service, ensure the OpenSearch instance has multiple availability zones. For how to add availability zones to the instance, see [Add availability zone](https://docs.byteplus.com/docs/cloudsearch/add-availability-zone). |
      |Enable high availability |High availability is supported when deploying inference services in a single availability zone.<br><br>Inference services with high availability require at least 2 nodes. |
      |Resource type |select the resource type used by the inference service from the dropdown list; you can choose between CPU and GPU resource types.<br><br>if the required resource type is not enabled or the specification is too low, choose to change the specification of AI Search first. For more information, see [Modify AI search](https://docs.byteplus.com/docs/cloudsearch/Modify_AI_search). |
      |Specification |Select specification from the dropdown list. |
      |Number of nodes |Set the number of nodes for the inference service.<br><br><br>* single availability zone deployment with high availability disabled: the number of nodes can be set from 1 to 512.<br><br>* single availability zone deployment with high availability enabled: the number of nodes must be a multiple of 2, with a maximum of 512.<br><br>* multi\-availability zone deployment: the number of nodes must be a multiple of the number of availability zones, with a maximum of 512. for example, if there are 2 availability zones, the number of nodes must be a multiple of 2. |
      |Network configuration |Enable private network access.<br><br>When enabled, the system assigns a private network access address to the models associated with the inference service, allowing clients within the same VPC environment as AI Search to access the associated models. |
      |Description |Customize the description of the inference service. |
      |Advanced Options |Configure custom parameters for the inference service, with `UserConfig` and `MaxReplicasPerNode` provided by default.<br><br>This article is related to the Image Embedding model and does not require input. |
      

4. Start the inference service.

   1. After creating the inference service, click **Start** in the actions column.

   2. In the pop\-up dialog box, click **OK**.

5. Obtain Image Embedding model call information.

   After starting the inference service, click **View call information** on the inference service details page, then get the model's call information.


<span id="abad89bc"></span>
### create ingest pipeline

To create an ingest pipeline, specify the Image Embedding model to use, which converts the designated field (picture information) into a vector and embeds it back.


1. Log in to the visualization tool and open the command line.

   1. Log in to the visualization tool. Log in to the visualization tool using the public access address. See [Public network access to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool#3cbdb7b4).

   2. Select **Management \> Dev Tools** from the left navigation bar.

2. Execute the following command to create an ingest pipeline with the ID `image_remote_embedding`.

   When creating the ingest pipeline, complete the following information:

   * `url`: Set this to the `URL` obtained from the model service's **call information**.

   * `model`: Set this to the `model` obtained from the model service's **call information**, such as `ImageSearch-Demo`.

   * `"vector_source_image": "vector"`: the `vector_source_image` field in the index indicates the TOS Bucket storage path of the picture. This configuration means converting the `vector_source_image` field into vector storage in `vector`.

   ```HTTP
   PUT _ingest/pipeline/image_remote_embedding
   {
       "description": "image embedding pipeline for remote inference",
       "processors":
       [
           {
               "remote_text_embedding":
               {
                   "remote_config":
                   {
                       "method": "POST",
                       "url": "http://d-182800***-serve-svc.r-00g**:8000/v1/embeddings",
                       "params":
                       {},
                       "headers":
                       {
                           "Content-Type": "application/json"
                       },
                       "advance_request_body":
                       {
                           "model": "ImageSearch-Demo"
                       }
                   }
                   ,
              "field_map":{
             "vector_source_image": "vector"
             }
               }
           }
       ]
   }
   ```
   


<span id="b33d413d"></span>
### create search pipeline

create a search pipeline by specifying the Image Embedding model to use.


1. log in to the visualization tool and open the command line.

   1. log in to the visualization tool. Log in to the visualization tool using the public access address. See [Public network access to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool#3cbdb7b4).

   2. Select **Management \> Dev Tools** in the left navigation bar.

2. execute the following command to create a search pipeline with ID `image_remote_embedding_search_pipeline`.

   when creating a search pipeline, fill in the following information:

   * `url`: set to the model's `url` obtained from the model service’s **call information**.

   * `model`: set the `model` obtained from the **call information** of the model service, such as `ImageSearch-Demo`.

   ```HTTP
   PUT _search/pipeline/image_remote_embedding_search_pipeline
   {
     "description": "image embedding pipeline for remote inference",
     "request_processors": [
       {
         "remote_embedding": {
            "remote_config":
                   {
                       "method": "POST",
                       "url": "http://d-1828002***-serve-svc.r-00g***:8000/v1/embeddings",
                       "params":
                       {},
                       "headers":
                       {
                           "Content-Type": "application/json"
                       },
                       "advance_request_body":
                       {
                           "model": "ImageSearch-Demo"
                       }
                   }
         }
       }
     ]
   }
   ```
   


<span id="c65fa2f0"></span>
### Create index

After the OpenSearch instance is created, you can create an index in the instance to store vector information of pictures.


1. Log in to the visualization tool and enter the command line.

   1. Log in to the visualization tool. Log in to the visualization tool using the public access address. See [Public network access to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool#3cbdb7b4).

   2. Select **Management \> Dev Tools** in the left navigation bar.

2. Execute the following command to create an index named `image_search`.

   * When creating the index, specify the default pipeline `default_pipeline` as the new Ingest Pipeline with the ID `image_remote_embedding`.

   * `id`: the ID field of the picture, which can be understood as the picture name or ID and serves as an identifier.

   * `vector_source_image`: indicates the storage path of the picture on the TOS Bucket, where the specific image can be accessed.

   * `vector`: represents the embedding vector field generated from the image. Set `vector` to `knn_vector`, and the `dimension` must match the model's dimension, for example, `512`.

   ```HTTP
   PUT imagesearch
   {
     "settings": {
       "default_pipeline": "image_remote_embedding", 
       "index": {
         "refresh_interval": "60s",
         "number_of_shards": "3",
         "knn.space_type": "cosinesimil",
         "knn": "true",
         "number_of_replicas": "1"
       }
     },
       "mappings": {
         "properties": {
           "id": {
             "type": "text"
           },
            "vector_source_image": {
              "type": "text"
           },
           "vector": {
            "type": "knn_vector",
            "dimension": 512,
            "method": {
             "name": "hnsw",
             "engine": "nmslib",
             "space_type": "cosinesimil"
           }
           }
         }
       }
   }
   ```
   


<span id="78b28e93"></span>
## Verify results

<span id="a14ee794"></span>
### Write image data

After creating the index in the instance, you can write images from the TOS Bucket into the index.


1. Log in to the visualization tool and open the command line.

   1. Log in to the visualization tool. Log in to the visualization tool using the public access address. See [Public network access to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool#3cbdb7b4).

   2. Select **Management \> Dev Tools** from the left navigation bar.

2. Execute the following command to write images from the TOS Bucket into the `imagesearch` index.

   * id: User\-defined ID field for images, which can directly use the image name as an identifier.

   * vector_source_image: Enter the storage path of the image in the TOS Bucket.

   ```HTTP
   POST _bulk
   { "index" : { "_index" : "imagesearch" } }
   { "id": "0a655b1f2c18632a534796bbf46a4ff7", "vector_source_image" : "tos://doc-test/picture/image_temp/0a655b1f2c18632a534796bbf46a4ff7.jpg" }
   { "index" : { "_index" : "imagesearch" } }
   { "id": "0a6854edd10ed7bf0aea33f49f6bf340", "vector_source_image" : "tos://doc-test/picture/image_temp/0a6854edd10ed7bf0aea33f49f6bf340.jpg" }
   { "index" : { "_index" : "imagesearch" } }
   { "id": "0ad4ea74a741352eb24dd12b1a3becfc", "vector_source_image" : "tos://doc-test/picture/image_temp/0ad4ea74a741352eb24dd12b1a3becfc.jpg" }
   { "index" : { "_index" : "imagesearch" } }
   { "id": "0ae481e0fba3fefae791a32f0432580a", "vector_source_image" : "tos://doc-test/picture/image_temp/0ae481e0fba3fefae791a32f0432580a.jpg" }
   { "index" : { "_index" : "imagesearch" } }
   { "id": "0b11ced2ae68745b38e5fd252c11384f", "vector_source_image" : "tos://doc-test/picture/image_temp/0b11ced2ae68745b38e5fd252c11384f.jpg" }
   ```
   

3. (Optional) After writing the image, you can check through the query interface whether the image data has been successfully written.

   ```HTTP
   POST imagesearch/_search
   {
     "query": {
       "match_all": {}
     }
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40fd2302fc8c4b17b5c8214e889abad6~tplv-goo7wpa0wc-image.image) </span>


<span id="55508fa5"></span>
### Text\-to\-image search

After completing the construction of the text and image retrieval application and writing the image data, you can perform text\-to\-image search and image\-to\-image search. In **Dev Tools**, execute the following command to query images by search keywords.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Differ text\-to\-image search and image\-to\-image search by entering different information in <code>query_text</code>.</div>



* <div data-tips="true" data-tips-type="tip">Enter search keywords to perform text\-to\-image search, for example, <code>White T-shirt</code>.</div>


* <div data-tips="true" data-tips-type="tip">Enter the image storage path in TOS for image\-to\-image search, for example, <code>tos://doc-test/picture/image_temp/aaa.jpg</code>.</div>


* <div data-tips="true" data-tips-type="tip">Enter the image base64 encoding for image\-to\-image search, for example, <code>data:image/jpeg;base64,iVBORw0KGgoAAAANSUhEUgA....</code>.</div>



```Shell
POST imagesearch/_search?search_pipeline=image_remote_embedding_search_pipeline
{
  "query": {
    "bool": {
      "must": [
        {
          "remote_neural": {
            "vector": {
              "query_text": "White T-shirt",
              "k": 1
            }
          }
        }
      ]
    }
  }
}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a26bd995c2d44a2b2919b728bcdfcd1~tplv-goo7wpa0wc-image.image) </span>

<span id="e405a85e"></span>
### Image\-to\-image search

After completing the construction of the image and text retrieval application and writing the image data, you can perform text\-to\-image and image\-to\-image searches. In **Dev Tools**, run the following command to query images based on the input image information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Distinguish between text\-to\-image and image\-to\-image searches by entering different information in <code>query_text</code>.</div>



* <div data-tips="true" data-tips-type="tip">Enter the TOS storage path of the image to perform image\-to\-image search, for example <code>tos://doc-test/picture/image_temp/aaa.jpg</code>.</div>


* <div data-tips="true" data-tips-type="tip">Enter the base64 encoding of the image to perform image\-to\-image search, for example <code>data:image/jpeg;base64,iVBORw0KGgoAAAANSUhEUgA....</code>.</div>


* <div data-tips="true" data-tips-type="tip">Enter the search keyword to perform text\-to\-image search, for example <code>White T-shirt</code>.</div>



```Shell
POST imagesearch/_search?search_pipeline=image_remote_embedding_search_pipeline
{
  "query": {
    "bool": {
      "must": [
        {
          "remote_neural": {
            "vector": {
              "query_text": "tos://doc-test/picture/image_temp/aaa.jpg",
              "k": 1
            }
          }
        }
      ]
    }
  }
}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80f069cc7b7d47068b9f12e9229444c3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cad8d3ef9d42aebac5c3a9eccd98c3~tplv-goo7wpa0wc-image.image) </span>

<span id="fa4fe6bd"></span>
## More information

The Image Embedding model created in this article supports direct vectorization of images and text and returns vectorized results.

You can obtain vectorized results of images and text by calling the Image Embedding model's private network access address from an ECS within the same VPC environment. For more information, see [Calling the embedding model](https://docs.byteplus.com/docs/6465/1337864).
