---
title: "Full-text search (pg_bigm)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_bigm"
---

pg_bigm is an extension provided by RDS for PostgreSQL. This extension offers full\-text search capabilities, allowing the creation of a 2\-gram GIN index to accelerate the search process.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The size of the column for creating a GIN index must not exceed 107,374,180 bytes (approximately 102 MB). Any attempt to input data exceeding this limit will cause an error.

* If the content stored in the database is not encoded in ASCII, it is recommended to change the database encoding to UTF8.


<span id=".5YmN572u5p2h5Lu2"></span>
## Prerequisites

Before using this extension, pg_bigm needs to be added to the shared_preload_libraries parameter. For more information about how to modify parameters, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is possible to create the extension without adding pg_bigm to the shared_preload_libraries parameter, <strong>but the extension will not function normally</strong>. The extension does not check shared_preload_libraries. Adding pg_bigm to the shared_preload_libraries parameter only reserves pg_bigm as a reserved_class_prefix to prevent users from using pg_bigm as a custom variable prefix. When not added to the shared_preload_libraries parameter, custom pg_bigm.xxx variables succeed but do not belong to the pg_bigm class. When added to the shared_preload_libraries parameter, custom pg_bigm.xxx variables fail because pg_bigm exists in reserved_class_prefix.</div>


<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   CREATE EXTENSION pg_bigm;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION pg_bigm;
   ```
   


<span id=".5L2_55So"></span>
## Usage

<span id=".5Yib5bu657Si5byV"></span>
### Create index

```sql
testdb=> CREATE TABLE books ( id SERIAL PRIMARY KEY, title TEXT, description TEXT);

testdb=> INSERT INTO books (title, description) VALUES
('Python 编程入门', '一本适合初学者的 Python 编程书籍。'),
('C 编程入门', '一本适合初学者的 C 编程书籍。'),
('数据库原理与应用', '介绍数据库的基本原理和实际应用。'),
('数据结构与算法', '深入讲解数据结构和算法知识。');

testdb=> CREATE INDEX idx_books_title ON books USING GIN (title gin_bigm_ops);
```


<span id=".5omn6KGM5YWo5paH5pys5pCc57Si"></span>
### Perform full\-text search

In this example, full\-text search matching is performed using LIKE, and results matching the keyword “Python programming” will be returned.

```sql
testdb=> SELECT * FROM books WHERE title LIKE '%Python 编程%';
 id |      title      |            description
----+-----------------+------------------------------------
  1 | Python 编程入门 | 一本适合初学者的 Python 编程书籍。
(1 row)
```


<span id=".5L2_55SoID0lIOaTjeS9nOespuaJp-ihjOebuOS8vOaAp-aQnOe0og=="></span>
### Perform similarity search using the `=%` operator

`=%` operator calculates the similarity between two strings and returns a float, with values closer to 1 indicating higher similarity.

```sql
testdb=> SET pg_bigm.similarity_limit TO 0.1;
testdb=> SELECT *FROM books WHERE title =% 'C 编程';
 id |      title      |            description
----+-----------------+------------------------------------
  1 | Python 编程入门 | 一本适合初学者的 Python 编程书籍。
  2 | C 编程入门      | 一本适合初学者的 C 编程书籍。
(2 rows)

testdb=> SET pg_bigm.similarity_limit TO 0.2;
testdb=> SELECT *FROM books WHERE title =% 'C 编程';
 id |   title    |          description
----+------------+-------------------------------
  2 | C 编程入门 | 一本适合初学者的 C 编程书籍。
