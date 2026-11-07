---
title: "Tencent Cloud COS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Tencent_Cloud_COS__"
---

<span id="f86056c4"></span>
# 1. Overview

Data connection supports access to Tencent Cloud COS.

<span id="36d68c28"></span>
# 2. Quick start

Here are two ways to create a Tencent Cloud COS data connection.

<span id="f736066c"></span>
## 2.1 Create a new data connection

(1) Enter the Volcano Engine, click to enter a specific project, click Data Preparation, find the data connection in the drop\-down list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select Tencent Cloud COS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ab5e5f7fd174502b67e2ad77de6b575~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05fc60f658b74e0d82a048c5cb09cfbf~tplv-goo7wpa0wc-image.image) </span>

**Data connection parameter description:** 


* Username: corresponding accessId

* Password: Corresponding accessKey

* Region: The distribution area of Tencent's cloud hosting room

* Bucket name: the name of the bucket

* File format: ORC

* Table type: optional partitioned table (divided into yyyMMdd and yyyy\-MM\-dd), non\-partitioned table

* File directory: that is, the path corresponding to the table, be careful not to start with/when filling in here


(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Enter a keyword search and select the newly created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85296b004d0e44b3b674f44cc38d0e20~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="7f4c288f"></span>
## 2.2 Creating a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting Data Connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a35ead73c655416aabcdcc9450272a85~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After completing the configuration, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<span id="dc5d7dbb"></span>
## 2.3 Description of directory structure


* **Non\-partitioned table**


Table name: student_np

```Plain
student_np              // The directory corresponding to the table name
├── student.orc         // Data file, type specified in the data connection, will read all data files of that type in the folder
├── student2.orc
```



* **Partition table**


Table name: student_p1

```Plain
student_p1              // The directory corresponding to the table name
├── 20240909            // partition
│   ├── _SUCCESS        // success file
│   ├── student.orc     // Data file, type specified in the data connection, will read all data files of that type in the folder
│   ├── student2.orc
│   └── student3.orc    
├── 20240910
│   ├── _SUCCESS
│   ├── student.orc
│   ├── student2.orc
│   └── student3.orc
```


<span id="121405ef"></span>
## 2.4 Detailed description of the rules


1. **File directory format** : Required, such as data/student

   1. Rule 1: The last directory name must be the same as the table name, in the format data/{tableName}, such as data/student

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data file is located. If there is one, the system will automatically skip it.

   3. Rule 3: It is not recommended to change the file directory. Please update the [DataWind\- Data Connection] configuration item before changing to avoid abnormal data query.

   4. Rule 4: A file directory represents a table, and it is not supported to share a file directory with multiple tables, nor to have multiple directories for a table

2. **File directory content:** 

   1. **Data file** : Required, only ORC is supported, there can be multiple files, and the name is not limited

   2. **Synchronization success flag file** : partition table required, do not fill in the non\-partition table, the file name is _SUCCESS, no suffix, placed in the corresponding partition directory

      1. Logic: used to mark whether the data is pushed, used to build dependency logic on S3 tasks

      2. Rule 1: The file must exist. When the task is executed, read the _SUCCESS under the corresponding partition to determine whether the data of the corresponding business date is ready
