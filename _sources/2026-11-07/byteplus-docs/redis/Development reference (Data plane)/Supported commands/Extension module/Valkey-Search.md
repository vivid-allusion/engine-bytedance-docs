---
title: "Valkey-Search"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/valkey-search"
---

Cache for Redis provides the Valkey\-Search extension module based on Valkey module. Leveraging Valkey\-Search's efficient vector storage and retrieval capabilities, you can convert historical conversation content into vector form and store it persistently in Redis instance. This helps build a Chatbot system with long\-term memory, providing reliable technical support for sustainable and highly consistent multi\-turn conversational interactions. This topic introduces the relevant information of the Valkey\-Search extension module in Cache for Redis, including its functional principles, applicable scenarios, and specific command syntax.

<span id="R6PyUhbP"></span>
## Prerequisites


* The instance version must meet the following requirements simultaneously to use the Valkey\-Search module:

   * The database version must be Redis 7.0.

   * The minor version of proxy must be greater than or equal to 1.511.0.

   * The minor version of server must be greater than or equal to 7.511.0.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the database version and minor version information of an instance on the <strong>Summary</strong> tab. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).


<span id="75WoXgko"></span>
## Features

Cache for Redis's Valkey\-Search provides two indexing algorithms for vector similarity search: Hierarchical Navigable Small World (HNSW) and Flat Search. The following table summarizes the feature differences and use cases of the two indexing algorithms for your reference.


|Feature comparison |HNSW |Flat search |
|---|---|---|
|Search principle |HNSW is a high\-performance approximate nearest neighbor search algorithm based on graph theory. The core of this algorithm lies in constructing a hierarchical navigable small\-world graph structure. By organizing data points into multi\-layer cascaded sparse graphs, it significantly improves search efficiency while maintaining high query accuracy. |Flat Search is a basic vector similarity retrieval method that uses an index\-free brute\-force matching mechanism. When performing a search, this algorithm compares the query vector with every vector in the dataset, without pre\-building complex data structures or performing approximate processing. This algorithm iterates through all data points for precise comparison, ensuring a 100% recall rate. |
|Search speed |A hierarchical graph structure enables short search paths and fast speeds. |Linear scan; query time increases linearly with data volume. With large data volumes, query latency is high, and resource consumption is significant. |
|Result accuracy |High accuracy in approximate searches, typically reaching over 90%\-99%. |100% accurate, returns the true nearest neighbor without approximation error. |
|Memory usage |High memory usage, requiring additional storage for graph edges and hierarchical structure. |Low memory usage, storing only raw vector data with almost no additional memory consumption. |
|Implementation complexity |Index construction is complex, algorithms and data structures are intricate, and parameter tuning is challenging. |Simple logic, easy to implement and maintain. |
|Data scalability |Highly scalable, suitable for large\-scale datasets ranging from hundreds of thousands to hundreds of millions. |Poor scalability, difficult to support real\-time updates or incremental addition of new data, suitable for small\-scale datasets. |
|Scenario |* Large\-scale, high\-dimensional, low\-latency, high\-concurrency vector search.<br><br>* Online services requiring fast response and high recall.<br><br>* Dynamic data environments (frequent insertions/deletions).<br><br>* Semantic search, recommendation systems, image retrieval, and so on. |* For small data volumes with no stringent query latency requirements.<br><br>* For scenarios requiring extremely high search result accuracy.<br><br>* Offline batch processing or experimental scenarios. |


<span id="BQyukabP"></span>
## Command syntax

<span id="CHrnNc9K"></span>
### Command list

The commands supported by Valkey\-Search are shown in the following table.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the command syntax in the following table, the definitions are as follows:</div>



* <div data-tips="true" data-tips-type="default"><code>UPPERCASE KEYWORD</code>: Command keyword, such as <code>FT.CREATE</code>.</div>


* <div data-tips="true" data-tips-type="default"><code>lowercase keyword</code>: Customizable parameter.</div>


* <div data-tips="true" data-tips-type="default"><code>[]</code>: The content within <code>[]</code> is an optional parameter, and the content outside <code>[]</code> is a required parameter.</div>


* <div data-tips="true" data-tips-type="default"><code><Option 1>|<Option 2>|<Option n></code>: A set of mutually exclusive parameter options, meaning only one parameter can be selected from the options for setting.</div>




