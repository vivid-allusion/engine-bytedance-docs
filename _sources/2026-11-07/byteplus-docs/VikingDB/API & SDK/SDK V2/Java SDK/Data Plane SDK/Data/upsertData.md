---
title: "upsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/upsertdata"
---

<span id="overview"></span>
# Overview

This interface is used to write data into a specified Collection. The data to be written is specified as a Map, allowing insertion of one or more data entries at a time, with a maximum of 100 entries per request. If the provided primary key already exists, the corresponding data will be updated; otherwise, new data will be inserted.

Adjustments have been made to the V2 version of the UpsertData interface (only affecting **datasets requiring vectorization** with **vectorize** configuration; datasets already with vector type fields are not affected), with key information as follows:


* For datasets with **vectorize** configuration, embedding calculation will change from real\-time synchronous to background asynchronous execution, resulting in some delay for data to take effect;

* For write failure error messages, you can view them on the "Log Management" page of the Vector Database Console;

* The response body parameter no longer returns the `token_usage` field.


<span id="method-definition"></span>
# Method Definition

```Java
public DataApiResponse<UpsertDataResult> upsertData(UpsertDataRequest request)
        throws ApiClientException, VectorApiException
```


<span id="request-body-parameters"></span>
# Request Body Parameters


|Name |Type |Description |Required |
|---|---|---|---|
|collectionName |String |The name of the collection. |Either this or resourceId is required |
|resourceId |String |The ID of the collection. | |
|data |List[Map[String, Object]] |The list of data to be written. Each Map in the list represents one data entry and must include the primary key field. |Yes |
|ttl |integer |Time\-To\-Live for the data, in seconds. Data will be automatically deleted after this time expires. |No |
|async |Boolean |**For datasets "requiring vectorization":**  This parameter only distinguishes whether to perform streaming updates.<br><br><br>* async=false, triggers index streaming update after asynchronous write takes effect<br><br>* async=true, does not trigger index streaming update even after asynchronous write takes effect<br><br><br>**For datasets "already with vector data":**  Asynchronous write switch.<br><br><br>* Asynchronous write rate limit threshold is 10 times that of synchronous writes<br><br>* Asynchronously written data is not synchronized to the collection in real time, with latency at the minute level. You can use the `FetchDataInCollection` interface to confirm whether data has been written to the collection<br><br>* Asynchronously written data does not trigger index streaming updates, index synchronization time is at the hour level. You can use the `FetchDataInIndex` interface to confirm whether data has been synchronized to the index |No |


<span id="data-parameter-field-value-format"></span>
# data Parameter Field Value Format

Note: The primary key cannot be 0 when inserting data.


|Field Type |Format |Description |
|---|---|---|
|int64 |Integer value |Integer |
|float32 |Floating point value |Float |
|string |String |String. Content limited to 256 bytes |
|bool |true/false |Boolean type |
|list[string] |String array |String array |
|list[int64] |Integer array |Integer array |
|vector |* Vector (floating point array)<br><br>* base64 encoding after float32/float64 compressed to bytes |Dense vector |
|sparse_vector |Input format is a dictionary list of <token_id, token_weight\>, used to represent non\-zero subscripts of sparse vectors and their corresponding values, where token_id is of string type, and token_weight is of float type |Sparse vector |
|text |String |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty) |
|image |Object |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Image TOS link `tos://{bucket}/{object}`<br><br>* http/https format link |
|video |Object |{<br><br>"value": `tos://{bucket}/{object}`, http/https format URL link, this field is required<br><br>"fps": 0.2 (value range 0.2\-5, optional)<br><br>} |
|dateTime |string |Minute level:<br><br>`yyyy-MM-ddTHH:mmZ` or `yyyy-MM-ddTHH:mm±HH:mm`<br><br>Second level:<br><br>`yyyy-MM-ddTHH:mm:ssZ` or `yyyy-MM-ddTHH:mm:ss±HH:mm`<br><br>Millisecond level:<br><br>`yyyy-MM-ddTHH:mm:ss.SSSZ` or `yyyy-MM-ddTHH:mm:ss.SSS±HH:mm`<br><br>Example: "2025\-08\-12T11:33:56+08:00" |
|geoPoint |string |Geographic coordinates `longitude,latitude`, where `longitude` ranges from (\-180,180) and `latitude` ranges from (\-90,90)<br><br>Example: "116.408108,39.915023" |


<span id="datetime-type-field-date-time"></span>
## DateTime Type Field (date_time)

You can only fill in one of the following formats, all following the RFC 3339 standard (https://datatracker.ietf.org/doc/html/rfc3339)

Example: "2025\-08\-12T12:34:56+08:00"


| |Format (string) |Example |Description |
|---|---|---|---|
|Minute level |`yyyy-MM-ddTHH:mmZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm±HH:mm` (specified timezone) |* `2025-08-12T04:34Z`<br><br>* `2025-08-12T12:34+08:00` |Both examples on the left will be parsed as Beijing time `2025-08-12` `12:34:00`. |
|Second level |`yyyy-MM-ddTHH:mm:ssZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm:ss±HH:mm` (specified timezone) |* `2025-08-12T04:34:56Z`<br><br>* `2025-08-12T12:34:56+08:00` |Both examples on the left will be parsed as Beijing time `2025-08-12` `12:34:56`. |
|Millisecond level |`yyyy-MM-ddTHH:mm:ss.SSSZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm:ss.SSS±HH:mm` (with timezone) |* `2025-08-12T04:34:56.147Z`<br><br>* `2025-08-12T12:34:56.147+08:00` |Both examples on the left will be parsed as Beijing time `2025-08-12` `12:34:56.147`. |


<span id="return-parameters"></span>
# Return Parameters

For common response body parameters, see [Data Plane API Call Flow](https://www.volcengine.com/docs/84313/1791125?lang=zh#%E5%93%8D%E5%BA%94%E4%BD%93%E5%85%AC%E5%85%B1%E5%8F%82%E6%95%B0%E4%BB%8B%E7%BB%8D). There are no special response body parameters.

<span id="request-example-code"></span>
# **Request Example Code**

```Java
import com.volcengine.vikingdb.runtime.Util;
import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.vector.model.request.UpsertDataRequest;
import com.volcengine.vikingdb.runtime.vector.model.response.DataApiResponse;
import com.volcengine.vikingdb.runtime.vector.model.response.UpsertDataResult;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

import java.util.Arrays;
import java.util.HashMap;

public class UpsertDataExample {

    public static void main(String[] args) {
        // 1. Initialize client (please replace with your configuration)
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com",
                    "cn-beijing",
                    new AuthWithAkSk("your-access-key", "your-secret-key"),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        // 2. Prepare request
        UpsertDataRequest request = UpsertDataRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .data(Arrays.asList(
                        new HashMap<String, Object>() {{ put("id", 1); put("field1", "value1"); put("vector", Util.generateRandomVector(128)); }},
                        new HashMap<String, Object>() {{ put("id", 2); put("field1", "value2"); put("vector", Util.generateRandomVector(128)); }},
                        new HashMap<String, Object>() {{ put("id", 3); put("field1", "value3"); put("vector", Util.generateRandomVector(128)); }}
                ))
                .build();

        // 3. Send request
        try {
            DataApiResponse<UpsertDataResult> response = vectorService.upsertData(request);
            System.out.println("Upsert data successfully:");
            System.out.println(response);
        } catch (Exception e) {
            System.err.println("Failed to upsert data: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```
