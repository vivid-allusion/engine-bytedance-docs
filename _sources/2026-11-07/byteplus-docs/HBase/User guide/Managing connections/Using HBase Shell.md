---
title: "Using HBase Shell"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Using_HBase_Shell"
---

This article describes how to run HBase database management commands using HBase Shell.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have connected to the target HBase database using HBase Shell. For the connection method, see [Connecting to the instance using the HBase Shell](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_HBase_Shell_1).

<span id="g3Szj7rl"></span>
## Create a table

Use the following command to create a table named `tb1` with a ColumnFamily named `cf`.

```json
hbase(main):001:0> create 'tb1', 'cf'
```


The following result is returned.

```json
Created table tb1
Took 1.1770 seconds
=> Hbase::Table - tb1
```


<span id="MBSJtW6x"></span>
## Set a value

Use the following command to set the value for row `r1` and column `cf:col1` in table `tb1` to `v1`.

```json
hbase(main):001:0>put 'tb1', 'r1', 'cf:col1', 'v1'
```


The following result is returned.

```json
Took 0.2374 seconds  
```


<span id="88s06rIB"></span>
## View a value

Use the following command to view the value of row `r1` in table `tb1`.

```json
hbase(main):001:0>get 'tb1', 'r1'
```


The following result is returned.

```json
COLUMN                           CELL               
f1:col1                          timestamp=1657619446922, value=v1
1 row(s)
Took 0.0927 seconds 
```


<span id="ED2rNmPK"></span>
## Related document

For more information about HBase Shell commands, see [HBase Shell Exercises](https://hbase.apache.org/1.1/book.html?spm=a2c4g.11186623.0.0.71702a79OogePa#shell_exercises) and [HBase Shell Commands](https://learnhbase.wordpress.com/2013/03/02/hbase-shell-commands/?spm=a2c4g.11186623.0.0.71702a79OogePa).
