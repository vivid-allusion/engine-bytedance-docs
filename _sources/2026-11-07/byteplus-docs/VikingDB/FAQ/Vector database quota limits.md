---
title: "Vector database quota limits"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/quota"
---

To ensure your application operates efficiently and avoids throttling, refer to this guide for the default API quota limits. This document details the specific rate limits for control plane APIs, data operations, bandwidth, and embedding models. If you encounter rate limiting, you can reduce call frequency or contact support to request a quota increase.

<span id="api-rate-limits"></span>
# API rate limits


|**Category** |**API V1** |**API V2** |**Quota** |
|---|---|---|---|
|Control plane API rate limits |Control plane APIs include:<br><br>/api/collection/create<br><br>/api/collection/list<br><br>/api/collection/info<br><br>/api/collection/drop<br><br>/api/collection/update<br><br>/api/collection/alias_info<br><br>/api/index/create<br><br>/api/index/list<br><br>/api/index/info<br><br>/api/index/drop<br><br>/api/index/update |All control plane APIs.<br><br>See [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2). |Account\-wide shared 50 QPS |
|Bandwidth | | |300 MB/s |
|Synchronous data write/delete/update |/api/collection/upsert_data<br><br>/api/collection/del_data<br><br>/api/collection/update_data |UpsertData (/api/vikingdb/data/upsert)<br><br>DeleteData (/api/vikingdb/data/delete)<br><br>UpdateData (/api/vikingdb/data/update) |Per collection shared 1,500 records/s |
|Asynchronous data write |/api/collection/upsert_data |UpsertData (/api/vikingdb/data/upsert) |Per collection shared 15,000 records/s |
|Synchronous data read |/api/collection/fetch_data |FetchDatainCollection (/api/vikingdb/data/fetch_in_collection) |Per collection shared 1,000 records/s |
|Embedding model throughput limits |/api/data/embedding/version/2 |Embedding (/api/vikingdb/embedding) |Per model 33,000 tokens/s<br><br>Note: doubao\-embedding\-large and doubao\-embedding\-vision default to 11,000 tokens/s. |
|Embedding image throughput limits |/api/data/embedding/version/2 |Embedding (/api/vikingdb/embedding) |Account\-wide shared 15 images/s |
|Embedding video throughput limits |/api/data/embedding/version/2 |Embedding (/api/vikingdb/embedding) |Account\-wide shared 1 video/s |
