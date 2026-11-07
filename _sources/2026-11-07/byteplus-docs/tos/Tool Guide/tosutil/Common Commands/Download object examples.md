---
title: "Download object examples"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download_object_examples"
---

This article uses macOS as an example to introduce common commands for downloading objects using the tosutil tool.

<span id="示例存储桶说明"></span>
## Example bucket description

The example bucket named **bucketname** contains the following objects:

```Plain
tos://bucketname/file1.txt
tos://bucketname/file2.txt
tos://bucketname/pic1.png
tos://bucketname/pic2.png
tos://bucketname/pic3.jpg
tos://bucketname/pic4.jpg
tos://bucketname/folder1/
tos://bucketname/folder1/file7.txt
tos://bucketname/folder2/
tos://bucketname/folder2/file8.txt
tos://bucketname/folder2/folder3/
tos://bucketname/folder2/folder3/file9.txt
```


<span id="常见实例"></span>
## Common examples

Based on the objects in the example bucket, example commands for different download scenarios are as follows.

<span id="21f1b482"></span>
### Download a specified object from the bucket to a local folder

Download the **file1.txt** file from the **bucketname** bucket to the local **folder1** folder:

```Plain
./tosutil cp tos://bucketname/file1.txt /folder1
```


After the download is complete, the generated local file is:

```Plain
└── folder1
    └── file1.txt
```


<span id="c8f4f754"></span>
### Download a specified object from the bucket to a local folder and rename it

Download the **file1.txt** file from the **bucketname** bucket to the local **folder1** folder:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the local <strong>folder1</strong> folder does not contain the <strong>file1_renamed.txt</strong> file, download it directly and name it <strong>file1_renamed.txt</strong> after downloading; if the <strong>folder1</strong> folder already contains <strong>file1_renamed.txt</strong>, overwrite it with the content of <strong>file1.txt</strong> when downloading.</div>


```Plain
./tosutil cp tos://bucketname/file1.txt /folder1/file1_renamed.txt
```


After the download is complete, the local files are:

```Plain
└── folder1
    └── file1_renamed.txt
```


<span id="9c00858a"></span>
### Download a specified folder (including the folder itself) from the bucket

Download all files and folders in the **folder2** folder in the **bucketname** bucket (**including the folder2 folder itself**) to the local **folder1** folder:

```Plain
./tosutil cp tos://bucketname/folder2 /folder1 -r
```


After the download is complete, the locally generated files are:

```Plain
└── folder1
    └── folder2
        ├── file8.txt
        └── folder3
            └── file9.txt
```


<span id="de0367f0"></span>
### Download a specified folder from the bucket (excluding the folder itself)

Download all files and folders in the **folder2** folder in the **bucketname** bucket (**excluding the folder2 folder itself**) to the local **folder2_renamed** folder:

```Plain
./tosutil cp tos://bucketname/folder2 /folder2_renamed -r -flat
```


After the download is complete, the locally generated files are:

```Plain
└── folder2_renamed
    ├── file8.txt
    └── folder3
        └── file9.txt
```


<span id="eec49a4b"></span>
### Download all files in the bucket

Download all files in the **bucketname** bucket to the **folder0** folder:

```Plain
./tosutil cp tos://bucketname /folder0 -r
```


The locally generated files after download are:

```Plain
└── folder0
    ├── file1.txt
    ├── file2.txt
    ├── pic1.png
    ├── pic2.png
    ├── pic3.jpg
    ├── pic4.jpg
    ├── folder1
        └── file7.txt
    └── folder2
        ├── file8.txt
        └── folder3
            └── file9.txt
```


<span id="a9b01dbc"></span>
### Download files from the storage bucket that meet the criteria

Download all  **.txt** and **pi?1.png** files in the **bucketname** bucket to the **folder0** folder:

```Plain
./tosutil cp tos://bucketname /folder0 -r -include=*.txt#*pi?1.png
```


The locally generated files after download are:

```Plain
└── folder0
    ├── file1.txt
    ├── file2.txt
    ├── pic1.png
    ├── folder1
        └── file7.txt
    └── folder2
        ├── file8.txt
        └── folder3
            └── file9.txt
```


&nbsp;
