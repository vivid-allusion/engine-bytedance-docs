---
title: "embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/embedding_v2"
---

<span id="overview"></span>
# Overview

embedding is used to vectorize unstructured data. It extracts content and semantics from unstructured data such as text, images, audio, and video through deep learning neural networks, converting them into feature vectors.


* The current Embedding service only supports generating vectors from text.

* The current Embedding service API does not support high concurrency requests; requests will be dropped when the request volume is too high.


<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<EmbeddingResult> embedding(EmbeddingRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter |Type |Required |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|---|---|
|denseModel |EmbeddingModel |At least one of the two is required |name |string |Yes |Model name |
| | | |version |string |No, but required for Doubao models |Model version |
| | | |dim |int |No |Dimension. If not filled, the default dimension of this model version will be used. |
|sparseModel |EmbeddingModel | |name |string |Yes |Model name |
| | | |version |string |No |Model version |
|data |List[EmbeddingDataItem] |Yes | | | |Data. See below for detailed fields. Maximum list length is 10. If data type is fullModalSeq, length is 1 |


Structure is as follows:


|Parameter |Type |Required |Description |
|---|---|---|---|
|text |string |At least one is required, can also be a combination of text, image, and video |Text string content. Will be truncated if too long. See below for truncation thresholds for each model. |
|image |Object | |* See MediaData rules below<br><br>* Image tos link `tos://{bucket}/{object}`<br><br>* http/https format link |
|video |Object | |* See MediaData rules below<br><br><br>{<br><br>"value": `tos://{bucket}/{object}`, http/https format URL link, this field is required<br><br>"fps": 0.2 (value range 0.2\-5, optional)<br><br>} |
|fullModalSeq |list |If fullModalSeq is selected, the three parameters including text above cannot appear |See FullModalData structure below |



* MediaData (e.g., image, video can be strings) format specification:



|Choose one of two |* tos resource address within the same region. `tos://{bucket}/{object_key}` |
|---|---|
| |* Publicly accessible http/https link. `http://` or `https://` |



* FullModalData structure:



|Choose one of three |Field Name |Type |Remarks |
|---|---|---|---|
| |text |String |Plain text |
| |image |Object |If there are no special configuration parameters, use string type to fill in the image resource address, refer to MediaData specification; |
| |video |Object |If there are no special configuration parameters, map type can be used, sub\-parameters include:<br><br><br>* value: Use string type to fill in the video resource address, refer to MediaData specification.<br><br>* fps: Indicates the frame extraction frequency. Default is 1 if not set, range is 0.2\-5.0. However, the server defaults to extracting at least 16 frames. The higher the value, the more frames are extracted, the more tokens are consumed, and the higher the latency. |


<span id="model-list"></span>
## Model List


|Model Name |Model Version |Supported Vectorization Types |Default Dense Vector Dimension |Optional Dense Vector Dimensions |Text Truncation Length |Supports Sparse Vectors |Supports Instruction |
|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |Yes |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |
|bge\-visualized\-m3 |(default) |text, image, and their combinations |1024 |1024 |8192 |No |No |
|Skylark\-embedding |*240715* |text |2048 |512, 1024, 2048 |4096 |No |Yes |
|Skylark\-embedding\-vision |*250615* |Compatible with *241215* usages. Additionally, supports fullModalSeq (text/image/video sequence) |2048 |2048, 1024 |128k |No |Yes |


<span id="response-parameters"></span>
# Response Parameters


|Sub\-parameter |Type |Description |
|---|---|---|
|data |List[EmbeddingItem] |Data list |
|tokenUsage |Object |Token statistics by model granularity.<br><br>Includes prompt_tokens, completion_tokens, image_tokens, total_tokens information |


EmbeddingItem structure:


|Parameter Name |Type |Description |
|---|---|---|
|dense |List[Float] |Dense vector result |
|sparse |Map[String, Float] |Sparse vector result |


<span id="request-parameters"></span>
# Request Parameters

```Java
package org.example.newsubproduct.data;

import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.exception.ApiClientException;
import com.volcengine.vikingdb.runtime.exception.VectorApiException;
import com.volcengine.vikingdb.runtime.vector.model.request.*;
import com.volcengine.vikingdb.runtime.vector.model.response.*;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

import java.util.Arrays;

public class Embedding {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name of the vector database data plane v2 https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        EmbeddingRequest request = EmbeddingRequest.builder()
                .denseModel(EmbeddingModel.builder().name("Skylark-embedding-large").version("240915").dim(1024).build()) // Replace with your dense model
                .data(Arrays.asList(
                        EmbeddingDataItem.builder().text("this is a text for embedding").build()
                ))
                .build();

        try {
            DataApiResponse<EmbeddingResult> response = vectorService.embedding(request);
            System.out.println("request success:");
            System.out.println(response);
        } catch (VectorApiException vectorApiException) {
            System.err.println("request vectorApiException:");
            System.out.println("apiName: " + vectorApiException.getApiName());
            System.out.println("httpStatusCode: " + vectorApiException.getHttpStatusCode());
            System.out.println("code: " + vectorApiException.getCode());
            System.out.println("message: " + vectorApiException.getMessage());
            System.out.println("requestId: " + vectorApiException.getRequestId());
            System.out.println("responseContext: " + vectorApiException.getResponseContext().getBody());
        } catch (Exception e) {
            System.err.println("request exception, message : " + e.getMessage());
            e.printStackTrace();
        }
    }
}

```