|command |Syntax |Description |
|---|---|---|
|FT.CREATE<br><br> |```Bash```<br>```FT.CREATE <index-name>```<br>```    [ON HASH \| JSON]```<br>```    [PREFIX <count> <prefix> [<prefix>...]]```<br>```    SCHEMA```<br>```        (```<br>```            <field-identifier> [AS <field-alias>]```<br>```                  NUMERIC```<br>```                \| TAG [SEPARATOR <sep>] [CASESENSITIVE]```<br>```                \| VECTOR [HNSW \| FLAT] <attr_count> [<attribute_name> <attribute_value>]+)```<br>```        )+```<br> |Create an empty index, specifying index\-related attributes during creation, such as allowed key prefixes, vector algorithms, and vector dimensions. Supports HASH and JSON data type indexes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the index is successfully created, a backfilling process starts:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Continuously scans existing data and builds data that meets the criteria into the index.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Newly inserted data that meets the index conditions will also be automatically added to the index.</div><br> |
|FT.DROPINDEX<br><br> |```Bash```<br>```FT.DROPINDEX <index_name>```<br> |Delete the specified index.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This command only deletes the index, not the original data. You can asynchronously or synchronously delete original data using the <a href="https://redis.io/docs/latest/commands/unlink/">UNLINK</a> or <a href="https://redis.io/commands/del">DEL</a> commands.</div><br> |
|FT.SEARCH |```Bash```<br>```FT.SEARCH <index-name> ```<br>```          <query_string> ```<br>```          [NOCONTENT] ```<br>```          [TIMEOUT] ```<br>```          [PARAMS <count> <name1> <value1>...]```<br>```          [RETURN <count> <field_or_jsonpath> [AS <alias>] ...]```<br>```          [LIMIT <offset> <count>]```<br>```          [DIALECT <dialect>]```<br> |Execute a search query within the specified index. Supports extracting results using JSONPath.<br><br> |
|FT._LIST |```Bash```<br>```FT._LIST```<br> |Query the list of indexes created in the current database. |
|FT.INFO |```Bash```<br>```FT.INFO <index_name>```<br> |Query the details of a specified index, e.g., index parameters, amount of indexed data, and so on. Includes key_type (HASH or JSON).<br><br> |


<span id="EJjVKVEU"></span>
### Precautions


