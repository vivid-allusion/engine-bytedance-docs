---
title: "Perform vector search using Python API"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/perform-vector-search-using-python-api"
---

This article explains how to connect to ByteHouse and use vector retrieval through the Python API.

<span id="87e6e2be"></span>
# Prerequisites


* Please ensure you have installed Python tools and are using version Python 3.8 or newer.

* Please ensure the ByteHouse you are using meets or exceeds version v2.2. You can log in to the ByteHouse console, click on **Tenant management** at the top, and view the engine version you are using on the **Basic information** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9c7749159774447ae90e4fe88549b56~tplv-goo7wpa0wc-image.image) </span>

* Please make sure you have enabled vector search. For details, refer to [Enable vector search](https://docs.byteplus.com/docs/bytehouse/vector-retrieval).

* For details on obtaining ByteHouse connection information, see [Retrieve ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity).


<span id="ccbbd987"></span>
# Connect via HTTP

<span id="b835cc83"></span>
## Step 1: Establish a connection

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


**Parameter Description**


|Parameter item |Required |Configuration Instructions |
|---|---|---|
|`host` |Yes |Set it as the server IP address or domain name. Set to the public network connection domain name of ByteHouse, you can view the corresponding information in ByteHouse console **Tenant Management**\>**Basic Information**\>**Network Information**. For details, please refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|`port` |Yes |Set it to 8123. |
|`user` |Yes |The configuration is set to bytehouse. |
|`password` |Yes |For ByteHouse's API Key, you can obtain your API Key via ByteHouse console under **Tenant ManagementConnection Information** . For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|`compress` |Yes |It defines the method of data compression, with options to set as zstd, lz4, or False.<br><br><br>* zstd: Recommended setting, high compression rate, moderate CPU overhead.<br><br>* lz4: High compression speed but lower compression ratio than ZSTD.<br><br>* False: Compression disabled. Disabling it may affect performance when transmitting large result sets. |
|`send_receive_timeout` |No |Set the timeout for a single request, measured in seconds. |
|`secure` |Yes |Set it as True. |


<span id="d003790b"></span>
## Step 2: Create a table


1. Define the schema for table creation.

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
   

   **Parameter Description**

   
   |Parameter item |Required |Configuration description |
   |---|---|---|
   |`embedding Array` |Yes |Vector field that stores arrays of floating\-point numbers. |
   |`CONSTRAINT cons_vec_len CHECK length(embedding)` |Yes |It defines the dimension value of the vector as `{dim}` to ensure data consistency and prevent index anomalies due to dimension mismatch. |
   |`INDEX vec_idx embedding` |Yes |It declares the index to be created and the column name of the index. In the example,<br><br><br>* `vec_idx` is the name of the index, which supports customization.<br><br>* `Embedding` is the column name for indexing, often using array fields that store vectors. |
   |`TYPE HNSW` |is |It defines the index algorithm used, supporting settings for HNSW, FLAT, IVF_FLAT, IVF_PQ, IVF_SQ.<br><br>Index supports setting parameters, with some defined as follows, more details are available in [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36):<br><br><br>* `METRIC`: Distance measurement method, supports setting to L2, COSINE.<br><br>* `DIM`: Vector dimension, must be consistent with the actual dimension value in the `embedding` field. |
   |`ENGINE` |is |The database engine is set to CnchMergeTree. |
   |`ORDER BY id` |Yes |Sort data by the `id` field to accelerate searches based on `id`. |
   

2. Execute the create table statement.

   ```Python
   client.command(schema)  
   ```
   


<span id="33066f2f"></span>
## Step 3: Insert vectors


1. Data Preprocessing.

   ```Python
   # embeddings (list of lists of floats) refers to a list of vectors
   # ids (list of integers) refers to the unique identifiers associated with the vectors
   data = zip(ids, embeddings)
   values = [list(elem) for elem in data] 
   ```
   

   **Parameter Description**

   
   |Parameter Items |Mandatory |Configuration Description |
   |---|---|---|
   |`data = zip(ids, embeddings)` |Yes |Data preprocessing involves pairing the `ids` and `embeddings` lists by element position, merging them into a tuple iterator |
   |`values = [list(elem) for elem in data]` |Yes |Data preprocessing involves converting each tuple into a list, ultimately resulting in a list of lists |
   

2. Insert Data.

   ```Python
   client.insert(f'{database}.{table}', values, column_names=['id', 'embedding'],
         column_type_names=['UInt64', 'Array(Float32)']) 
   ```
   

   **Parameter Description**

   
   |Parameter item |Required |Configuration description |
   |---|---|---|
   |`client.insert` |Yes |It defines the data to be inserted. |
   |`f'{database}.{table}'` |Yes |It defines the target table name. |
   |`values` |Yes |A two\-dimensional list representing multiple rows of data. The order of data in each row must be consistent with `column_names`. |
   |`column_names` |Yes |It specifies the order of column names. |
   |`column_type_names` |Yes |It designates the type of the specified column. |
   


<span id="1d167ebb"></span>
## Step 4: Query


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
   

   **Parameter Description**

   
   |Parameter items |Required |Configuration description |
   |---|---|---|
   |`{database}.{collection}` |Yes |It designates the target table name. |
   |`{metric}Distance` |Yes |It defines the distance function, allowing settings for `L2Distance` or `CosineDistance`. It must be consistent with the function used during table creation.<br><br>`{str(query)}`: Convert the query vector into a list string (such as `[0.1, 0.2, ...]`). |
   |`LIMIT {k}` |Yes |Return the top `k` most similar records. |
   |`settings` |Yes |The settings parameter configured in the example is described as follows, for other configurable settings parameters, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126):<br><br><br>* `enable_new_ann`: Set to 1, indicating the activation of the new Approximate Nearest Neighbor (ANN) search engine.<br><br>* `hnsw_ef_s` : represents the ef value used during search, which controls the search range. The higher the value, the more precise the search, but the lower the performance. |
   