(1 row)
```


<span id=".5o-S5Lu25bi455So5Ye95pWw"></span>
## Extension common functions

The pg_bigm extension’s common functions include likequery, show_bigm, bigm_similarity, and pg_gin_pending_stats. The basic information of these functions is as follows:


|Functions |Feature |Parameter |Return |Implementation principle |
|---|---|---|---|---|
|likequery |Generate a string recognized by the LIKE keyword. |1 request parameter with string type |Search string recognizable by the LIKE keyword. |* Add `%` symbol before and after the keyword.<br><br>* Use `\` to automatically escape the symbol `%`. |
|show_bigm |return the set of all 2\-gram elements of the given string |1 request parameter with string type |Array containing all 2\-gram elements. |* Add space characters before and after the string.<br><br>* Calculate all 2\-gram substrings. |
|bigm_similarity |Calculate the similarity between two strings. |2 request parameters, both of type string. |A floating\-point number representing similarity. |* Count the common 2\-gram elements between two strings.<br><br>* The similarity range is [0, 1], where 0 means completely different strings and 1 means identical strings.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When calculating 2\-gram, spaces are added before and after the string, so <code>ABC</code> and <code>B</code> have a similarity of 0, <code>ABC</code> and <code>A</code> have a similarity of 0.25.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The bigm_similarity function is case\-sensitive, for example, <code>ABC</code> and <code>abc</code> have a similarity of 0.</div><br> |
|pg_gin_pending_stats |return the number of pages and tuples in the pending list of the GIN index |1, the name or OID of the GIN index. |2, number of pages and tuples in the pending list. |If the GIN index is created with the parameter FASTUPDATE set to `false`, the GIN index does not have a pending list and returns 0. |


<span id=".5bi455So5Ye95pWw5L2_55So56S65L6L"></span>
### Examples of using common functions


* likequery

   ```sql
   testdb=> SELECT * FROM books WHERE title LIKE likequery('数据');
    id |      title       |           description
   ----+------------------+----------------------------------
     3 | 数据库原理与应用 | 介绍数据库的基本原理和实际应用。
     4 | 数据结构与算法   | 深入讲解数据结构和算法知识。
   (2 rows)
   ```
   

* show_bigm

   ```sql
   testdb=> SELECT show_bigm('full text search');
                               show_bigm                             
   ------------------------------------------------------------------
    {" f"," s"," t",ar,ch,ea,ex,fu,"h ","l ",ll,rc,se,"t ",te,ul,xt}
   (1 row)
   
   testdb=> SELECT show_bigm('Python 编程');
                     show_bigm
   ---------------------------------------------
    {"程 ",编程," 编"," P",Py,ho,"n ",on,th,yt}
   (1 row)
   ```
   

* bigm_similarity

   `bigm_similarity` function calculates the similarity between two strings, similar to the `=%` operator but called as a function.

   ```sql
   testdb=> SELECT bigm_similarity('ABC', 'A');
    bigm_similarity -----------------
               0.25
   (1 row)
   testdb=>  SELECT bigm_similarity('ABC', 'B');
    bigm_similarity -----------------
                  0
   (1 row)
   testdb=> SELECT bigm_similarity('ABC', 'abc');
    bigm_similarity -----------------
                  0
   (1 row)
   
   testdb=> SELECT id, title, bigm_similarity(title, 'Python 编程') AS similarity FROM books WHERE bigm_similarity(title, 'Python 编程') > 0.2;
    id |      title      | similarity
   ----+-----------------+------------
     1 | Python 编程入门 |       0.75
     2 | C 编程入门      |        0.2
   (2 rows)
   ```
   

* pg_gin_pending_stats

   ```sql
   testdb=> SELECT * FROM pg_gin_pending_stats('idx_books_title');
    pages | tuples 
   -------+--------
        0 |      0
   (1 row)
   ```
   


<span id=".5o-S5Lu25Y-C5pWw"></span>
## Extension parameter


|Parameter |Type |Default value |Value range |Description |
|---|---|---|---|---|
|pg_bigm.last_update |String |None |Read\-only parameter, cannot be modified. |the extension's last update date. |
|pg_bigm.enable_recheck |Boolean |on |on，off |Whether to proceed with recheck (an internal process of full\-text search).<br><br><br>1. Retrieve result candidates from the full\-text search index.<br><br>2. Select the correct search result from the candidates. The following process here is called recheck. Results retrieved from the full\-text search index may contain errors. The recheck process removes these errors.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to keep the default value (on) to ensure result accuracy.</div><br> |
|pg_bigm.gin_key_limit |Integer |0 |0 ~ 2147483647 |Limit the maximum number of 2\-gram elements for full\-text search. Default value 0 means use all 2\-gram elements. If performance drops using all 2\-gram elements, adjust this parameter to limit the number of 2\-gram elements to improve performance. |
|pg_bigm.similarity_limit |Real |0.3 |0~1 |Set the similarity threshold; tuples with similarity above this threshold are returned as similarity search results. |


Some parameter usage examples are as follows:


* pg_bigm.last_update

   ```sql
   testdb=> SHOW pg_bigm.last_update;
    pg_bigm.last_update 
   ---------------------
    2024.06.06
   (1 row)
   ```
   

* pg_bigm.enable_recheck

   ```sql
   testdb=> CREATE TABLE tbl (doc text);
   CREATE TABLE
   testdb=> INSERT INTO tbl VALUES('He is awaiting trial');
   INSERT 0 1
   testdb=> INSERT INTO tbl VALUES('It was a trivial mistake');
   INSERT 0 1
   testdb=> CREATE INDEX tbl_idx ON tbl USING gin (doc gin_bigm_ops);
   CREATE INDEX
   testdb=> SET enable_seqscan TO off;
   SET
   testdb=> EXPLAIN ANALYZE SELECT * FROM tbl WHERE doc LIKE likequery('trial');
                                                      QUERY PLAN                                                   
   ----------------------------------------------------------------------------------------------------------------
    Bitmap Heap Scan on tbl  (cost=5.50..6.61 rows=1 width=32) (actual time=0.014..0.015 rows=1 loops=1)
      Recheck Cond: (doc ~~ '%trial%'::text)
      Rows Removed by Index Recheck: 1
      Heap Blocks: exact=1
      ->  Bitmap Index Scan on tbl_idx  (cost=0.00..5.50 rows=1 width=0) (actual time=0.008..0.008 rows=2 loops=1)
            Index Cond: (doc ~~ '%trial%'::text)
    Planning Time: 0.221 ms
    Execution Time: 0.037 ms
   (8 rows)
   
   testdb=> SELECT * FROM tbl WHERE doc LIKE likequery('trial');
            doc
   ----------------------
    He is awaiting trial
   (1 row)
   
   testdb=> SET pg_bigm.enable_recheck = off;
   SET
   testdb=> SELECT * FROM tbl WHERE doc LIKE likequery('trial');
              doc
   --------------------------
    He is awaiting trial
    It was a trivial mistake
   (2 rows)
   
   testdb=>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, the bitmap index scan retrieved two rows from the full\-text search index, but only one row was returned after the recheck process.   </div>
   

<span id=".5YW25LuW"></span>
## Others


* Differences and similarities between pg_trgm and pg_bigm

   pg_trgm is another extension provided by RDS for PostgreSQL, using the 3\-gram model to implement full\-text search. The pg_bigm extension is a redevelopment based on pg_trgm. The differences between pg_bigm and pg_trgm are as follows:

   
   |Features and functions |pg_trgm |pg_bigm |
   |---|---|---|
   |phrase matching method for full\-text search |3\-gram |2\-gram |
   |Supported index types |GIN and GIST |GIN Only |
   |Supported full\-text search operators |LIKE (~~), ILIKE (~~\*), ~, ~\* |LIKE Only |
   |Full\-text search for non\-alphabetic languages (for example: Japanese) |Not support |Support |
   |full\-text search for keywords with 1 to 2 characters |Slow |fast |
   |Similarity search |Support |Support |
   |maximum indexable column size |238,609,291 bytes (about 228MB) |107,374,180 bytes (about 102MB) |
   

* For more information, refer to the [official documentation](https://github.com/pgbigm/pg_bigm/blob/v1.2-20240606/README.md).
