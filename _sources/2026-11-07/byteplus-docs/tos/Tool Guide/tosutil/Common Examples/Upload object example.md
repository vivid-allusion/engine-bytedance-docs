---
title: "Upload object example"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-example"
---

This article uses macOS as an example to introduce common example commands for uploading objects with the tosutil tool.

<span id="示例文件夹说明"></span>
## Example folder description

The format description of the local example folder is as follows:

```Plain
└── folder1
    ├── folder2
        ├── file1.txt
        └── file2.txt
    └── file3.txt
    ├── folder3
    ├── folder4
        ├── file4.txt
        └── file5.txt
        └── pic1.png
        └── pic2.png
        └── pic3.jpg
        └── pic4.jpg
```


<span id="常见示例"></span>
## Common examples

Based on the example folder description, the example commands for different upload scenarios are as follows.

<span id="c42b7b88"></span>
### Upload a specified local file

Upload the **file3.txt** file under the local **folder1** folder to the root directory of the **bucketname** bucket:

```Plain
./tosutil cp /folder1/file3.txt tos://bucketname
```


After a successful upload, the generated object in the bucket is:

```Plain
tos://bucketname/file3.txt
```


<span id="ea0d7fda"></span>
### Upload specified local file and rename

Upload the **folder1** folder's **file3.txt** file from local to the root directory of the **bucketname** bucket and rename it to **aaa.txt**:

```Plain
./tosutil cp /folder1/file3.txt tos://bucketname/aaa.txt
```


After successful upload, the object generated in the bucket is:

```Plain
tos://bucketname/aaa.txt
```


<span id="e3fa5b2c"></span>
### Upload specified local file to the specified directory in the storage bucket

Upload the **folder1** folder's **file3.txt** file from local to the **folder** folder in the **bucketname** bucket:

```Plain
./tosutil cp /folder1/file3.txt tos://bucketname/folder/
```


After successful upload, the object generated in the bucket is:

```Plain
tos://bucketname/folder/file3.txt
```


<span id="145bddc0"></span>
### Upload local folder (including the folder itself)

Upload all files in the local **folder2** folder (**including the folder2 folder itself**) to the root directory of the **bucketname** bucket:

```Plain
./tosutil cp /folder1/folder2 tos://bucketname -r
```


After successful upload, the object generated in the bucket is:

```Plain
tos://bucketname/folder2/
tos://bucketname/folder2/file1.txt
tos://bucketname/folder2/file2.txt
```


<span id="2c7111d3"></span>
### Upload local folder to the specified directory in the storage bucket (including the folder itself)

Upload all files and folders in the local **folder1** folder (**including the folder1 folder itself**) to the **folder0** folder in the **bucketname** bucket:

```Plain
./tosutil cp /folder1 tos://bucketname/folder0 -r
```


After successful upload, the objects created in the bucket are:

```Plain
tos://bucketname/folder0/folder1/
tos://bucketname/folder0/folder1/folder2/
tos://bucketname/folder0/folder1/folder2/file1.txt
tos://bucketname/folder0/folder1/folder2/file2.txt
tos://bucketname/folder0/folder1/folder3/
tos://bucketname/folder0/folder1/file3.txt
tos://bucketname/folder0/folder1/folder4/file4.txt
tos://bucketname/folder0/folder1/folder4/file5.txt
tos://bucketname/folder0/folder1/folder4/pic1.png
tos://bucketname/folder0/folder1/folder4/pic2.png
tos://bucketname/folder0/folder1/folder4/pic3.jpg
tos://bucketname/folder0/folder1/folder4/pic4.jpg
```


<span id="2ea18b14"></span>
### Upload the local folder to the specified directory in the storage bucket (excluding the folder itself)

Upload all files and folders in the local **folder1** folder (**excluding the folder1 folder itself**) to the **folder0** folder in the **bucketname** bucket:

```Plain
./tosutil cp /folder1 tos://bucketname/folder0 -r -flat
```


After successful upload, the objects created in the bucket are:

```Plain
tos://bucketname/folder0/
tos://bucketname/folder0/folder2/
tos://bucketname/folder0/folder2/file1.txt
tos://bucketname/folder0/folder2/file2.txt
tos://bucketname/folder0/folder3/
tos://bucketname/folder0/file3.txt
tos://bucketname/folder0/folder4/file4.txt
tos://bucketname/folder0/folder4/file5.txt
tos://bucketname/folder0/folder4/pic1.png
tos://bucketname/folder0/folder4/pic2.png
tos://bucketname/folder0/folder4/pic3.jpg
tos://bucketname/folder0/folder4/pic4.jpg
```


<span id="116781bf"></span>
### Upload files with specified names from the local folder

Upload all  **.txt** and **pi?1.png** files from the local **folder4** folder to the **bucketname** bucket:

```Plain
./tosutil cp /folder4 tos://bucketname -r -include=*.txt#*pi?1.png
```


After successful upload, the objects created in the bucket are:

```Plain
tos://bucketname/file4.txt
tos://bucketname/file5.txt
tos://bucketname/pic1.png
```


<span id="ad772c79"></span>
### Upload files meeting the specified conditions from the local folder

Upload all files except  **.png** from the local **folder4** folder to the **bucketname** bucket:

```Plain
./tosutil cp /folder4 tos://bucketname -r -exclude=*.png
```


After successful upload, the objects created in the bucket are:

```Plain
tos://bucketname/file4.txt
tos://bucketname/file5.txt
tos://bucketname/pic3.jpg
tos://bucketname/pic4.jpg
```


&nbsp;
