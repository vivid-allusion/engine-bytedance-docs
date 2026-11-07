---
title: "Cleaning space (pg_repack)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/cleaning_space-pg_repack"
---

RDS for PostgreSQL supports online Vacuum Full through the pg_repack extension. This feature addresses the issue of increasing physical disk space used by tables, indexes, and other objects due to frequent operations such as Update and Delete. Compared to Cluster and Vacuum Full, pg_repack does not block DML actions on the target table during execution.

<span id=".5Y6f55CG5LuL57uN"></span>
## Principle introduction

pg_repack supports repacking of entire tables and indexes to reduce disk space used by tables and indexes caused by Update and Delete actions.

<span id=".5a-55YWo6KGo6L-b6KGMIHJlcGFjaw=="></span>
### Repack the whole table

The principle of repacking the whole table is as follows:


1. Create a log table to record changes to the original table.

2. Create triggers in the original table, recording the `INSERT`, `UPDATE`, and `DELETE` actions to the log table.

3. Create a new table with the same rows and columns as the original table.

4. Perform `INSERT INTO SELECT` on the new table to import data from the original table.

5. Create indexes in the new table to match those in the original table one by one.

6. Apply changes from the log table to the new table.

7. Exchange the physical files of the new table (and its indexes) and the repacked original table (and its indexes).

8. Delete the new table and new indexes.

9. Perform `ANALYZE` on the target table to update statistical information.


In steps 1, 2, 6, 7, and 8 above, pg_repack briefly holds an ACCESS EXCLUSIVE lock; in other steps, pg_repack only needs to hold an ACCESS SHARE lock on the original table, not affecting the original table's `INSERT`, `UPDATE`, and `DELETE`.

<span id=".5a-557Si5byV6L-b6KGMIHJlcGFjaw=="></span>
### Repack the indexes

The principle of repacking the indexes is as follows:


1. Create a new index concurrently.

2. Exchange the physical files of the new indexes and the repacked target indexes.

3. Delete the old index files.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions


* pg_repack must be used with the client. RDS for PostgreSQL currently supports pg_repack versions 1.4.8 and 1.5.2, requiring the server binary version to match the client version.

* pg_repack requires additional storage space. When repacking the entire table, the remaining storage space must be at least twice the total space occupied by the table to be repacked and all its indexes.

* If the target table to be repacked has a primary key, and the primary key index definition includes an `INCLUDE` clause, then the columns included must be NOT NULL.

* pg_repack cannot clean up temporary tables.

* pg_repack cannot perform DDL on tables involved in repack operations during runtime. pg_repack will hold an ACCESS SHARE lock, preventing the execution of DDL.

* Rebuilding tables and indexes will occupy a lot of disk IO, it is recommended to assess the impact on the business in advance when using it.

* During pg_repack, do not perform a large amount of DML Actions, especially `UPDATE`, otherwise it will affect the efficiency and effect of the repack.

* pg_repack will generate a large amount of WAL logs, which will have a certain impact on archiving.

* The extension must be created in the target database that needs repacking.

* pg_repack must be executed by a super account.

* Before repacking large tables, it is recommended to execute `ALTER USER high privilege account name SET idle_in_transaction_session_timeout to 0` on the high\-privileged account involved in repack to prevent repack task failure due to excessively long repack time. After the repack task is completed, it can be reset by `ALTER USER high privilege account name RESET idle_in_transaction_session_timeout`.

* In the target library to be repacked, there should not be a `FOR ALL TABLES` publication, otherwise it will cause the repack to fail in the final application increment stage. Before executing repack, you can check through `SELECT count(*) FROM pg_publication WHERE puballtables = true` whether there is a `FOR ALL TABLES` publication in the target library to be repacked, a result of 0 indicates that there is none.


<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The pg_repack extension cannot be upgraded via the UPDATE method. It is necessary to first delete the old version of the plugin and then create the new version.</div>



* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   CREATE EXTENSION pg_repack;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION pg_repack;
   ```
   


<span id=".5a6J6KOF5a6i5oi356uv"></span>
### Install the client

pg_repack must be used with the client. The compilation method is as follows:


1. Download, unpack, compile, and install PostgreSQL 12.13.


```bash
wget https://github.com/postgres/postgres/archive/refs/tags/REL_12_13.tar.gz
tar -zxf REL_12_13.tar.gz
cd postgres-REL_12_13/

./configure --prefix=/usr/local/pgsql-12.13
make clean
make -sj
make install
```



2. Set up environmental variables.


```bash
export PG_HOME=/usr/local/pgsql-12.13
export PG_CONFIG=${PG_HOME}/bin/pg_config
export PATH=${PG_HOME}/bin:${PATH}

export PG_INCLUDE_DIR=$(${PG_HOME}/bin/pg_config --includedir)
export PG_PKG_INCLUDE_DIR=$(${PG_HOME}/bin/pg_config --pkgincludedir)
export PG_SERVER_INCLUDE_DIR=$(${PG_HOME}/bin/pg_config --includedir-server)
export PG_LIB_DIR=$(${PG_HOME}/bin/pg_config --libdir)
export PG_PKG_LIB_DIR=$(${PG_HOME}/bin/pg_config --pkglibdir)