* To use the Valkey\-Search feature, [submit a support ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.

* After the application is completed, accounts with the Administrator role will have all permissions for Valkey\-Search related commands by default. You can also create a new role that allows the use of all Valkey\-Search commands according to business needs (that is, the ACL rule of this role needs to be set to `+@valkey_search`). After creating the role, you need to log in to Redis with an account that has this role to use Valkey\-Search related commands. For specific procedures about creating a role, refer to [Creating role](https://docs.byteplus.com/en/docs/redis/create-role).

* The Cache for Redis supports big and hot key analysis for the Valkey\-Search data type. It can help timely discover and analyze the details of hot keys and big keys in the database, providing data references for you to optimize hot keys and big keys. For specific procedures, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).

* After successfully applying for the use of the Valkey\-Search function, the instance will no longer support any data recovery functions, including:

   * [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set)

   * [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point)

   * [Recovery from deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance)


<span id="4UVhy4Oy"></span>
### FT.CREATE


|Category |Description |
|---|---|
|Command syntax |```Bash```<br>```FT.CREATE <index-name>```<br>```    [ON HASH \| JSON]```<br>```    [PREFIX <count> <prefix> [<prefix>...]]```<br>```    SCHEMA```<br>```        (```<br>```            <field-identifier> [AS <field-alias>]```<br>```                  NUMERIC```<br>```                \| TAG [SEPARATOR <sep>] [CASESENSITIVE]```<br>```                \| VECTOR [HNSW \| FLAT] <attr_count> [<attribute_name> <attribute_value>]+)```<br>```        )+```<br> |
|Time complexity |O (N log N), where N is the number of indexed items. |
|Command description |Create an empty index, specifying index\-related attributes during creation, such as allowed key prefixes, vector algorithms, and vector dimensions.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the index is successfully created, a backfilling process starts:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Continuously scans existing data and builds data that meets the criteria into the index.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Newly inserted data that meets the index conditions will also be automatically added to the index.</div><br> |
|Option |* `index-name`: The name of the newly created index. Required.<br><br>* `ON HASH \| JSON`: Specifies the data type of the indexed data, optional. Default value: HASH. To index JSON documents, set this to `JSON`.<br><br>* `PREFIX <count> <prefix>...`: Specifies the allowed key prefixes to be indexed. This parameter is optional; if not set, all HASH data is indexed by default.<br><br>   Among them, `<count>` is the number of prefixes, and `<prefix>` is the specific prefix. Multiple prefixes can be passed simultaneously. For example, `PREFIX 2 doc: user:` means that only keys starting with `doc:` or `user:` are indexed.<br><br>* `SCHEMA`: The core part of the index creation command, used to specify the index field name, field type, and field properties. Among them:<br><br>   * `field-identifier`: For HASH, it's the field name; for JSON, it's a JSONPath expression (e.g., `$.user.age`).<br><br>   * `AS field-alias`: Set an alias for the field, recommended for use with JSONPath to simplify queries.<br><br>   * `NUMERIC \| TAG \| VECTOR`: Specifies the index field type as `NUMERIC`, `TAG`, or `VECTOR`, where:<br><br>      * `NUMERIC`: Specifies numeric data for indexing.<br><br>      * `TAG`: The specified index contains data for the target tag.<br><br>         You can set the following properties for an index field of `TAG` type:<br><br>         * `SEPARATOR <sep>`: Specifies the delimiter for the tag. Optional. Value range: `,.<>{}[]\"':;!@#$%^&*()-+=~`. Default value: `,`.<br><br>         * `CASESENSITIVE`: Specifies whether the tag is case\-sensitive. Optional. Case\-insensitive by default.<br><br>      * `VECTOR`: Specifies data of the index vector type.<br><br>         You can select the `HNSW` or `FLAT` vector indexing algorithm for an index field of `VECTOR` type. Different indexing algorithms support different configurable properties:<br><br>         * `FLAT` algorithm supports the following properties:<br><br>            * `DIM <number>`: Vector dimension. Required.<br><br>            * `TYPE FLOAT32`: Data type. Required. Currently, only FLOAT32 is supported.<br><br>            * `DISTANCE_METRIC [L2 \| IP \| COSINE]`: Distance algorithm. Required. Value range: `L2`, `IP`, or `COSINE`.<br><br>            * `INITIAL_CAP <size>`: Initial index size. Optional.<br><br>         * `HNSW` algorithm supports setting the following properties:<br><br>            * `DIM <number>`: Vector dimension. Required.<br><br>            * `TYPE FLOAT32`: Data type. Required. Currently, only FLOAT32 is supported.<br><br>            * `DISTANCE_METRIC [L2 \| IP \| COSINE]`: Distance algorithm. Required. Value range: `L2`, `IP`, or `COSINE`.<br><br>            * `INITIAL_CAP <size>`: Initial index size. Optional.<br><br>            * `M <number>`: Specifies the maximum number of neighbors per node (that is the maximum outgoing edges) when building the index. Optional. Default value: 16, maximum value: 512.<br><br>            * `EF_CONSTRUCTION <number>`: Specifies the number of vectors to check during index construction. Optional. A higher value for this parameter increases recall, but also increases index creation time. Default value: 200, maximum value: 4096.<br><br>            * `EF_RUNTIME <number>`: Specifies the number of vectors to check during query operations. Optional. Default value: 10, maximum value: 4096. You can set this parameter for each query independently. A higher parameter value increases the recall rate but also extends the query time.<br><br>            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div><br>            <br><br>            <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">For more information about HNSW and FLAT vector index algorithms, refer to <a href="https://bytedance.larkoffice.com/docx/N5S0djrhLo6KHDxWcDGcZptpnmd#share-MOmPdrTnRo9qIvx6ZMfcu7g4nXc">Features</a>.            </div><br>             |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Create an HNSW index named `redis_doctest`. An example command is as follows.<br><br>```Bash```<br>```FT.CREATE redis_doctest SCHEMA doctest VECTOR HNSW 6 TYPE FLOAT32 DIM 3 DISTANCE_METRIC L2```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="XbmFvpfE"></span>
### FT.DROPINDEX


|Category |Description |
|---|---|
|Command syntax |```Bash```<br>```FT.DROPINDEX <index_name>```<br> |
|Time complexity |O(N), where N is the amount of indexed data. |
|Command description |Delete the specified index.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This command only deletes the index, not the original data. You can asynchronously or synchronously delete original data using the <a href="https://redis.io/docs/latest/commands/unlink/">UNLINK</a> or <a href="https://redis.io/commands/del">DEL</a> commands.</div><br> |
|Option |`<index_name>`: The name of the index to be deleted. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example<br><br> |Command example.<br><br>```Bash```<br>```FT.DROPINDEX redis_doctest```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="DD8fCSSe"></span>
### FT.SEARCH


|Category |Description |
|---|---|
|Command syntax |```Bash```<br>```FT.SEARCH <index-name> ```<br>```          <query_string> ```<br>```          [NOCONTENT] ```<br>```          [TIMEOUT] ```<br>```          [PARAMS <count> <name1> <value1>...]```<br>```          [RETURN <count> <field1>...]```<br>```          [LIMIT <offset> <count>]```<br>```          [DIALECT <dialect>]```<br> |
|Time complexity |O(N), where N is the amount of indexed data. |
|Command description |Execute a search query within the specified index. |
|Option |* `index-name`: The index name to query. Required.<br><br>* `query_string`: The expression string for the search query. Required. The specific format of the query expression is `<filtering>=>[ KNN <K> @<vector_field_name> $<vector_parameter_name> <query-modifiers>]`. Among them:<br><br>   * `filtering`: Filtering condition. Using an asterisk (\*) indicates that no filtering is applied, meaning all vectors within the index will be searched.<br><br>   * `vector_field_name`: The vector field name for the specified index.<br><br>   * `KNN <K>`: Specifies using the KNN algorithm to return the `<K>` most similar results.<br><br>   * `@<vector_field_name>`: Specifies the KNN query vector field name. The vector must be encoded using Float32 numbers.<br><br>   * `$<vector_parameter_name>`: A placeholder for query parameters. The specific query vector binary data is passed through `PARAMS <count> <name1> <value1>...`. Parameters are passed.<br><br>   * `query-modifiers`: Keywords that specify KNN search behavior. Optional. The following keywords can be set:<br><br>      * `EF_RUNTIME`: Followed by a numeric value, which overrides the `EF_RUNTIME` parameter value specified during index creation.<br><br>      * `AS`: Renames the 'score' field in the query results to a specified string.<br><br>* `NOCONTENT`: Specifies whether to return the field content of the results. Optional. If this value is set, the search results will display the names of the keys, but other content like 'score' will not be returned.<br><br>* `TIMEOUT`: Specifies the query timeout. Optional. Unit: milliseconds.<br><br>* `PARAMS <count> <name1> <value1>...`: The number of parameters in the query string. Optional.<br><br>* `RETURN <count> <field1>...`: Specifies the fields required for search results. Optional. All fields are returned by default. Supports passing JSONPath paths to directly extract and return specific sub\-fields from JSON documents.<br><br>* `LIMIT <offset> <count>`: Limits the offset (`offset`) and count (`count`) of the returned results, optional. Default value: `LIMIT 0 10`, which means a maximum of 10 keys are returned.<br><br>* `DIALECT <dialect>`: Specifies the dialect of the query parser. Optional. When using JSONPath indexing or complex extraction, it must be set to `DIALECT 2`. |
|Response |* When the execution succeeds, returns results that match the query conditions.<br><br>* Other cases reply corresponding exception information. |
|Example |The following code uses vector similarity search as an example to introduce related command examples:<br><br><br>1. Execute the following command to create an HNSW index named `redis_doctest`, where `doctest` is the vector field.<br><br>   ```Bash```<br>```   FT.CREATE redis_doctest SCHEMA doctest VECTOR HNSW 6 TYPE FLOAT32 DIM 3 DISTANCE_METRIC L2```<br>```   ```<br>   <br><br>2. Execute the following command to insert test data.<br><br>   ```Bash```<br>```   HSET p1 doctest "\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x80?"```<br>```   HSET p2 doctest "\x00\x00\x00\x00\x00\x00\x80?\x00\x00\x00\x00"```<br>```   HSET p3 doctest "\x00\x00\x80?\x00\x00\x00\x00\x00\x00\x00\x00"```<br>```   HSET p4 doctest "\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x80?"```<br>```   HSET p5 doctest "\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x80?"```<br>```   ```<br>   <br><br>3. Execute the following command to perform a vector similarity search and return the 3 most similar data entries.<br><br>   ```Bash```<br>```   FT.SEARCH redis_doctest "*=>[KNN 3 @doctest $query_vector]" PARAMS 2 query_vector "\xcd\xccL?\x00\x00\x00\x00\x00\x00\x00\x00" DIALECT 2```<br>```   ```<br>   <br><br>   Query result example.<br><br>   ```Bash```<br>```   1) (integer) 3```<br>```   2) "p3"```<br>```   3) 1) "__doctest_score"```<br>```      2) "0.0399999953806"```<br>```      3) "doctest"```<br>```      4) "\x00\x00\x80?\x00\x00\x00\x00\x00\x00\x00\x00"```<br>```   4) "p2"```<br>```   5) 1) "__doctest_score"```<br>```      2) "1.6400001049"```<br>```      3) "doctest"```<br>```      4) "\x00\x00\x00\x00\x00\x00\x80?\x00\x00\x00\x00"```<br>```   6) "p1"```<br>```   7) 1) "__doctest_score"```<br>```      2) "1.6400001049"```<br>```      3) "doctest"```<br>```      4) "\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x80?"```<br>```   ```<br>    |


<span id="CjOPP6UF"></span>
### FT._LIST


|Category |Description |
|---|---|
|Command syntax |```Bash```<br>```FT._LIST```<br> |
|Time complexity |O(1). |
|Command description |Query the list of indexes created in the current database. |
|Option |None. |
|Response |* When the execution succeeds, all index names created in the current database are returned.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```FT._LIST```<br><br><br>Response example.<br><br>```Bash```<br>```1) redis_doctest```<br>```2) redis_doctest1```<br> |


<span id="ilvzg0OJ"></span>
### FT.INFO


|Category |Description |
|---|---|
|Command syntax |```Bash```<br>```FT.INFO <index_name>```<br> |
|Time complexity |O(1). |
|Command description |Query the details of a specified index, e.g., index parameters, amount of indexed data, and so on. |
|Option |`<index_name>`: The name of the index to query. |
|Response |* When the execution succeeds, relevant information about the specified index will be returned.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```FT.INFO redis_doctest```<br><br><br>Response example.<br><br>```Bash```<br>``` 1) index_name```<br>``` 2) redis_doctest```<br>``` 3) index_options```<br>``` 4) (empty array)```<br>``` 5) index_definition```<br>``` 6) 1) key_type```<br>```    2) HASH```<br>```    3) prefixes```<br>```    4) 1) ```<br>```    5) default_score```<br>```    6) "1"```<br>``` 7) attributes```<br>``` 8) 1) 1) identifier```<br>```       2) doctest```<br>```       3) attribute```<br>```       4) doctest```<br>```       5) type```<br>```       6) VECTOR```<br>```       7) index```<br>```       8)  1) capacity```<br>```           2) (integer) 10240```<br>```           3) dimensions```<br>```           4) (integer) 3```<br>```           5) distance_metric```<br>```           6) L2```<br>```           7) size```<br>```           8) "2"```<br>```           9) data_type```<br>```          10) FLOAT32```<br>```          11) algorithm```<br>```          12) 1) name```<br>```              2) HNSW```<br>```              3) m```<br>```              4) (integer) 16```<br>```              5) ef_construction```<br>```              6) (integer) 200```<br>```              7) ef_runtime```<br>```              8) (integer) 10```<br>``` 9) num_docs```<br>```10) "2"```<br>```11) num_terms```<br>```12) "0"```<br>```13) num_records```<br>```14) "2"```<br>```15) hash_indexing_failures```<br>```16) "0"```<br>```17) backfill_in_progress```<br>```18) "0"```<br>```19) backfill_complete_percent```<br>```20) "1.000000"```<br>```21) mutation_queue_size```<br>```22) "0"```<br>```23) recent_mutations_queue_delay```<br>```24) "0 sec"```<br>```25) state```<br>```26) ready```<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more details on the parameter information of the return results, refer to <a href="https://valkey.io/commands/ft.info/">Response</a>.</div><br> |
