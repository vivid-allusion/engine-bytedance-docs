---
title: "Time-ordered globally unique identifier (pg_uuidv7)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_uuidv7"
---

<span id="2FLTw43R"></span>
## Introduction and applicable scenarios

UUID (universally unique identifier) is a 128\-bit identifier designed to ensure uniqueness with very high probability in distributed systems. However, traditional UUIDs (such as v4) are completely random. When used as database primary keys, they cause poor index insertion performance. Because new data is randomly distributed across index leaf nodes, leading to index fragmentation and frequent page splits.

The pg_uuidv7 extension implements the UUID v7 standard. The core feature of UUID v7 is **time ordering**. It embeds a high\-precision Unix timestamp in the high\-order bytes of the UUID, while the low\-order bytes are filled with random numbers to ensure uniqueness. This design offers significant advantages:


* **Index performance improvement**: since newly generated IDs are sequential in time, their physical positions in the B\-tree index are also adjacent. This greatly enhances index locality, reduces random I/O, and makes primary key index insertion performance close to auto\-increment integers (`SERIAL` or `BIGSERIAL`).

* **Global uniqueness**: retains the core advantages of UUID, suitable for use in distributed systems or scenarios that require merging records from different data sources, avoiding conflicts that may arise from auto\-increment IDs.

* **Sortability**: can be sorted by ID, equivalent to sorting by creation time.


pg_uuidv7 is an ideal choice in modern applications to replace auto\-increment integers or random UUIDs as primary keys.

<span id="NF4kmhN6"></span>
## Precautions


* **Time information exposure**: UUID v7 contains timestamp information at the time of generation. Although the precision is high, this is an explicit design feature that requires attention in scenarios sensitive to creation time.

* **Timestamp precision**: as specified in the official standard, the timestamp embedded in UUID v7 has millisecond precision.


<span id="pDBJ1xHt"></span>
## Create and delete extension

<span id="PwpwBWs3"></span>
### Create extension

Execute the following SQL commands to create the pg_uuidv7 extension.

```SQL
CREATE EXTENSION pg_uuidv7;
SELECT * FROM pg_extension WHERE extname = 'pg_uuidv7';
```


<span id="MDUUjnW1"></span>
### Delete extension

Execute the following command to delete the extension.

```Bash
DROP EXTENSION pg_uuidv7;
```


<span id="WxZmpN52"></span>
## Basic usage

pg_uuidv7 provides a series of functions for generating and parsing UUID v7.


|**Functions** |**Description** |**Usage** |
|---|---|---|
|`uuid_generate_v7()` |generate a standard UUID v7 value. This is the most commonly used function, usually used as the default value for table primary keys. |```SQL```<br>```-- generate single```<br>```SELECT uuid_generate_v7();  ```<br>```  ```<br>```-- use with default value```<br>```CREATE TABLE events (  ```<br>```    id UUID PRIMARY KEY DEFAULT uuid_generate_v7(),  ```<br>```    event_data JSONB  ```<br>```);  ```<br>```INSERT INTO events (event_data) VALUES ('{"type": "login"}'); ```<br> |
|`uuid_timestamp_to_v7(ts)` |Convert a `timestamp` to a UUID v7 value. When the second parameter is `true`, generate the start value with the random part as 0. The `false` default value applies otherwise.<br><br> |```SQL```<br>```SELECT uuid_timestamp_to_v7('2023-01-01 00:00:00'::timestamp);```<br> |
|`uuid_timestamptz_to_v7(tstz)` |Convert a `timestamptz` time to a UUID v7 value. When the second parameter is `true`, generate the start value with the random part as 0. The `false` default value applies otherwise. |```SQL```<br>```select uuid_timestamptz_to_v7(NOW() - INTERVAL '1 hour', true);```<br> |
|`uuid_v7_to_timestamp(uuid)`<br><br> |Extract the included `timestamp` from a UUID v7 value. |```SQL```<br>```SELECT uuid_v7_to_timestamp('01856ad8-a4c8-72f6-bae3-30453a7eeed5');```<br> |
|`uuid_v7_to_timestamptz(uuid)`<br><br> |Extract the included `timestamptz` time from a UUID v7 value. |```SQL```<br>```select uuid_v7_to_timestamptz('019b3541-5fa6-7a85-ad96-1ca1de8a39d5');```<br> |
