---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hdfs_basic_usage"
---

<span id="hdfs-常见操作命令"></span>
## **Common HDFS operation commands**

**1. List HDFS files**

```Plain
hdfs dfs -ls <path>

```


**2. Upload files to HDFS**

```Plain
hdfs dfs -put <local file> <hdfs file>

#example:

hdfs dfs -put testFile /input/testFile

#把当前本地目录下的testFile文件上传到HDFS /input目录下，并命名为testFile

```


**3. Copy files from HDFS to the local system**

```Plain
hdfs dfs -get <hdfs file> <local file or dir>
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The names of the local file and the HDFS file must not be the same. Otherwise, a message will indicate that the file already exists. Files without duplicate names will be copied to the local system.</div>


To copy multiple files or directories to the local system, the local path must be a folder:

```Plain
hdfs dfs -get <hdfs file or dir> ... <local dir>

```


**4. Delete files**

```Plain
hdfs dfs -rm <hdfs file>

hdfs dfs -rm -r <hdfs dir>

```


**5. View a file in HDFS**

```Plain
hdfs dfs -cat <hdfs file>

```


**6. Create HDFS directories**

```Plain
hdfs dfs -mkdir <hdfs path>

```


It is important to note that the parent directory of the subdirectory to be created must exist. If the parent directory does not exist, an error will occur when using this command.

When using the following command to create a directory, the parent directory will be created automatically if it does not exist:

```Plain
hdfs dfs -mkdir -p <hdfs path>

```


**7. Copy files**

```Plain
hdfs dfs -cp <hdfs file> <hdfs file>

```


**8. Move files**

```Plain
hdfs dfs -mv <hdfs file> <hdfs file>

```


**9. Modify the permissions of directories or files**

```Plain
hadoop fs -chmod -R mode <hdfs file or dir>

#example：
hadoop fs -chmod -R 777 /usr

```


**10. View the storage usage of files or directories**

```Plain
hdfs dfs -du URI [URI …]

```


For more detailed information about HDFS commands, refer to the [Apache Hadoop](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html) community documentation.
