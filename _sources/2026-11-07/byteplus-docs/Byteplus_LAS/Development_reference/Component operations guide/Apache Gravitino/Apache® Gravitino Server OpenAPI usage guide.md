---
title: "Apache® Gravitino Server OpenAPI usage guide"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Gravitino_Server_OpenAPI_usage_guide"
---

<span id="f9e40ba0"></span>
## Overview

Apache® Gravitino Server OpenAPI is a managed metadata service based on Apache® Gravitino. By providing standardized REST APIs, it enables users to centrally manage and discover data and AI assets scattered across different systems. This document is intended to provide external customers with instructions for using the core OpenAPI of Gravitino Server, helping customers quickly integrate this service into their existing data applications and workflows.

> Apache Gravitino, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in the allowlist phase and is only supported in North China 2 (Beijing) and East China 2 (Shanghai) regions. To use this feature, please <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submit a ticket</a></div>


<div data-tips="true" data-tips-type="tip">to apply. After activation, you will receive the service access endpoint (Endpoint). With the BytePlus access key (AK/SK), you can configure and use the service in the compute engine.</div>


<span id="5fa87f22"></span>
## Concepts and mappings

To ensure compatibility and consistency with the BytePlus ecosystem, you need to understand the mapping relationships of the following core concepts before using Gravitino Server OpenAPI:


* **Metalake**: Corresponds to your **BytePlus account ID (Volcengine AccountId)** . Metalake is the highest\-level unit for metadata isolation. All resources, permissions, and governance policies are bounded by it.

* **Catalog**: Maps to the Hive Catalog in the LAS (Lakehouse Analytics Service) metadata service. Catalog is a container for organizing and managing metadata, such as databases and tables.

* **Schema**: Refers to a database or schema, which is a collection of tables.

* **Table**: The definition of structured data, including columns, partitions, attributes, and other information.

* **Fileset**: A metadata abstraction for unstructured data, usually referring to a group of files.

* **Topic**: A topic in a message queue (such as Kafka).

* **Model**: Model metadata in AI/ML scenarios.


<span id="bf29f06f"></span>
## Preparation before use

Before calling the API, you need to complete the following preparatory tasks:

<span id="4ba40171"></span>
### Obtain service access information


* **Service endpoint**: `https://{endpoint}` (Please replace with the actual service address provided by BytePlus).

* **BytePlus access key (AK/SK)** : Used for API request signing. Please securely obtain and manage your Access Key ID (AK) and Secret Access Key (SK) from the BytePlus console.


<span id="a24e4994"></span>
### API request signature

All requests to Gravitino Server OpenAPI must be signed to verify the identity of the requester and ensure data integrity during transmission. The signature mechanism follows the unified standard of BytePlus.


* **Signature algorithm**: HMAC\-SHA256

* **Core request headers**:

   * `X-Date`: UTC time, formatted as `YYYYMMDDTHHMMSSZ`, for example `20251117T083000Z`.

   * `Authorization`: A string containing AK, signature version, timestamp, region, service, list of signed headers, and the final signature digest.


**Signature process overview**:


1. **Construct the canonical request (Canonical Request)** : Concatenate the HTTP method, URI, query string, request headers, and the hash value of the request body.

2. **Create the string to sign (String to Sign)** : Combine the signature algorithm, timestamp, credential scope, and the hash value of the canonical request.

3. **Calculate the signing key (Signing Key)** : Derive the signing key using the SK, time, region, service, and other information.

4. **Calculate the final signature (Signature)** : Use the signing key to perform HMAC\-SHA256 hashing on the string to sign.

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
Path = "/iceberg/v1/namespaces/{namespace}/tables"
Timestamp = "20251117T100000Z" # UTC time in ISO8601 format
Headers = "host;x-date"
RequestPayload = "{...}" # JSON content of the request body

# 2. Construct canonical request (Canonical Request)
CanonicalRequest = Method + '\n' + Path + '\n' + '' + '\n' + 'host:' + Host + '\n' + 'x-date:' + Timestamp + '\n' + '\n' + Headers + '\n' + Hex(SHA256(RequestPayload))

