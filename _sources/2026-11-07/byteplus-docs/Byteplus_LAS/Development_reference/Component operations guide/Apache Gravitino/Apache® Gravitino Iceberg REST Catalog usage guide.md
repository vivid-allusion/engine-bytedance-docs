---
title: "Apache® Gravitino Iceberg REST Catalog usage guide"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Gravitino_Iceberg_REST_Catalog_user_guide"
---

The Catalog is a managed service designed for enterprise data platforms, strictly adhering to the Apache Iceberg REST API specification. It provides unified and standardized Iceberg metadata read and write capabilities for various compute engines. This service is intended to simplify data management and security governance in multi\-engine and multi\-tenant environments.

<span id="348c60c2"></span>
## **Key advantages**


* **Unified access**: By offering a single REST endpoint for multiple compute engines and workloads, it significantly reduces integration and maintenance costs.

* **Multi\-tenant and multi\-catalog management**: Resources are isolated and governed based on Volcano Engine account and Catalog boundaries, which simplifies permission management and auditing.

* **Open standard compatibility**: Fully compatible with the Iceberg REST v1 specification, supporting the complete set of standard operations such as namespace and table creation, query, and deletion.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in the allowlist open phase and is only supported in North China 2 (Beijing) and East China 2 (Shanghai) regions. To use this feature, please <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submit a ticket</a> to apply. After activation, you will receive the service access endpoint (Endpoint). With the Volcano Engine access key (AK/SK), you can configure and use it in the compute engine.</div>


<span id="4c7a3e54"></span>
## Concept mapping

Before use, be sure to understand the mapping of the following key concepts in the Volcano Engine environment:


* **Metalake**: Corresponds to your **Volcano Engine account ID (AccountId)** . All resources and permissions are isolated and managed within this boundary.

* **Catalog**: Uniformly mapped to the **Hive Catalog** in the Volcano Engine LAS metadata management service.


<span id="38664b7f"></span>
## Preparation before use

Before configuring the client, complete the following preparations to ensure the service can be called successfully.

<span id="939e36cb"></span>
### Service endpoint and region (Region)

You need to obtain the service access endpoint (Endpoint) from Volcano Engine. Ensure that the client is deployed in the same region as the service or has network connectivity. Examples of region values include `cn-beijing` and `cn-shanghai`.

<span id="7114edd9"></span>
### Obtain access keys (AK/SK)

All API requests must be authenticated with a signature. Go to the "[Access Control](https://docs.byteplus.com/en/docs/297/bpiamconsole)" page in the Volcano Engine console to create and obtain access keys (Access Key ID and Secret Access Key).

<span id="858ad77e"></span>
### API signature

Apache® Gravitino Iceberg REST Catalog uses the Volcano Engine standard API signature mechanism to ensure confidentiality, integrity, and authentication of requests. You need to add the `Authorization` and `X-Date` fields to the header of each request.

> Apache Gravitino, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


**Signature steps overview**:


1. **Construct the canonical request (Canonical Request)** : Concatenate the HTTP method, URI, query string, request headers, and the hash value of the request body.

2. **Create the string to sign (String to Sign)** : Combine the signature algorithm, timestamp, credential scope, and the hash value of the canonical request.

3. **Calculate the signing key (Signing Key)** : Derive the signing key using the SK, time, region, service, and other information.

4. **Calculate the final signature (Signature)** : Use the signing key to perform an HMAC\-SHA256 hash calculation on the string to sign.

5. **Assemble the Authorization header**: Combine the AK and the calculated signature information to form the final `Authorization` request header.


The following is a pseudocode example for generating a signature to help you understand the signing process:

```Bash
# 1. Prepare input
AK = "{ak}" # Your Access Key ID
SK = "{sk}" # Your Secret Access Key
Region = "{region}" # For example: cn-beijing
Service = "las" # The service name is fixed as las
Host = "{endpoint}" # Service endpoint
Method = "POST"
Path = "/v1/namespaces/{namespace}/tables"
Timestamp = "20251117T100000Z" # UTC time in ISO8601 format
Headers = "host;x-date"
RequestPayload = "{...}" # Request body JSON content

# 2. Construct canonical request (Canonical Request)
CanonicalRequest = Method + '\n' + Path + '\n' + '' + '\n' + 'host:' + Host + '\n' + 'x-date:' + Timestamp + '\n' + '\n' + Headers + '\n' + Hex(SHA256(RequestPayload))

# 3. Construct string to sign (String to Sign)
StringToSign = "HMAC-SHA256" + '\n' + Timestamp + '\n' + Date(Timestamp) + '/' + Region + '/' + Service + '/request' + '\n' + Hex(SHA256(CanonicalRequest))

# 4. Calculate signing key (Signing Key)
DateKey = HMAC-SHA256(Date(Timestamp), SK)
DateRegionKey = HMAC-SHA256(Region, DateKey)
DateRegionServiceKey = HMAC-SHA256(Service, DateRegionKey)
SigningKey = HMAC-SHA256("request", DateRegionServiceKey)

# 5. Calculate final signature (Signature)
Signature = Hex(HMAC-SHA256(StringToSign, SigningKey))

# 6. Construct Authorization Header
AuthorizationHeader = "HMAC-SHA256 Credential=" + AK + "/" + Date(Timestamp) + "/" + Region + "/" + Service + "/request, SignedHeaders=" + Headers + ", Signature=" + Signature
```


**Note**: The above pseudocode is mainly for demonstrating the core signing process. In actual use, to control the signature validity period, additionally include the `X-Expire` field in the request header. This field works in conjunction with `X-Date` to control the number of valid days. For example, `-1` means does not expire. To maintain compatibility, `SignedHeaders` may omit `X-Expire`.

<span id="42338a6b"></span>
## API reference

The following are detailed descriptions of the core APIs. All requests must include the correct signature headers `Authorization` and `X-Date`.

<span id="4752edfe"></span>
### List namespaces

Query all namespaces under the specified catalog.


* **Method**: `GET`

* **Path**: `/v1/namespaces`


**Query parameters:** 


|Parameter name |Type |Required |Description |
|---|---|---|---|
|`pageToken` |string |No |Pagination token, used to retrieve the next page of results. Not required for the first request. |
|`pageSize` |integer |No |The number of results returned per page. The default is 100. |


**Request example:** 

```Bash
curl --location 'https://{endpoint}/iceberg/v1/namespaces?pageSize=10' \
--header 'X-Date: 20251117T100000Z' \
--header 'X-Expire: -1' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/grlavitinos/request, SignedHeaders=host;x-date, Signature={signature}' \
--header 'Region: {region}'
```


**Response example (success):** 

```JSON
{
    "namespaces": [
        ["default"],
        ["production"]
    ],
    "next-page-token": "..."
}
```


**Status codes and error codes:** 


* `200 OK`: Request succeeded.

* `401 Unauthorized`: Invalid signature or insufficient permissions.

* `500 Internal Server Error`: Internal server error.


<span id="23e3a1a7"></span>
### Create namespace

Create a new namespace in the catalog.


* **Method**: `POST`

* **Path**: `/v1/namespaces`


**Request body:** 


|Parameter name |Type |Required |Description |
|---|---|---|---|
|`namespace` |array[string] |Yes |The namespace to create. Supports multiple levels, for example `["accounting", "tax"]`. |
|`properties` |map[string, string] |No |Additional properties, for example `{"location": "tos://..."}` to specify the storage location. |


**Request example:** 

```Bash
curl --location 'https://{endpoint}/iceberg/v1/namespaces' \
--header 'X-Date: 20251117T100000Z' \
--header 'X-Expire: -1' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/grlavitinos/request, SignedHeaders=host;x-date, Signature={signature}' \
--header 'Region: {region}' \
--header 'Content-Type: application/json' \
--data '{
    "namespace": ["sales"],
    "properties": {
        "location": "tos://my-bucket/sales_data"
    }
}'
```