2. Execute the query.

   ```Python
   results = client.query(q_str)   
   ```
   

3. Parse the results and extract the result ID.

   ```Python
   result_ids = [int(id) for id in results.result_columns[0]]  
   ```
   


<span id="9a1dffe0"></span>
# Connect via TCP

<span id="0622b339"></span>
## Step 1: Establish a connection

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


**Parameter Description**


|Parameter item |Required |Configuration Instructions |
|---|---|---|
|`host` |Yes |Set it as the server IP address or domain name. Configure it as ByteHouse's public connection domain name, which you can view under **Tenant Management**\>**Basic Information**\>**Network Information** on ByteHouse console. For details, please refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|`port` |Yes |Set it to 9000. |
|`user` |Yes |Fixed configuration is bytehouse. |
|`password` |Yes |For ByteHouse's API Key, you can obtain the API Key in **Tenant management** \> **Connection information** of the ByteHouse console. For more information, please see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|`compress` |Yes |It defines the data compression method, supporting settings of zstd, lz4, or False.<br><br><br>* zstd: Recommended setting, high compression ratio, moderate CPU overhead.<br><br>* lz4: Fast compression speed, but lower compression ratio compared to ZSTD.<br><br>* False: Compression is disabled. Disabling may affect performance when transmitting large result sets. |
|`send_receive_timeout` |No |Set the timeout for a single request, in seconds. |