# 3. Construct string to sign (String to Sign)
StringToSign = "HMAC-SHA256" + '\n' + Timestamp + '\n' + Date(Timestamp) + '/' + Region + '/' + Service + '/request' + '\n' + Hex(SHA256(CanonicalRequest))

# 4. Calculate signing key (Signing Key)
DateKey = HMAC-SHA256(Date(Timestamp), "VOLC" + SK)
DateRegionKey = HMAC-SHA256(Region, DateKey)
DateRegionServiceKey = HMAC-SHA256(Service, DateRegionKey)
SigningKey = HMAC-SHA256("request", DateRegionServiceKey)

# 5. Calculate final signature (Signature)
Signature = Hex(HMAC-SHA256(StringToSign, SigningKey))

# 6. Construct Authorization Header
AuthorizationHeader = "HMAC-SHA256 Credential=" + AK + "/" + Date(Timestamp) + "/" + Region + "/" + Service + "/request, SignedHeaders=" + Headers + ", Signature=" + Signature
```


<span id="e751a338"></span>
## Core API description

The following describes the core OpenAPI interfaces of Gravitino Server. All interfaces must be accessed via HTTP and follow the signature authentication method described in the "Preparation" section.

<span id="c43a144f"></span>
### Query Metalake information

Load the details of the specified Metalake. In the BytePlus environment, this usually corresponds to the current BytePlus account.


* **Method**: `GET`

* **Path**: `/api/metalakes/{metalake_name}`


**Path parameters**:


|Parameter name |Type |Required |Description |
|---|---|---|---|
|`metalake_name` |String |Yes |The name of the Metalake, corresponding to the BytePlus account ID. |


**Request example**:

```Bash
curl -X GET 'https://{endpoint}/api/metalakes/your_account_id' \ 
--header 'X-Date: 20251117T090000Z' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/gravitino/request, SignedHeaders=host;x-date, Signature={signature}'
```


**Response example**:

```JSON
{
  "code": 0,
  "metalake": { 
    "name": "your_account_id",
    "comment": "This is a metalake for the current account.",
    "properties": {},
    "audit": {
      "creator": "system",
      "createTime": "2025-11-17T08:00:00Z"
    }
  }
}
```


**Status codes and common errors**:


* `200 OK`: Request succeeded.

* `404 Not Found`: The specified Metalake does not exist.


<span id="1c72a3d3"></span>
### List Catalogs

List all Catalogs under the specified Metalake.


* **Method**: `GET`

* **Path**: `/api/metalakes/{metalake_name}/catalogs`


**Request example**:

```Bash
curl -X GET 'https://{endpoint}/api/metalakes/your_account_id/catalogs' \
--header 'X-Date: 20251117T090500Z' \ 
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/gravitino/request, SignedHeaders=host;x-date, Signature={signature}'
```


**Response example**:

```JSON
{
  "code": 0,
  "identifiers": [
    {
      "namespace": [
        "your_account_id"
      ],
      "name": "hive_prod"
    }
  ]
}
```


<span id="3968160a"></span>
### Load Catalog

Retrieve the details of the specified Catalog.


* **Method**: `GET`

* **Path**: `/api/metalakes/{metalake_name}/catalogs/{catalog_name}`


**Request example**:

```Bash
curl -X GET 'https://{endpoint}/api/metalakes/your_account_id/catalogs/hive_prod' \
--header 'X-Date: 20251117T091000Z' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/gravitino/request, SignedHeaders=host;x-date, Signature={signature}'
```


**Response example**:

```JSON
{
  "code": 0,
  "catalog": {
    "name": "hive_prod",
    "type": "RELATIONAL",
    "provider": "hive",
    "comment": "Production Hive catalog",
    "properties": {
      "metastore.uris": "thrift://localhost:9083"
    },
    "audit": {
      "creator": "user1",
      "createTime": "2025-11-10T10:00:00Z"
    }
  }
}
```


<span id="664ea755"></span>
### List Schemas

List all Schemas (databases) under the specified Catalog.


* **Method**: `GET`

* **Path**: `/api/metalakes/{metalake_name}/catalogs/{catalog_name}/schemas`


**Request example**:

```Bash
curl -X GET 'https://{endpoint}/api/metalakes/your_account_id/catalogs/hive_prod/schemas' \
--header 'X-Date: 20251117T091500Z' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/gravitino/request, SignedHeaders=host;x-date, Signature={signature}'
```


**Response example**:

```JSON
{
  "code": 0,
  "identifiers": [
    {
      "namespace": [
        "your_account_id",
        "hive_prod"
      ],
      "name": "default"
    },
    {
      "namespace": [
        "your_account_id",
        "hive_prod"
      ],
      "name": "sales_db"
    }
  ]
}
```


<span id="579efbe4"></span>
### List Tables

List all Tables under the specified Schema.


* **Method**: `GET`

* **Path**: `/api/metalakes/{metalake_name}/catalogs/{catalog_name}/schemas/{schema_name}/tables`


**Request example**:

```Bash
curl -X GET 'https://{endpoint}/api/metalakes/your_account_id/catalogs/hive_prod/schemas/sales_db/tables' \
--header 'X-Date: 20251117T092000Z' \
--header 'Authorization: HMAC-SHA256 Credential={ak}/20251117/{region}/gravitino/request, SignedHeaders=host;x-date, Signature={signature}'
```


**Response example**:

```JSON
{
  "code": 0,
  "identifiers": [
    {
      "namespace": [
        "your_account_id",
        "hive_prod",
        "sales_db"
      ],
      "name": "orders"
    },
    {
      "namespace": [
        "your_account_id",
        "hive_prod",
        "sales_db"
      ],
      "name": "customers"
    }
  ]
}
```


<span id="84e2794b"></span>
### Fileset, Model, Topic

Currently, only Hive Catalog is supported in the product capabilities. To use other types of Catalogs, please contact technical support.

<span id="27d23a16"></span>
### Pagination parameter description

For APIs that return lists (such as listing Catalogs, Schemas, or Tables), pagination parameters are supported to control the quantity and position of returned results.


* `pageSize`: Specifies the number of entries returned per page. The default is 100.

* `pageToken`: Token used to obtain the next page of results. No need to provide this parameter for the first request. For subsequent requests, use the `nextPageToken` value returned in the previous response as this parameter.


<span id="6ac9abe6"></span>
## Region example values

When making API requests, you must specify the correct Region in the scope of the signature credentials and/or the request header. The following are example values for some available zones in BytePlus. Please refer to the region where the service is located for specifics:


* `cn-beijing`

* `cn-shanghai` (to be released)

* `cn-guangzhou` (to be released)


<span id="eb7838b3"></span>
## Frequently asked questions and troubleshooting

**Q**: **When calling the API,**  **`401 Unauthorized`** ** or ** **`SignatureDoesNotMatch`** ** errors are returned. What is the reason?** 

**A**: This usually indicates that the API request signature is incorrect. Please check carefully:


1. Whether the AK/SK is correct and has not expired.

2. Whether the time in the `X-Date` request header matches the current UTC time of the server, with a deviation not exceeding 15 minutes.

3. Whether the HTTP request content involved in the signature (method, path, parameters, request headers) is consistent with what was actually sent.

4. Whether the signature calculation process strictly follows the specifications in the official BytePlus documentation.


**Q: How to confirm which** **`metalake_name`** ** should be used?** 

**A**: `metalake_name` is mapped directly to the BytePlus account ID. You can find it on the account management page in the BytePlus console.

**Q: What should be entered in the** **`provider`** ** field when creating a Catalog?** 

**A**: `provider` specifies the type of Catalog, such as `hive`, `iceberg`, `jdbc`, and so on. In the BytePlus managed environment, you should typically enter `hive` to connect to the Hive Catalog in LAS.
