---
title: "Error codes for troubleshooting"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Error_codes_for_troubleshooting"
---

<span id="Error codes for troubleshooting"></span>
# Error codes for troubleshooting

<span id="1a89b460"></span>
# Get the error code

<span id="d2f311a9"></span>
## API

<span id="4ac6616a"></span>
#### Success

When a request succeeds, `code = 0` is returned as follows:

```Python
{"code":0,"message":"success","request_id":"02173901722303500000000000000000000ffff0a004c5f712d93"}
```


<span id="1e9ad313"></span>
#### Failure

When a request fails, the corresponding error code is returned. As shown in the following example, `code = 1000005` indicates that the `collection` does not exist.

```Plain
{"code":1000005,"message":"collection does not exist","request_id":"02173901687058500000000000000000000ffff0a004c5f532dbf"}
```


<span id="83f453b1"></span>
## SDK

In an SDK, an exception is thrown when the request fails. The content of the returned exception is in the same format as an API response. You can capture the exception and extract the `code` to troubleshoot the issue.

<span id="2791bfb1"></span>
# Error codes


|**Error Code** |**Description** |**Trigger Condition** |**Suggestion** |
|---|---|---|---|
|0 |The request succeeds. | | |
|1000001 |The authentication fails. |This code is returned when the access key ID or secret access key is incorrect, the request body is not signed, or the permission of the subaccount is insufficient. |* Check whether the access key ID and secret access key are correct.<br><br>* Check whether the subaccount has sufficient permissions. If not, see the linked document for information on granting permissions.<br><br>* Use the official API signature demo. For more information, refer to the following document.<br><br><br>https://docs.byteplus.com/en/docs/VikingDB/Preparation<br><br><br>* Use the automatic signing feature of the SDK. |
|1000003 |A request parameter is invalid. |This code is returned when a request parameter is incorrectly formatted or used. |* Check the request parameter based on the error message. If the error message is not clear, send your feedback. |
|1000004 |The collection already exists. |This code is returned when the collection you create has the same name as an existing one. |Check whether the collection exists. |
|1000005 |The collection does not exist. |This code is returned when the collection name is incorrect or non\-existent. |Check whether the collection exists. |
|1000007 |The index already exists. |This code is returned when the index you create has the same name as an existing one in the collection. |Check whether the index exists. |
|1000008 |The index does not exist. |This code is returned when the index name is incorrect or non\-existent. |Check whether the index exists. |
|1000011 |The row of data does not exist in the collection. |This code is returned when the row of data you update does not exist. |Check whether the row of data exists. |
|1000013 |The data fails to be deleted from the collection. |This code is returned when the data fails to be deleted. This is often caused by an issue on the server side. |Contact the customer support team for help. |
|1000014 |The data fails to be written to the collection. |This code is returned when the data fails to be written. This is often caused by an issue on the server side. |Contact the customer support team for help. |
|1000016 |The query vectors are invalid. |This code is returned when the query vectors are invalid due to inconsistent dimensions or incorrect format. |Check the query vectors. |
|1000017 |The primary key is invalid. |This code is returned when the primary key type does not match or the primary key format is incorrect. |Check the primary key. |
|1000019 |The scalar filter statement is invalid. |This code is returned when the format is incorrect, the field is not added to the scalar index, or the filter statement is improper. | |
|1000021 |The index search encounters an error. |This code is returned when an unknown error or failure occurs on the server side. |Contact the customer support team for help. |
|1000022 |The data fails to be retrieved from the index. |This code is returned when an unknown error or failure occurs on the server side. |Contact the customer support team for help. |
|1000023 |The index is being initialized. |This code is returned when you retrieve or query data during the initialization of the index. |Wait for the index to be initialized. If the index is not initialized after an hour, contact the customer support team for help. |
|1000025 |The embedding operation encounters an error. |This code is returned when an unknown error or failure occurs during the embedding of the unstructured data on the server side. |If the error occurs occasionally, check whether the format of the input data is correct.<br><br>Otherwise, contact the customer support team for help. |
|1000028 |An internal error occurs on the server side. |This code is returned when an unexpected error occurs on the server side. |Contact the customer support team for help. |
|1000029 |Rate limiting is triggered for requests. |This code is returned when the QPS of the API operation is too high. |If search requests are rate\-limited, increase the CPU quota. For more information, contact the customer support team.<br><br>If requests to other API operations are rate\-limited, check the call logic to avoid repeatedly initializing indexes or collections and adjust the frequency of calls. |
|1000031 |The collection alias does not exist. |This code is returned when the collection alias is incorrect or non\-existent. |Check whether the collection alias exists. |
|1000032 |The user has not subscribed to the service. |The user requests the vector database service in a region, such as North China, without subscribing to the service in that region. |Purchase the vector database service on the official BytePlus website or the Vector Database Cloud product page. |
|1000033 |The user has overdue payments. |This code is returned when the user has overdue payments. |Add funds to your account. |
|1000035 |The offline task does not exist. |This code is returned when no offline task is found based on the task ID. |Check whether the offline task exists. |
