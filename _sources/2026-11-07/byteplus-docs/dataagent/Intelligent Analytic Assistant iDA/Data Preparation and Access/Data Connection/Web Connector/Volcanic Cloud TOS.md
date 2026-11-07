---
title: "Volcanic Cloud TOS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Volcanic_Cloud_TOS__"
---

<span id="9cad3b81"></span>
# 1. Overview

Data connection supports access to Volcanic Cloud TOS.

<span id="e47c0577"></span>
# 2. Quick start

Here are two ways to create a volcanic cloud TOS data connection.

<span id="a117a519"></span>
## 2.1 Create a new data connection

(1) Enter the Volcano Engine, click to enter a specific project, click Data Preparation, find the data connection in the drop\-down list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select Volcanic Cloud TOS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44c27165fe79463782bf7c8ba5cc3439~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/031bab506c4b40a28d8d2a540c1f7610~tplv-goo7wpa0wc-image.image) </span>

**Data connection parameter description:** 


* Server: corresponding to the access domain name of S3Endpoint, and add https://in front of it, for example, TOS Beijing corresponds to https://tos\-s3\-cn\-beijing.volces.com

* Username: corresponding accessId

* Password: Corresponding accessKey

* Bucket name: the name of the bucket

* File format: optional csv, txt

* Table type: optional partitioned table (divided into yyyMMdd and yyyy\-MM\-dd), non\-partitioned table

* File directory: that is, the path corresponding to the table, be careful not to start with/when filling in here.


(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(6) Enter a keyword search and select the newly created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/890373dcd4b9416b9a3ec84ba14e670b~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="7760bd59"></span>
## 2.2 Creating a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting Data Connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with **steps (2) and (3) of 2.1** above. After completing the configuration, it will stop in the pop\-up box of the dataset selection data connection, and you can directly proceed to the next step of dataset creation.

<span id="74860be5"></span>
## 2.3 Description of directory structure


* **Non\-partitioned table**


Table name: student_np

```Plain
student_np              // The directory corresponding to the table name
├── student.txt         // Data file, type specified in the data connection, will read all data files of that type in the folder
├── student2.txt 
└── student_np.yml      // schema file,whose name must be consistent with the table name
```



* **Partition table**


Table name: student_p1

```Plain
student_p1              // The directory corresponding to the table name
├── 20240909            // partition
│   ├── _SUCCESS        // success file
│   ├── student.csv     // Data file, type specified in the data connection, will read all data files of that type in the folder
│   ├── student2.csv
│   └── student3.csv    
├── 20240910
│   ├── _SUCCESS
│   ├── student.csv
│   ├── student2.csv
│   └── student3.csv
└── student_p1.yml      // schema file,whose name must be consistent with the table name
```


<span id="72e0c7b0"></span>
## 2.4 Detailed description of the rules


1. **File directory format** : Required, such as data/student

   1. Rule 1: The last directory name must be the same as the table name, in the format data/{tableName}, such as data/student

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data file is located. If there is one, the system will automatically skip it.

   3. Rule 3: It is not recommended to change the file directory. Please update the [DataWind\- Data Connection] configuration item before changing to avoid abnormal data query.

   4. Rule 4: A file directory represents a table, and it is not supported to share a file directory with multiple tables, nor to have multiple directories for a table

2. **File directory content:** 

   1. **Data file** : Required, only support CSV, TXT, can have multiple files, name is not limited

      1. Rule 1: The order of columns (fields) in the data file must be consistent with the metadata file, and the data file does not contain a header (field name line).

      2. Rule 2: Each time you query, pull all the data according to the file directory address (excluding subdirectory files)

      3. Rule 3: The total file size in a single file directory is recommended to be less than 500G.

      4. Rule 4: CSV is best for databases and other systems to directly export files, do not re\-edit, which may cause abnormal date types

   2. **Meta information file** : Required, {tableName} .yml (if there are structural changes, you need to change this file), directly in the directory corresponding to the table name

      1. Rule 1: Use to parse data files mapped to structured tables

      2. Rule 2: {tableName} is the table name, table name change is not supported, {tableName} needs to be consistent with the directory name

      3. Rule 3: If it is a partition table, the partition field does not need to be written in the meta information file, the system will automatically add aeolus_partition field as partition

      4. Rule 4: See Appendix for file format

   3. **Synchronization success flag file** : partition table required, do not fill in the non\-partition table, the file name is _SUCCESS, no suffix, placed in the corresponding partition directory

      1. Logic: used to mark whether the data is pushed, used to build dependency logic on S3 tasks

      2. Rule 1: The file must exist. When the task is executed, read the _SUCCESS under the corresponding partition to determine whether the data of the corresponding business date is ready
