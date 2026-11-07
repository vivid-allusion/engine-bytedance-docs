---
title: "Memory hypothetical index (hypopg)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-hypopg"
---

hypopg is a PostgreSQL extension that supports creating hypothetical indexes in memory. These indexes exist in memory and are not written to disk, so they do not occupy physical storage space nor incur actual I/O overhead.

Its core value lies in allowing database administrators (DBAs) and developers to safely and cost\-effectively evaluate the potential optimization effects of new indexes on specific queries without modifying production environment data structures or affecting online service performance. By analyzing the query plan with `EXPLAIN`, it is possible to determine whether the optimizer would choose to use this hypothetical index, providing a basis for deciding whether to create a real index.

<span id="RUOlHw1i"></span>
## Precautions


* **Applicable scope**: hypothetical indexes are visible to the optimizer only during query plan analysis with `EXPLAIN`, while `EXPLAIN ANALYZE` and actual query execution do not use them.

* **Session isolation**: hypothetical indexes are effective only in the current database session that created them. Other concurrent sessions cannot perceive or use them.

* **Lifecycle**: creating hypothetical indexes does not generate WAL (write\-ahead log) records, so all created hypothetical indexes are automatically lost when the database service restarts or the session ends.

* **Supported type**: only supports creating four types of hypothetical indexes: B\-tree, BRIN, HASH, and BLOOM (using BLOOM index requires the `bloom` extension installed).


<span id="ppNa3DHD"></span>
## Create and delete extension

<span id="LE25TwmM"></span>
### Create extension

Execute the following SQL command to create the hypopg extension and verify the installation's success by querying the `pg_extension` view.

```SQL
-- create
create extension hypopg;
-- check if the creation succeeded
SELECT * FROM pg_extension WHERE extname = 'hypopg';
```


<span id="Y0UMhs7s"></span>
### Delete extension

Execute the following command to delete the extension.

```Bash
drop extension hypopg;
```


<span id="3RGkdLYe"></span>
## Basic usage

<span id="N7n3JwAl"></span>
### Function enabling and configuration

Before using the hypothetical index function, enable and configure it through the GUC parameter.

```SQL
-- Function enabling
-- off: hypothetical index will not be used, and existing ones will not be deleted.
SET hypopg.enabled = on;
-- use real OID
-- off: use reserved OID range (about 2,500)
-- on: use real OID, unlimited quantity
SET hypopg.use_real_oids = off;
```


<span id="iAEMv0hP"></span>
### Key functions and views

The following table summarizes the core functions and views provided by the hypopg extension and their usage.


|Object |Function |Usage |
|---|---|---|
|hypopg_hidden_indexes<br><br> |Record all hidden indexes<br><br> |```SQL```<br>```SELECT * FROM hypopg_hidden_indexes;```<br> |
|hypopg_list_indexes<br><br> |Record all hypothetical indexes<br><br> |```SQL```<br>```SELECT * FROM hypopg_list_indexes;```<br> |
|hypopg |Retrieve hypothetical index details |```SQL```<br>``` SELECT * FROM hypopg();```<br> |
|hypopg_create_index |Create a hypothetical index |```SQL```<br>```SELECT * FROM hypopg_create_index('CREATE INDEX ON test_table (id, value)');```<br> |
|hypopg_drop_index |Delete hypothetical indexes |```SQL```<br>```-- first column of hypopg_list_indexes records indexrelid```<br>```SELECT hypopg_drop_index(indexrelid);```<br> |
|hypopg_get_indexdef |Retrieve definition |```SQL```<br>```SELECT hypopg_get_indexdef(indexrelid);```<br><br><br> |
|hhypopg_hidden_indexes<br><br> |Retrieve and record all hidden indexes |```SQL```<br>```SELECT * FROM hypopg_hidden_indexes();```<br> |
|hypopg_hide_index |Hide existing indexes, including hypothetical and real indexes |```SQL```<br>```SELECT hypopg_hide_index('index_name'::regclass);```<br> |
|hypopg_relation_size |Hypothetical index size |```SQL```<br>```SELECT pg_size_pretty(hypopg_relation_size(indexrelid));```<br> |
|hypopg_reset |Clear all hypothetical indexes<br><br> |```SQL```<br>```SELECT hypopg_reset();```<br> |
|hypopg_reset_index |Clear all hypothetical indexes<br><br> |```SQL```<br>```SELECT hypopg_reset_index();```<br> |
|hypopg_unhide_all_indexes |Cancel hiding all indexes |```SQL```<br>```SELECT hypopg_unhide_all_indexes();```<br> |
|hypopg_unhide_index |Cancel hiding a single index |```SQL```<br>```SELECT hypopg_unhide_index(index_oid);```<br> |
