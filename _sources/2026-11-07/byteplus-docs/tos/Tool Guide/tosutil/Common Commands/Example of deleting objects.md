---
title: "Example of deleting objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Example_of_deleting_objects"
---

This article uses the macOS system as an example to introduce common command examples for deleting objects with the tosutil tool.

<span id="示例存储桶对象说明"></span>
## Description of example bucket objects

The example bucket named **bucketname** contains the following objects:

```Plain
tos://bucketname/file1.txt
tos://bucketname/file2.txt
tos://bucketname/file3.txt
tos://bucketname/file4.txt
tos://bucketname/file5.txt
tos://bucketname/file6.txt
tos://bucketname/folder1/
tos://bucketname/folder1/file7.txt
tos://bucketname/folder2/
tos://bucketname/folder2/file8.txt
tos://bucketname/folder2/folder3/
tos://bucketname/folder2/folder3/file9.txt
```


<span id="常见示例"></span>
## Common examples

Based on the example bucket objects description, sample commands for different deletion scenarios are as follows.

<span id="5832702d"></span>
### Delete a specific file

Delete the **file1.txt** file from the **bucketname** bucket:

```Plain
./tosutil rm tos://bucketname/file1.txt
```


<span id="17a0eb35"></span>
### Delete a specific folder

Delete the **folder2** folder from the **bucketname** bucket:

```Plain
./tosutil rm tos://bucketname/folder2/ -r
```


<span id="081afa12"></span>
### Delete files with the specified prefix

Delete all files and folders with the prefix **folder** in the **bucketname** bucket:

```Plain
./tosutil rm tos://bucketname/folder -r
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The above command will delete both <strong>folder1/</strong> and <strong>folder2/</strong> folders!</div>