export LD_LIBRARY_PATH=${PG_LIB_DIR}:${PG_PKG_LIB_DIR}${LD_LIBRARY_PATH+:${LD_LIBRARY_PATH}}
export C_INCLUDE_PATH=${PG_INCLUDE_DIR}:${PG_PKG_INCLUDE_DIR}:${PG_SERVER_INCLUDE_DIR}${C_INCLUDE_PATH+:${C_INCLUDE_PATH}}
export CPLUS_INCLUDE_PATH=${PG_INCLUDE_DIR}:${PG_PKG_INCLUDE_DIR}:${PG_SERVER_INCLUDE_DIR}${CPLUS_INCLUDE_PATH+:${CPLUS_INCLUDE_PATH}}
```



3. Download and install the source code of pg_repack 1.4.8 by compiling it.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The installation process of pg_repack version 1.5.2 is basically the same. All you need to do is modify the version number to 1.5.2 in the following steps.</div>


```bash
wget https://github.com/reorg/pg_repack/archive/refs/tags/ver_1.4.8.tar.gz
tar -zxf ver_1.4.8.tar.gz 
cd pg_repack-ver_1.4.8/

export PG_CONFIG=${PG_HOME}/bin/pg_config
make clean
make -sj
make install
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use Linxu x86, get the pg_repack 1.4.8 client from the link below.</div>



* <div data-tips="true" data-tips-type="tip">pg_repack 1.4.8</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c47d244577c2ff1220add59841f33aaa.gz"><ins>pg_repack 1.4.8 for PostgreSQL 11</ins></a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d33ac895bbcccf081cd6c2126a25b8e.gz">pg_repack 1.4.8 for PostgreSQL 12</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f7913928be0768fd4b3629f18f3627c.gz">pg_repack 1.4.8 for PostgreSQL 13</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03108d2a365e8541722ce42f6cf1fd5f.gz">pg_repack 1.4.8 for PostgreSQL 14</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9877efb75febd05614aef595553766cf.gz">pg_repack 1.4.8 for PostgreSQL 15</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b3e832c8aeb76759d96fdbb27f683610.gz">pg_repack 1.4.8 for PostgreSQL 16</a></div>


* <div data-tips="true" data-tips-type="tip">pg_repack 1.5.2</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d71faa47f96abf146bac622516445966">pg_repack 1.5.2 for PostgreSQL 11</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f35b0ed3513af8824d7420940eeb223">pg_repack 1.5.2 for PostgreSQL 12</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_37a439c2842df4b08464c90c4a3c059e">pg_repack 1.5.2 for PostgreSQL 13</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b34a5064357ab988331a4692543cc6b6">pg_repack 1.5.2 for PostgreSQL 14</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41294f953cafb02ae06e6775cb276343">pg_repack 1.5.2 for PostgreSQL 15</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abe6f1677108f178477ef4c927712bfc">pg_repack 1.5.2 for PostgreSQL 16</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7618cff8ddf158e8c044864c871022.8">pg_repack 1.5.2 for PostgreSQL 17</a></div>



<span id=".5L2_55So56S65L6L"></span>
## Examples


* See the help manual: `pg_repack --help`.

   ```bash
   pg_repack re-organizes a PostgreSQL database.
   
   Usage:
     pg_repack [OPTION]... [DBNAME]
   Options:
     -a, --all                 repack all databases
     -t, --table=TABLE         repack specific table only
     -I, --parent-table=TABLE  repack specific parent table and its inheritors
     -c, --schema=SCHEMA       repack tables in specific schema only
     -s, --tablespace=TBLSPC   move repacked tables to a new tablespace
     -S, --moveidx             move repacked indexes to TBLSPC too
     -o, --order-by=COLUMNS    order by columns instead of cluster keys
     -n, --no-order            do vacuum full instead of cluster
     -N, --dry-run             print what would have been repacked
     -j, --jobs=NUM            Use this many parallel jobs for each table
     -i, --index=INDEX         move only the specified index
     -x, --only-indexes        move only indexes of the specified table
     -T, --wait-timeout=SECS   timeout to cancel other backends on conflict
     -D, --no-kill-backend     don't kill other backends when timed out
     -Z, --no-analyze          don't analyze at end
     -k, --no-superuser-check  skip superuser checks in client
     -C, --exclude-extension   don't repack tables which belong to specific extension
   
   Connection options:
     -d, --dbname=DBNAME       database to connect
     -h, --host=HOSTNAME       database server host or socket directory
     -p, --port=PORT           database server port
     -U, --username=USERNAME   user name to connect as
     -w, --no-password         never prompt for password
     -W, --password            force password prompt
   
   Generic options:
     -e, --echo                echo queries
     -E, --elevel=LEVEL        set output message level
     --help                    show this help, then exit
     --version                 output version information, then exit
   
   Read the website for details: <https://reorg.github.io/pg_repack/>.
   Report bugs to <https://github.com/reorg/pg_repack/issues>.
   ```
   

* Check the current version of pg_repack.

   ```bash
   pg_repack --version
   ```
   

* Only print tables that support repack, but do not actually perform: `--dry-run`.

   ```bash
   pg_repack --no-superuser-check --dry-run --echo -h dbHost -p dbPort -d dbName -U dbUser --table tableName
   ```
   

* Repack a single table.

   ```bash
   pg_repack --no-superuser-check --echo -h dbHost -p dbPort -d dbName -U dbUser --table tableName
   ```
   

* Repack indexes.

   * Repack all indexes of the target table.

      ```bash
      pg_repack --no-superuser-check --echo -h dbHost -p dbPort -d dbName -U dbUser --table tableName --only-indexes
      ```
      

   * Repack specified indexes in the target table.

      ```bash
      pg_repack --no-superuser-check --echo -h dbHost -p dbPort -d dbName -U dbUser --index=indexName
      ```
      

* Repack all databases.

   Considering the success rate and efficiency of repack, it is recommended that you primarily choose single table repack, and do not perform full database repack.

   ```bash
   pg_repack --no-superuser-check --echo -h dbHost -p dbPort -d dbName -U dbUser --all
   ```
   


<span id=".5pu05aSa5Y-C6ICD"></span>
## More references

For more detailed instructions on using pg_repack, please refer to the [official pg_repack help document](https://reorg.github.io/pg_repack/).