**Response example (success):** 

```JSON
{
  "namespace": ["sales"],
  "properties": {
    "location": "tos://my-bucket/sales_data"
  }
}
```


**Status codes and error codes:** 


* `200 OK`: Created successfully.

* `409 Conflict`: Namespace already exists.


<span id="62aa7b98"></span>
### Query namespace details

Obtain the metadata of the specified namespace.


* **Method**: `GET`

* **Path**: `/v1/namespaces/{namespace}`


**Request example:** 

```Bash
curl --location 'https://{endpoint}/iceberg/v1/namespaces/sales' \
--header 'X-Date: 20251117T100000Z' \
--header 'X-Expire: -1' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/grlavitinos/request, SignedHeaders=host;x-date, Signature={signature}' \
--header 'Region: {region}'
```


**Response example (success):** 

```JSON
{
  "namespace": ["sales"],
  "properties": {
    "location": "tos://bucket-path/sales_data"
  }
}
```


**Status codes and error codes:** 


* `200 OK`: Query succeeded.

* `404 Not Found`: Namespace does not exist.


<span id="ecd9b9b1"></span>
### Delete namespace

Delete an empty namespace.


* **Method**: `DELETE`

* **Path**: `/v1/namespaces/{namespace}`


**Request example:** 

```Bash
curl --location --request DELETE 'https://{endpoint}/iceberg/v1/namespaces/temp_ns' \
--header 'X-Date: 20251117T100000Z' \
--header 'X-Expire: -1' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/grlavitinos/request, SignedHeaders=host;x-date, Signature={signature}' \
--header 'Region: {region}'
```


**Response example (success):** 

```Plain
(无响应体，状态码 204 No Content)
```


**Status codes and error codes:** 


* `204 No Content`: Deleted successfully.

* `404 Not Found`: Namespace does not exist.

* `409 Conflict`: Namespace is not empty and cannot be deleted.


<span id="792fe929"></span>
### List tables

Query all tables under the specified namespace.


* **Method**: `GET`

* **Path**: `/v1/namespaces/{namespace}/tables`


**Request example:** 

```Bash
curl --location 'https://{endpoint}/iceberg/v1/namespaces/sales/tables' \
--header 'X-Date: 20251117T100000Z' \
--header 'X-Expire: -1' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/grlavitinos/request, SignedHeaders=host;x-date, Signature={signature}' \
--header 'Region: {region}'
```


**Response example (success):** 

```JSON
{
    "identifiers": [
        {"namespace": ["sales"], "name": "orders"},
        {"namespace": ["sales"], "name": "customers"} 
    ]
}
```


<span id="cbcfda45"></span>
### Create table

Create a new table in the specified namespace.


* **Method**: `POST`

* **Path**: `/v1/namespaces/{namespace}/tables`


**Request body:** 

The request body is a complex JSON object that includes the table name, schema, partition specification, write mode, properties, and more. For detailed structure, refer to the official Iceberg REST API documentation.

**Request example:** 

```Bash
curl --location 'https://{endpoint}/iceberg/v1/namespaces/sales/tables' \
--header 'X-Date: 20251117T100000Z' \
--header 'X-Expire: -1' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/grlavitinos/request, SignedHeaders=host;x-date, Signature={signature}' \
--header 'Region: {region}' \
--header 'Content-Type: application/json' \
--data '{
    "name": "new_orders",
    "schema": { ... },
    "partition-spec": { ... }
}'
```


**Response example (success):** 

Returns the complete table metadata JSON object.

```JSON
{
    "metadata-location": "tos://.../metadata.json",
    "metadata": { ... } 
}
```


For more interface details, see [REST Catalog Spec - Apache Iceberg™](https://github.com/apache/iceberg/blob/main/open-api/rest-catalog-open-api.yaml).
