---
title: "Logical log conversion (wal2json)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/logical_log_conversion-wal2json"
---

The wal2json extension can output logical log files in JSON format for viewing or consumption by downstream systems.

<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   No need to execute SQL commands to create a plugin, just set the instance's modifiable parameter wal_level to `logical`. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

* Delete extension

   ```sql
   -- To stop output and release resources, execute the following command to delete the replication slot:
   SELECT 'drop' FROM pg_drop_replication_slot('replication_slot');
    ?column? 
   ----------
    drop
   (1 row)
   
   postgres=# select * from pg_replication_slots ;
    slot_name | plugin | slot_type | datoid | database | temporary | active | active_pid | xmin | catalog_xmin | restart_lsn | confirmed_flush_lsn | wal_status | safe_wal_size 
   -----------+--------+-----------+--------+----------+-----------+--------+------------+------+--------------+-------------+---------------------+------------+---------------
   (0 rows)
   ```
   


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage

```sql
--Create test table
CREATE TABLE test_table_pk (id SERIAL, name VARCHAR(30), time_info TIMESTAMP NOT NULL, PRIMARY KEY(id));
CREATE TABLE test_table_2_pk_no (id SERIAL, num NUMERIC(5,2), info TEXT);
-- create replication slot, slot name can be modified (note that different DBs need to create different slots, such as: replication_slot_xxx)
SELECT 'creat' FROM pg_create_logical_replication_slot('replication_slot', 'wal2json');
 ?column? 
----------
 creat
(1 row)

-- view the created replication slot
select * from pg_replication_slots ;
    slot_name     |  plugin  | slot_type | datoid | database | temporary | active | active_pid | xmin | catalog_xmin | restart_lsn | confirmed_flush_lsn | wal_status | safe_
wal_size 
------------------+----------+-----------+--------+----------+-----------+--------+------------+------+--------------+-------------+---------------------+------------+------
---------
 replication_slot | wal2json | logical   |  14037 | postgres | f         | f      |            |      |          495 | 0/17F5E28   | 0/17F5F80           | reserved   |      
        
(1 row)

--to add, delete, or modify data
BEGIN;
INSERT INTO test_table_pk (name, time_info) VALUES('myuser1', now());
INSERT INTO test_table_pk (name, time_info) VALUES('myuser2', now());
INSERT INTO test_table_pk (name, time_info) VALUES('myuser3', now());
DELETE FROM test_table_pk WHERE id < 3;
INSERT INTO test_table_2_pk_no (num, info) VALUES(3.14, 'pie');
UPDATE test_table_2_pk_no SET info = 'pizza' WHERE info = 'pie';
COMMIT;

--View the log in JSON format
SELECT data FROM pg_logical_slot_get_changes('replication_slot', NULL, NULL, 'pretty-print', '1');
WARNING:  table "test_table_2_pk_no" without primary key or replica identity is nothing
                                                    data                                                     
-------------------------------------------------------------------------------------------------------------
 {                                                                                                          +
         "change": [                                                                                        +
                 {                                                                                          +
                         "kind": "insert",                                                                  +
                         "schema": "public",                                                                +
                         "table": "test_table_pk",                                                          +
                         "columnnames": ["id", "name", "time_info"],                                        +
                         "columntypes": ["integer", "character varying(30)", "timestamp without time zone"],+
                         "columnvalues": [1, "myuser1", "2024-08-16 16:39:24.320516"]                        +
                 }                                                                                          +
                 ,{                                                                                         +
                         "kind": "insert",                                                                  +
                         "schema": "public",                                                                +
                         "table": "test_table_pk",                                                          +
                         "columnnames": ["id", "name", "time_info"],                                        +
                         "columntypes": ["integer", "character varying(30)", "timestamp without time zone"],+
                         "columnvalues": [2, "myuser2", "2024-08-16 16:39:24.320516"]                      +
                 }                                                                                          +
                 ,{                                                                                         +
                         "kind": "insert",                                                                  +
                         "schema": "public",                                                                +
                         "table": "test_table_pk",                                                          +
                         "columnnames": ["id", "name", "time_info"],                                        +
                         "columntypes": ["integer", "character varying(30)", "timestamp without time zone"],+
                         "columnvalues": [3, "myuser3", "2024-08-16 16:39:24.320516"]                         +
                 }                                                                                          +
                 ,{                                                                                         +
                         "kind": "delete",                                                                  +
                         "schema": "public",                                                                +
                         "table": "test_table_pk",                                                          +
                         "oldkeys": {                                                                       +
                                 "keynames": ["id"],                                                        +
                                 "keytypes": ["integer"],                                                   +
                                 "keyvalues": [1]                                                           +
                         }                                                                                  +
                 }                                                                                          +
                 ,{                                                                                         +
                         "kind": "delete",                                                                  +
                         "schema": "public",                                                                +
                         "table": "test_table_pk",                                                          +
                         "oldkeys": {                                                                       +
                                 "keynames": ["id"],                                                        +
                                 "keytypes": ["integer"],                                                   +
                                 "keyvalues": [2]                                                           +
                         }                                                                                  +
                 }                                                                                          +
                 ,{                                                                                         +
                         "kind": "insert",                                                                  +
                         "schema": "public",                                                                +
                         "table": "test_table_2_pk_no",                                                     +
                         "columnnames": ["id", "num", "info"],                                              +
                         "columntypes": ["integer", "numeric(5,2)", "text"],                                +
                         "columnvalues": [1, 3.14, "pie"]                                                   +
                 }                                                                                          +
         ]                                                                                                  +
 }
(1 row)

注：因为test_table_2_pk_no没有主键，所以update数据无法展示
```


<span id=".5YW25LuW"></span>
## Others

For more information, please see the[ wal2json official documentation](https://github.com/eulerto/wal2json).
