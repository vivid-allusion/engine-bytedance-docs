---
title: "Use vector search with Python API"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/python-api"
---

This article explains how to connect to ByteHouse and use vector search through the Python API.

<span id="4bbb7658"></span>
# Prerequisites


* Ensure you have installed Python tools, version 3.8 or higher.

* Ensure you use ByteHouse version v2.6 or above. You can log in to the ByteHouse console, enter the **Cluster list**, click the target cluster, and check the engine version on the **Basic information** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31ca108046f64d40b89d9e8c335325cd~tplv-goo7wpa0wc-image.image) </span>

* Make sure you have enabled vector search. For details, refer to [Enable vector search](https://docs.byteplus.com/docs/bytehouse/start-vector-search-service).

* Obtain ByteHouse connection information; see details in [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).


<span id="b3c37914"></span>
# Connect via HTTP

<span id="aa7410c2"></span>
## Step 1: Establish connection

```Python
from clickhouse_connect import get_client
client = get_client(host="server", # server ip
                         port=8123,  # server http port
                         user="bytehouse", # user
                         password="password", # password
                         compress='zstd', # compress method, zstd recommanded
                         send_receive_timeout=1000, # connect timeout
                         secure=True) 
```


**Parameter description**


|Parameter item |Required |Configuration description |
|---|---|---|
|`host` |Yes |The server IP address or domain name. Set to ByteHouse's public connection domain name. You can find this information in the ByteHouse console under **Cluster management** \> **Cluster list** \> **Cluster** \> **Basic information**. For details, see [Cluster connection address](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#6ab9e6d0). |
|`port` |Yes |Set it to 8123. |
|`user` |Yes |Set it as the cluster connection account. You can log in to the ByteHouse Enterprise console, click the ByteHouse **Personal center** in the upper right corner. Then click **Account management** to view and copy the username in the cluster connection account. |
|`password` |Yes |After logging into BytePlus for the first time using IAM account and password, the system automatically generates the initial ByteHouse service password. You can log in to the ByteHouse Enterprise console, click the ByteHouse **Personal center** in the upper right corner. Then click **Account management** to view and copy the password in the cluster connection account. If the password is lost or forgotten, you can [Reset connection password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#9f131fd8). |
|`compress` |Yes |It defines data compression methods, supporting zstd, lz4, and False.<br><br><br>* zstd: Recommended setting with high compression ratio and moderate CPU usage.<br><br>* lz4: Fast compression speed but lower compression ratio than zstd.<br><br>* False: It disables compression. Disabling may affect performance when transferring large result sets. |
|`send_receive_timeout` |No |Set the timeout for a single request in seconds. |
|`secure` |Yes |Set it as True. |


<span id="437bf39c"></span>
## Step 2: Create table


1. Define the create table schema.

   ```Python
   schema = f"""\
                   CREATE TABLE IF NOT EXISTS {database}.{table}(
                       id UInt64,
                       embedding Array(Float32),
                       CONSTRAINT cons_vec_len CHECK length(embedding) = {dim},
                       INDEX vec_idx embedding TYPE HNSW('METRIC={metric.upper()}, DIM={dim}')
                   ) ENGINE = {engine} ORDER BY id\
                   """
   ```
   

   **Parameter description**

   
   |Parameter item |Required |Configuration description |
   |---|---|---|
   |`embedding Array` |Yes |A vector field that stores an array of floating\-point numbers. |
   |`CONSTRAINT cons_vec_len CHECK length(embedding)` |Yes |It defines the vector dimension value as {dim} to ensure data consistency and prevent index errors caused by dimension mismatches. |
   |`INDEX vec_idx embedding` |Yes |It declares the index to be created and its column name. For example,<br><br><br>* `vec_idx` is the name of the index and supports customization.<br><br>* `embedding` is the column name to create the index, typically using an array field that stores vectors. |
   |`TYPE HNSW` |Yes |It defines the index algorithm in use; supports HNSW, HNSW_SQ, FLAT, IVF_FLAT, IVF_PQ, IVF_SQ.<br><br>Index parameters can be set; some parameters are defined as follows, and other configurable parameters can be found at [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486):<br><br><br>* `METRIC`: Distance measurement method, supports L2 and COSINE.<br><br>* `DIM`: Vector dimension. It must match the actual dimension count of the `embedding` field. |
   |`ENGINE` |Yes |Database engine, which can be set to MergeTree, HaMergeTree, or HaUniqueMergeTree. |
   |`ORDER BY id` |Yes |Sort data by the `id` field to speed up queries based on `id`. |
   

2. Execute the create table statement.

   ```Python
   client.command(schema) 
   ```
   


<span id="9e9ff745"></span>
## Step 3: Insert vectors


1. Preprocess data.

   ```Python
   # embeddings(list[list[float]]) refers to a list of vectors
   # ids(list[int]) refers to the unique identifiers corresponding to the vectors
   data = zip(ids, embeddings)
   values = [list(elem) for elem in data]
   ```
   

   **Parameter description**

   
   |Parameter items |Required |Configuration description |
   |---|---|---|
   |`data = zip(ids, embeddings)` |Yes |Data preprocessing. It pairs elements from the `ids` and `embeddings` lists by position, merging them into a tuple iterator. |
   |`values = [list(elem) for elem in data]` |Yes |Data preprocessing. It converts each tuple into a list, resulting in a list of lists. |
   

2. Insert data.

   ```Python
   client.insert(f'{database}.{table}', values, column_names=['id', 'embedding'],
         column_type_names=['UInt64', 'Array(Float32)'])
   ```
   

   **Parameter description**

   
   |Parameters |Required |Configuration description |
   |---|---|---|
   |`client.insert` |Yes |It defines the data to be inserted. |
   |`f'{database}.{table}'` |Yes |It defines the target table name. |
   |`values` |Yes |A two\-dimensional list representing multiple rows of data. The order of each row must match `column_names`. |
   |`column_names` |Yes |It specifies the order of column names. |
   |`column_type_names` |Yes |It specifies the type of the column. |
   


<span id="7e545bad"></span>
## step 4: Query


1. Build the query statement.

   ```Python
   # query: list[float]
   q_str = f"""
           SELECT id
           FROM {database}.{collection}
           ORDER BY {metric}Distance(embedding, {str(query)}) 
           LIMIT {k}
           settings enable_new_ann=1, hnsw_ef_s={search_param["ef"]}
           """
   ```
   

   **Parameter description**

   
   |Parameter items |Required |Configuration description |
   |---|---|---|
   |`{database}.{collection}` |Yes |It specifies the target table name. |
   |`{metric}Distance` |Yes |It defines the distance function; set to `L2Distance` or `CosineDistance`. Must match the function used when creating the table.<br><br>`{str(query)}`: It converts the query vector into a list string (e.g., `[0.1, 0.2, ...]`). |
   |`LIMIT {k}` |Yes |It returns the top `k` most similar records. |
   |`settings` |yes |The settings parameters configured in the example are explained as follows. For other configurable settings parameters, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d):<br><br><br>* `enable_new_ann`: Set it to 1 to enable the new approximate nearest neighbor (ANN) vector search engine.<br><br>* `hnsw_ef_s`: It represents the ef value used during search to control the search scope; the larger the value, the more precise the search but lower the performance. |
   

2. Execute the query.

   ```Python
   results = client.query(q_str)  
   ```
   

3. Parse the results and extract the result ID.

   ```Python
   result_ids = [int(id) for id in results.result_columns[0]] 
   ```
   


<span id="20ca9e36"></span>
# Connect via TCP

<span id="d60076ff"></span>
## Step 1: Establish connection

```Python
from clickhouse_driver import Client
client = Client(host="server", # server ip
                         port=9000,  # server tcp port
                         user="test", # user
                         password="password", # password
                         connect_timeout=3000,
                         send_receive_timeout=3000) # connect timeout
                         
# If the version of clickhouse-driver is ≥ 0.2.9, you need to use the parameters below:
client = Client(host="server", # server ip
                         port=9000,  # server tcp port
                         user="test", # user
                         password="password", # password
                         connect_timeout=3000,
                         send_receive_timeout=3000,
                         client_revision=54430)
```


**Parameter description**


|Parameter item |Required |Configuration description |
|---|---|---|
|`host` |Yes |Server IP address or domain name. configure as ByteHouse’s public domain for connection. You can find this info in ByteHouse console under **Cluster management** \> **Cluster list** \> **Cluster** \> **Basic information**. See [Cluster connection address](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#6ab9e6d0) for details. |
|`port` |Yes |Set it to 9000. |
|`user` |Yes |Set it as the cluster connection account. You can log in to the ByteHouse Enterprise console, click the ByteHouse **Personal center** in the upper right corner. Then click **Account management** to view and copy the username in the cluster connection account. |
|`password` |Yes |After logging into BytePlus for the first time using IAM account and password, the system automatically generates the initial ByteHouse service password. You can log in to the ByteHouse Enterprise console, click the ByteHouse **Personal center** in the upper right corner. Then click **Account management** to view and copy the password in the cluster connection account. If the password is lost or forgotten, you can [Reset connection password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#9f131fd8). |
|`compress` |Yes |It defines the data compression method, supporting zstd, lz4, or False.<br><br><br>* zstd: Recommended setting It offers high compression rate with moderate CPU usage.<br><br>* lz4: Fast compression speed but lower compression rate than zstd.<br><br>* False: It disables compression. Disabling compression may affect performance when transmitting large result sets. |
|`send_receive_timeout` |No |Set the timeout for a single request, in seconds. |


<span id="50eb61a6"></span>
## Step 2: Create table


1. Define the table creation schema.

   ```Python
   schema = f"""\
                   CREATE TABLE IF NOT EXISTS {database}.{table}(
                       id UInt64,
                       embedding Array(Float32),
                       CONSTRAINT cons_vec_len CHECK length(embedding) = {dim},
                       INDEX vec_idx embedding TYPE HNSW('METRIC={metric.upper()}, DIM={dim}')
                   ) ENGINE = {engine} ORDER BY id\
                   """
   ```
   

   **Parameter description**

   
   |Parameter |Required |Configuration description |
   |---|---|---|
   |`{database}.{table}` |Yes |Customize the database and the table name. |
   |`embedding Array` |Yes |Vector field storing an array of floating\-point numbers. |
   |`CONSTRAINT cons_vec_len CHECK length(embedding)` |Yes |It defines the vector dimension value as {dim} to ensure data consistency and prevent index anomalies caused by dimension mismatch. |
   |`INDEX vec_idx embedding` |Yes |It declares the index to be created and the column name for the index. For example,<br><br><br>* `vec_idx` is the custom index name.<br><br>* `embedding` is the column name for the index, usually an array field storing vectors. |
   |`TYPE HNSW` |Yes |It defines the index algorithm used, supporting HNSW, HNSW_SQ, FLAT, IVF_FLAT, IVF_PQ, IVF_SQ.<br><br>Index supports parameter settings. Some parameters are defined as follows, for other configurable parameters refer to [Index parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#e7fa6486):<br><br><br>* `METRIC`: distance metric method, supports setting to L2 or COSINE.<br><br>* `DIM`: vector dimension, must match the actual dimension value of the `embedding` field. |
   |`ENGINE` |Yes |Database engine. It can be set to MergeTree, HaMergeTree, or HaUniqueMergeTree. |
   |`ORDER BY id` |Yes |Sort data by `id` field to speed up queries based on `id`. |
   

2. Execute create table statement.

   ```Python
   client.execute(schema)
   ```
   


<span id="a286c4f4"></span>
## Step 3: Insert vectors


1. Preprocess data.

   ```Python
   #  embeddings(list[list[float]]): list of embeddings
   #  ids(list[int]): list of ids
   data = zip(ids, embeddings)
   values = [list(elem) for elem in data]
   ```
   

   **Parameter description**

   
   |Parameter items |Required |Configuration description |
   |---|---|---|
   |`data = zip(ids, embeddings)` |Yes |Data preprocessing. It pairs the `ids` and `embeddings` lists element by element, merging them into an iterator of tuples. |
   |`values = [list(elem) for elem in data]` |Yes |Data preprocessing. It converts each tuple into a list, resulting in a list of lists. |
   

2. Insert data.

   ```Python
   client.execute(f'INSERT INTO {database}.{table} (id, embedding) VALUES', values)
   ```
   

   **Parameter description**

   
   |Parameter items |Required |Configuration Description |
   |---|---|---|
   |`client.execute()` |Yes |It defines the data to insert. |
   |`f'INSERT INTO {database}.{table} (id, embedding) VALUES'` |Yes |It defines the target table name and the fields with their values to insert.<br><br><br>* `{database}.{table}`: specify the target database and table name.<br><br>* `id, embedding`: specify the list of column names.<br><br>* `VALUES`: data to be inserted. |
   |`values` |Yes |Two\-dimensional list. It represents multiple rows of data. The order of data in each row must match `column_names`. |
   


<span id="1dfa6fa7"></span>
## Step 4: Query


1. Build query statement.

   ```Python
   # query: list[float]
   q_str = f"""
           SELECT id
           FROM {database}.{collection}
           ORDER BY {metric}Distance(embedding, {str(query)}) 
           LIMIT {k}
           settings enable_new_ann=1, hnsw_ef_s={search_param["ef"]}
           """
   ```
   

   **Parameter description**

   
   |Parameter items |Required |Configuration description |
   |---|---|---|
   |`{database}.{collection}` |Yes |Specify the target table name. |
   |`{metric}Distance` |Yes |It defines the distance function, supporting `L2Distance` or `CosineDistance`. Must be consistent with the function used when creating the table.<br><br>`{str(query)}`: converts the query vector into a list string (e.g., `[0.1, 0.2, ...]`). |
   |`LIMIT {k}` |Yes |Return the top `k` most similar records. |
   |`settings` |Yes |The parameter description for settings configured in the example is as follows, for details on other configurable settings parameters, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/use-vector-search#fc1ac31d):<br><br><br>* `enable_new_ann`: set to 1 to activate the new approximate nearest neighbor (ANN) search engine.<br><br>* `hnsw_ef_s`: represents the ef value used during search, which controls the search scope. Larger values mean more accurate search but lower performance. |
   

2. Execute query.

   ```SQL
   results = client.query(q_str) 
   ```
   

3. Parse result and extract result ID.

   ```SQL
   result_ids = [int(i) for (i,) in results]
   ```
   


&nbsp;
