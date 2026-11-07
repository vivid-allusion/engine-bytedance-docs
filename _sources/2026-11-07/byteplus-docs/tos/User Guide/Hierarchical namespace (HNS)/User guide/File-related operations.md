---
title: "File-related operations"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/File-related-operations"
---

You can use the command line to upload, download, delete, and perform other operations in a hierarchical bucket.

<span id="69b57852"></span>
## Prerequisites


* A hierarchical namespace has been created. For detailed steps, refer to [Create a hierarchical namespace](https://docs.byteplus.com/docs/tos/Create-a-hierarchical-namespaces).

* EMR service has been activated and TOS authentication configured.


<span id="BErQf6tb"></span>
## Related commands and examples

<span id="4683ea0f"></span>
### Uploading a file

The following command uploads the local file `file1` to the `bucket1` bucket.

```JSON
hdfs dfs -put file1 tos://bucket1/file1
Or
hdfs dfs -put file1 tos://bucket1/
```


<span id="31db1707"></span>
### Create directory

The following command creates a `dir1` directory in the root of the `bucket1` bucket.

```JSON
hdfs dfs -mkdir tos://bucket1/dir1
```


<span id="26398d1b"></span>
### View file or directory information


* The following command lists the subfiles and subdirectories in the `dir1` directory.


```JSON
hdfs dfs -ls tos://bucket1/dir1   
```



* The following command checks the information of the `file1` file.


```JSON
hdfs dfs -ls tos://bucket1/file1
```



* The following command checks the size of the `dir1` directory.


```JSON
hdfs dfs -du tos://bucket1/dir1
```


<span id="bd7176ae"></span>
### Copy a file

The following command copies the `file1` file in the `bucket1` bucket as the `file3` file.

```JSON
hdfs dfs -cp tos://bucket1/file1 tos://bucket1/file3
```


<span id="46fac34e"></span>
### Downloading a file


* The following command downloads the `file1` file in the `bucket1` bucket to the local device and renames it to `file_download`.


```JSON
hdfs dfs -get tos://bucket1/file1  ./file_download
```



* For text files, you can use the following command to read the file content directly in the command line and print it to the screen.


```JSON
hdfs dfs -cat tos://bucket1/examplefile.txt
```


<span id="1f281d56"></span>
### Rename a file or directory


* The following command renames the file `file1` to `file4`.


```JSON
hdfs dfs -mv tos://bucket1/file1 tos://bucket1/file4  # Rename file1 to file4
```



* The following command renames the directory `dir1` to `dir2`.


```JSON
hdfs dfs -mv tos://bucket1/dir1 tos://bucket1/dir2  # Rename directory dir1 to dir2.
```


<span id="b59cd47f"></span>
### Delete a file or directory


* The following command deletes the file `file3`.


```JSON
hdfs dfs -rm tos://bucket1/file3   # Delete file file3.
```



* The following command deletes the directory `dir2` and recursively deletes all its subfiles and subdirectories.

   The `-r` option means recursive deletion.


```JSON
hdfs dfs -rm -r tos://bucket1/dir2  #Delete directory dir2 and recursively remove all its subfiles and subdirectories. The -r option stands for recursive deletion.
```