<span id="921ee00b"></span>
## Step 2: Create a table


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
   

   **Parameter Description**

   
   |Parameter item |Required |Configuration description |
   |---|---|---|
   |`{database}.{table}` |Yes |Customize database and table names. |
   |`embedding Array` |Yes |Vector field, stores arrays of floating\-point numbers. |
   |`CONSTRAINT cons_vec_len CHECK length(embedding)` |Yes |It defines the dimension value of the vector as `{dim}` to ensure data consistency and prevent indexing issues due to mismatched dimensions. |
   |`INDEX vec_idx embedding` |Yes |It declares the indexes to be created and the column names for the indexes. In the example,<br><br><br>* `vec_idx` is the name of the index, which supports customization<br><br>* `embedding` is the column name for which the index is created, typically using an array field that stores vectors |
   |`TYPE HNSW` |Yes |It defines the indexing algorithm used, with settings for HNSW, FLAT, IVF_FLAT, IVF_PQ, IVF_SQ.<br><br>Index supports setting parameters, some of the parameters are defined as follows, for other parameters refer to [Index parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#91fa5d36):<br><br><br>* `METRIC`: Distance measurement method, with settings for L2, COSINE<br><br>* `DIM`: Vector dimension, must be consistent with the actual dimensionality number in the `embedding` field |
   |`ENGINE` |Yes |Database engine, settings: CnchMergeTree. |
   |`ORDER BY id` |Yes |Sort data by `id` Field, speed up queries based on `id`. |
   

2. Execute the create table statement.

   ```Python
   client.execute(schema) 
   ```
   


<span id="05b220c8"></span>
## Step 3: Insert vector


1. Data Preprocessing.

   ```Python
   #  embeddings(list[list[float]]): list of embeddings
   #  ids(list[int]): list of ids
   data = zip(ids, embeddings)
   values = [list(elem) for elem in data] 
   ```
   

   **Parameter Description**

   
   |Parameter Items |Required |Configuration Description |
   |---|---|---|
   |`data = zip(ids, embeddings)` |Yes |Data preprocessing step, merge the `ids` and `embeddings` lists by pairing elements by position, creating a tuple iterator. |
   |`values = [list(elem) for elem in data]` |Yes |Data preprocessing step, transform each tuple into a list, ultimately yielding a list of lists. |
   

2. Insert Data.

   ```Python
   client.execute(f'INSERT INTO {database}.{table} (id, embedding) VALUES', values) 
   ```
   

   **Parameter Description**

   
   |Parameter Items |Required |Configuration Description |
   |---|---|---|
   |`client.execute()` |Yes |It defines the data to be inserted. |
   |`f'INSERT INTO {database}.{table} (id, embedding) VALUES'` |Yes |It defines the target table name and the fields to be inserted along with their values.<br><br><br>* `{database}.{table}`: Specifies the target database and table name.<br><br>* `id, embedding`: Specifies the list of column names.<br><br>* `VALUES`: The data to be inserted. |
   |`values` |Yes |Two\-dimensional list, representing multiple rows of data. The order of each row of data must be consistent with `column_names`. |
   


<span id="f7676750"></span>
## Step 4: Query


1. Build Query Statement.

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
   

   **Parameter Description**

   
   |Parameter items |Required |Configuration description |
   |---|---|---|
   |`{database}.{collection}` |Yes |It specifies the target table name. |
   |`{metric}Distance` |Yes |It defines the distance function; support setting as `L2Distance` or `CosineDistance`. Must be consistent with the function used when creating the table.<br><br>`{str(query)}`: Convert the query vector into a list string (e.g., `[0.1, 0.2, ...]`). |
   |`LIMIT {k}` |Yes |Return the top `k` most similar records. |
   |`settings` |Yes |The parameter descriptions of settings configured in the example are as follows. For details on other configurable settings parameters, see [Settings parameters](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL#ec887126):<br><br><br>* `enable_new_ann`: Set to 1 to activate the new approximate nearest neighbor (ANN) search engine.<br><br>* `hnsw_ef_s`: Indicates the ef value used during search, which controls the search scope. A higher value results in more accurate searches but lower performance. |
   

2. Execute the query.

   ```SQL
   results = client.query(q_str)  
   ```
   

3. Analyze the results and extract the result ID.

   ```SQL
   result_ids = [int(i) for (i,) in results] 
   ```
   


&nbsp;
