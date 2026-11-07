---
title: "upsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/upsertData"
---

<span id="overview"></span>
# Overview

This interface is used to write data into a specified Collection. The data to be written is specified as a Map, allowing one or more data entries to be inserted at a time, with a maximum of 100 data entries per insertion. If the provided primary key already exists, the corresponding data will be updated; otherwise, new data will be inserted.

Adjustments have been made to the V2 version of the UpsertData interface (only affecting **datasets requiring vectorization** with **vectorize** configuration; datasets already with vector\-type fields are not affected). Key information is as follows:


* For dataset writes with **vectorize** configuration, embedding calculation will change from real\-time synchronous to background asynchronous execution, resulting in some lag before data becomes effective;

* For write failure error messages, you can view them on the "Log Management" page of the Vector Database Console;

* The response body parameter no longer returns the `token_usage` field.


<span id="request-body-parameters"></span>
# Request Body Parameters


|Name |Type |Description |Required |
|---|---|---|---|
|CollectionName |string |Name of the dataset. |Either one is required |
|ResourceID |string |ID of the dataset. | |
|Data |[]map[string]any{} |List of data to be updated. Each Map in the list represents one data entry and must contain the primary key field. |Yes |
|TTL |int32 |Time\-To\-Live of the data, in seconds. Data will be automatically deleted after this time expires. |No |
|Async |bool |**For datasets "requiring vectorization":**  This parameter only distinguishes whether to perform streaming updates.<br><br><br>* Async=false, triggers index streaming update after asynchronous write takes effect<br><br>* Async=true, does not trigger index streaming update even after asynchronous write takes effect<br><br><br>**For datasets with "existing vector data":**  Asynchronous write switch.<br><br><br>* Asynchronous write rate limit threshold is 10 times that of synchronous writes<br><br>* Asynchronously written data is not synchronized to the collection in real time, with a lag time at the minute level. You can use the `FetchDataInCollection` interface to confirm whether data has been written to the collection<br><br>* Asynchronously written data does not trigger index streaming updates, index synchronization time is at the hour level. You can use the `FetchDataInIndex` interface to confirm whether data has been synchronized to the index |No |


<span id="data-parameter-field-value-format"></span>
# Data Parameter Field Value Format

Note: The primary key cannot be 0 when inserting data


|Field Type |Format |Description |
|---|---|---|
|int64 |Integer value |Integer |
|float32 |Floating point value |Floating point number |
|string |String |String. Content limit is 256 bytes |
|bool |true/false |Boolean type |
|list |String array |String array |
|list |Integer array |Integer array |
|vector |* Vector (array of floats)<br><br>* Base64 encoding after float32/float64 compression into bytes |Dense vector |
|sparse_vector |Dictionary list of input format <token_id, token_weight\>, used to represent the non\-zero index and corresponding value of the sparse vector, where token_id is string type and token_weight is float type |Sparse vector |
|text |string |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty) |
|image |interface{} |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Image TOS link `tos://{bucket}/{object}`<br><br>* http/https format link |
|video |interface{} |{<br><br>"value": `tos://{bucket}/{object}`, http/https format URL link, this field is required<br><br>"fps": 0.2 (value range 0.2\-5, optional)<br><br>} |
|dateTime |string |Minute level:<br><br>`yyyy-MM-ddTHH:mmZ` or `yyyy-MM-ddTHH:mm±HH:mm`<br><br>Second level:<br><br>`yyyy-MM-ddTHH:mm:ssZ` or `yyyy-MM-ddTHH:mm:ss±HH:mm`<br><br>Millisecond level:<br><br>`yyyy-MM-ddTHH:mm:ss.SSSZ` or `yyyy-MM-ddTHH:mm:ss.SSS±HH:mm`<br><br>Example: "2025\-08\-12T11:33:56+08:00" |
|geoPoint |string |Geographic coordinates `longitude,latitude`, where `longitude` ranges from (\-180,180) and `latitude` ranges from (\-90,90)<br><br>Example: "116.408108,39.915023" |


<span id="creation-time-type-field-date-time"></span>
## Creation Time Type Field (date_time)

Only one of the following formats can be used, all following the RFC3339 standard (https://datatracker.ietf.org/doc/html/rfc3339)

Example: "2025\-08\-12T12:34:56+08:00"


| |Format (string) |Example |Description |
|---|---|---|---|
|Minute level |`yyyy-MM-ddTHH:mmZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm±HH:mm` (specified timezone) |* `2025-08-12T04:34Z`<br><br>* `2025-08-12T12:34+08:00` |Both examples on the left will be parsed as Beijing time `2025-08-12` `12:34:00`. |
|Second level |`yyyy-MM-ddTHH:mm:ssZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm:ss±HH:mm` (specified timezone) |* `2025-08-12T04:34:56Z`<br><br>* `2025-08-12T12:34:56+08:00` |Both examples on the left will be parsed as Beijing time `2025-08-12` `12:34:56`. |
|Millisecond level |`yyyy-MM-ddTHH:mm:ss.SSSZ` (UTC time) or<br><br>`yyyy-MM-ddTHH:mm:ss.SSS±HH:mm` (with timezone) |* `2025-08-12T04:34:56.147Z`<br><br>* `2025-08-12T12:34:56.147+08:00` |Both examples on the left will be parsed as Beijing time `2025-08-12` `12:34:56.147`. |


<span id="return-parameters"></span>
# Return Parameters

The response body contains common parameters (see "Response Body Common Parameters Introduction" below).

<span id="response-body-common-parameters-introduction"></span>
## Response Body Common Parameters Introduction


|Parameter Name |Type |Description |
|---|---|---|
|RequestID |string |Request ID. |
|Code |string |Operation status code. Success is `Success`, otherwise it is an error code phrase. |
|Message |string |Execution information. On success, it is `The API call was executed successfully.`, otherwise it is an error message. |
|Result |map[string]interface{} |Operation result. If no data needs to be returned, `result = null`. |


<span id="request-example-code"></span>
# **Request Example Code**

```Go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/vikingdb-go-sdk/vector"
    "github.com/volcengine/vikingdb-go-sdk/vector/model"
    "os"
    "time"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       endpoint  = "https://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
       region    = "ap-southeast-1"
    )

    client, err := vector.New(
       vector.AuthIAM(accessKey, secretKey), // IAM auth
       // vector.AuthAPIKey(apiKey),            // APIKey auth
       vector.WithEndpoint(endpoint),
       vector.WithRegion(region),
       vector.WithTimeout(time.Second*30),
       vector.WithMaxRetries(3),
    )
    if err != nil {
       fmt.Println("New client failed, err: ", err)
       panic(err)
    }
    ctx := context.Background()

    resp, err := client.Collection(model.CollectionLocator{
       CollectionName: "Your Collection Name",
    }).Upsert(ctx, model.UpsertDataRequest{
       WriteDataBase: model.WriteDataBase{
          Data: []model.MapStr{
             {
                "id":      1,
                "type":    "type1",
                "name":    "vikingdb data",
                "content": "vikingdb is a vector database",
             },
          },
       },
    })
    if err != nil {
       fmt.Println("Upsert failed, err: ", err)
       panic(err)
    }

    fmt.Println(resp.Message)
}
```
