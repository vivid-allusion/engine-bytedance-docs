---
title: "updateVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateVikingdbCollection"
---

<span id="overview"></span>
# Overview

updateVikingdbCollection is used to add fields to a specified Collection and can modify the collection description.

Collections support adding new fields. Already defined fields cannot be modified; only the collection description can be modified.

<span id="method-definition"></span>
# Method Definition

```Java
public UpdateVikingdbCollectionResponse updateVikingdbCollection(UpdateVikingdbCollectionRequest body) throws ApiException 
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is UpdateVikingdbCollectionRequest. The parameters included in the UpdateVikingdbCollectionRequest class are shown in the table below.


|Parameter |Type |Required |Description |
|---|---|---|---|
|projectName |String |No |Project name. Corresponds to the Volcengine "project" concept. If not filled, it defaults to "default". |
|collectionName |String |One of two |Collection name.<br><br>Restrictions: English letters, numbers, or underscores. Must start with an English letter, length 1\-128 bytes. |
|resourceId |String | |Collection ID. Either this or collectionName is required (both can be filled). It is recommended to fill both to ensure accuracy. |
|description |String |No |Collection description.<br><br>Restrictions: English letters, numbers, or underscores. Must start with an English letter. Length not exceeding 64 bytes. |
|fields |List[FieldForUpdateVikingdbCollectionInput] |Yes |Fields in the collection.<br><br>Restrictions: Maximum 128 fields per collection. |



* Field Parameter Structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|fieldName |String |Yes |Field name.<br><br>Restrictions: English letters, numbers, or underscores. Must start with an English letter. Length not exceeding 64 bytes. |
|fieldType |FieldTypeEnum (Enumeration) |Yes |Field type.<br><br>Enumeration values include:<br><br>vector, sparse_vector, string, int64, float32, bool, list[string], list[int64], text, image, video |
|defaultValue |Object |No |Default value for field content.<br><br>Note: Fields of type vector/sparse_vector/text/image/video do not support default values. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |String |success |Operation result information |


<span id="example"></span>
## Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.console.collection;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

import java.util.Arrays;

public class UpdateVikingdbCollection {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the domain name of the vector database control plane v2  https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region


        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);


        VikingdbApi api = new VikingdbApi(apiClient);


        UpdateVikingdbCollectionRequest request = new UpdateVikingdbCollectionRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .fields(Arrays.asList(
                        new FieldForUpdateVikingdbCollectionInput().fieldName("f_string_add_1").fieldType(FieldForUpdateVikingdbCollectionInput.FieldTypeEnum.STRING),
                        new FieldForUpdateVikingdbCollectionInput().fieldName("f_float32_add_1").fieldType(FieldForUpdateVikingdbCollectionInput.FieldTypeEnum.FLOAT32)
                ));

        try {
            UpdateVikingdbCollectionResponse response = api.updateVikingdbCollection(request);
            System.out.println("response body: " + response);
            System.out.println();
            System.out.println("response meta RequestId: " + response.getResponseMetadata().getRequestId());
            System.out.println("response meta Service: " + response.getResponseMetadata().getService());
            System.out.println("response meta Region: " + response.getResponseMetadata().getRegion());
            System.out.println("response meta Action: " + response.getResponseMetadata().getAction());
            System.out.println("response meta Version: " + response.getResponseMetadata().getVersion());
        } catch (ApiException e) {
            System.out.println("exception http code: " + e.getCode());
            System.out.println("exception response body: " + e.getResponseBody());
            System.out.println();
            System.out.println("exception RequestId: " + e.getResponseMetadata().getRequestId());
            System.out.println("exception Action: " + e.getResponseMetadata().getAction());
            System.out.println("exception Region: " + e.getResponseMetadata().getRegion());
            System.out.println("exception Service: " + e.getResponseMetadata().getService());
            System.out.println("exception Error.Code: " + e.getResponseMetadata().getError().getCode());
            System.out.println("exception Error.Message: " + e.getResponseMetadata().getError().getMessage());
        }
    }
}
```
