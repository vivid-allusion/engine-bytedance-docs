---
title: "Intelligent index recommendation (index_advisor)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-index_advisor"
---

<span id="L7prlJgI"></span>
## Introduction and applicable scenarios

index_advisor is a practical PostgreSQL extension that automatically analyzes given SQL queries and recommends optimal indexes to improve query performance. This extension generates specific index creation suggestions by internally using hypopg to create hypothetical indexes and evaluate their impact on query plans.

Typical applicable scenarios include:


* **SQL tuning**: use it to quickly retrieve index optimization suggestions for a slow query.

* **Development phase**: assist developers in designing reasonable index strategies for complex queries in new features during development.


<span id="6hSf8baR"></span>
## Precautions


* **hypopg dependency**: index_advisor's functionality fully depends on the hypopg extension. When installing index_advisor, ensure that hypopg is also installed and enabled.

* **Index type limitation**: currently, index_advisor only supports recommending single\-column B\-tree indexes. It cannot provide suggestions for multi\-column indexes or other types of indexes.

* **Parameterized query**: when analyzing prepared statements containing parameters (such as `$1`, `$2`), if the extension cannot automatically infer the data type of the parameter, you may need to explicitly add type conversion for parameters in the query string, such as `...` `WHERE user_id = $1::integer`.


<span id="5XX0AnPu"></span>
## Create and delete extension

<span id="epIg1StV"></span>
### Create extension

Execute the `CREATE EXTENSION` command to install index_advisor. Using the `CASCADE` clause ensures its dependent hypopg extension is also installed automatically.

```SQL
-- requires hypopg, add cascade if hypopg is not installed
CREATE EXTENSION index_advisor cascade;
-- check if installation succeeded
SELECT * FROM pg_extension WHERE extname = 'hypopg' or extname = 'index_advisor';
```


<span id="nGu47D4M"></span>
### Delete extension

Execute the following command to delete the extension.

```Bash
DROP EXTENSION index_advisor;
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Uninstalling index_advisor will not automatically uninstall hypopg. If hypopg is no longer needed, it must be uninstalled separately.</div>


<span id="w01fVnpc"></span>
## Basic usage

The core function of index_advisor is provided through the `index_advisor()` function. This function accepts a SQL query string as input and returns one or more index creation suggestions.

<span id="yNARKvEr"></span>
### Function prototype

`index_advisor(sql_query TEXT)`

<span id="XCxNGcZw"></span>
### Examples


1. Create an example table

   ```SQL
   CREATE TABLE book (    id INT PRIMARY KEY,    title TEXT NOT NULL,    author_id INT NOT NULL);
   ```
   

2. Recommend an index for a simple query

   Analyze a query with a `WHERE` condition.

   ```SQL
   SELECT * FROM index_advisor('SELECT id FROM book WHERE title = ''A Tale of Two Cities''');
   ```
   

3. Recommend indexes for parameterized queries

   Analyze a query using placeholders.

   ```SQL
   SELECT * FROM index_advisor('SELECT id FROM book WHERE author_id = $1');
   ```
   

4. Recommend indexes for complex `JOIN` queries

   The index_advisor can also handle complex queries with multi\-table joins.

   ```SQL
   -- assume tables author and publisher exist
   SELECT * FROM index_advisor('    
   SELECT b.id, b.title    
   FROM book b    
   JOIN author a ON b.author_id = a.id    
   WHERE a.name = $1
   ');
   ```
