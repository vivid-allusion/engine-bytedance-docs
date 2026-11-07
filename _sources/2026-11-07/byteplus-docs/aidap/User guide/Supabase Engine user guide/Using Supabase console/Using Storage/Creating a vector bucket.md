---
title: "Creating a vector bucket"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Creating_a_vector_bucket"
---

This topic introduces two methods to configure and manage vector buckets in the Supabase console and through the Admin API.

<span id="BwBftPLw"></span>
## Background

Vector bucket is a logical container provided by the AI\-native BaaS platform Supabase version for vector data management. It stores vector retrieval related data organization and actions. After creating a vector bucket, users can further create one or more vector tables within it to store vectors, metadata, and corresponding index configurations, supporting typical AI application scenarios such as semantic search, similarity search, RAG, and knowledge base recall.

From a usage perspective, vector bucket continues the developer\-friendly design in the Supabase ecosystem, enabling users to create, manage, and query vector data within the familiar Storage / Admin API system; however, at the core, the BytePlus AI\-native BaaS platform Supabase version is not limited to Supabase official default capabilities but enhances them with BytePlus’s self\-developed platform capabilities. Compared with the Supabase official solution, the BytePlus version offers the following advantages in vector capabilities:


* **Higher resource scale limits**: A single branch supports creating up to 1000 vector buckets, with the total number of vector tables across all vector buckets also limited to 1000, accommodating more business isolation scenarios (such as splitting vector data by tenant, knowledge base, business module, or environment).

* **Higher vector dimension support**: Vector tables support vector dimensions up to **32768 (32K)** , significantly higher than Supabase official current **4096 (4K)**  limit, suitable for high\-dimensional embedding models and scenarios requiring more semantic features.

* **Stronger query performance**: Vector retrieval is supported by a professional vector database at the core, offering better query performance than the Supabase official default solution (specific performance data subject to Milvus official release).

* **Professional vector database driven**: Powered by [Milvus version vector database](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Release_notes) at the core, supporting high\-dimensional vector retrieval, massive vector data management, and specialized vector capability development in AI scenarios.


<span id="E8JBZRVK"></span>
## Precautions


* A branch can create up to 1000 vector buckets.

* A branch can create up to 1000 vector tables in total across all vector buckets.

* New branches created via [Creating child branch](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_child_branch) and [Restoring branch](https://docs.byteplus.com/en/docs/aidap/Supabase-Restoring_a_branch) do not inherit buckets from the parent or original branch


<span id="QYLKEHFN"></span>
## Create vector buckets in the Supabase console

<span id="ycjIf4rU"></span>
### Prerequisites


* A workspace using the Supabase engine is created, and its status is Running. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="GcJFp02S"></span>
### Procedure


1. In the Supabase console, click **Storage** on the left to enter the Storage page.

2. In the left navigation bar of the Storage page, click **Vectors**, then on the **Vectors** page click  **+ New bucket**. In the pop\-up **Create vector bucket** window, complete the following configurations and click **Create** to finish creating the vector bucket.



|**Configuration item** |**Decscription** |
|---|---|
|Bucket name |Bucket name. Bucket name must meet the following rules:<br><br><br>* Only lowercase letters (a~z), numbers (0~9), and hyphens (\-) are allowed.<br><br>* Must start and end with a lowercase letter (a~z) or number (0~9).<br><br>* Length must be between 3 and 63 characters. |


<span id="BGmiPbh4"></span>
### Next steps

After creating the vector bucket, you also need to create a vector table.


1. On the **Vectors** page, click  **+ Create table**. In the pop\-up **Create vector table** page, complete the following configurations and click **Create** to finish creating the vector bucket.



|**Configuration item** |**Decscription** |
|---|---|
|**Name**<br><br> |The name of the vector table. Name of the vector table must meet the following rules:<br><br><br>* Only lowercase letters (a~z), numbers (0~9), hyphens (\-), and dots (.) are allowed.<br><br>* Length must be between 3 and 63 characters. |
|**Dimension** |Enter the vector dimension value. The dimension value must be an integer between 2 and 32768. |
|**Distance metric** |Choose vector distance measurement method:<br><br><br>* Cosine: cosine distance. Calculates similarity based on vector direction, regardless of vector length.<br><br>* Euclidean: Euclidean distance. Calculates the straight\-line distance between two vectors, considering both direction and length.<br><br>* Inner product (IP): inner product. Calculates the projection value of one vector on another; the larger the value, the higher the similarity. |
|**Metadata keys** |Add metadata key. Optional.<br><br>In the **Metadata keys** area, click **Add metadata key**, then enter the metadata key name in the input box.<br><br>The key name length must be between 1 and 63 characters and unique within the current table. To add multiple metadata keys, repeat clicking **Add metadata key**. |


<span id="byLg4YX8"></span>
## Configure and manage vector bucket through admin API

<span id="VbDqqApp"></span>
### Prerequisites

Obtained `SUPABASE_BASE_URL` and `SERVICE_ROLE_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).

<span id="1kC3PoRU"></span>
### Manage vector buckets through Admin API


* Query vector bucket list


```Bash
curl -X POST "$SUPABASE_BASE_URL/storage/v1/vector/ListVectorBuckets" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{}'
```



&nbsp;

* Create a vector bucket


```Bash
curl -X POST "$SUPABASE_BASE_URL/storage/v1/vector/CreateVectorBucket" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "vectorBucketName": "embeddings"
  }'
```



* Query vector tables


```Bash
curl -X POST "$SUPABASE_BASE_URL/storage/v1/vector/ListIndexes" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "vectorBucketName": "embeddings"
  }'
```



* Create a vector table


```JSON
curl -X POST "$SUPABASE_BASE_URL/storage/v1/vector/CreateIndex" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "vectorBucketName": "embeddings",
    "indexName": "documents-openai",
    "dataType": "float32",
    "dimension": 1536,
    "distanceMetric": "cosine"
  }'
```


<span id="sg6SOZa4"></span>
## Example: manage vector bucket and table through Supabase Client SDK

<span id="IO0S2FpN"></span>
### Initialize client

```JavaScript
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'https://your-project-id.supabase.co',
  'your-service-key'
)
```


<span id="WuHeRZtr"></span>
### Query and create vector bucket

```JavaScript
const { data: buckets } = await supabase.storage.vectors.listBuckets()

await supabase.storage.vectors.createBucket('embeddings')

const { data: bucket } = await supabase.storage.vectors.getBucket('embeddings')

console.log('✓ Vector bucket ready:', bucket)
```


<span id="BSvPisqE"></span>
### Create and query vector table

```JavaScript
const bucket = supabase.storage.vectors.from('embeddings')

await bucket.createIndex({
  indexName: 'documents-openai',
  dataType: 'float32',
  dimension: 1536,
  distanceMetric: 'cosine',
})

const { data: tables } = await bucket.listIndexes()
const { data: table } = await bucket.getIndex('documents-openai')

console.log('✓ Vector table ready:', table)
```
