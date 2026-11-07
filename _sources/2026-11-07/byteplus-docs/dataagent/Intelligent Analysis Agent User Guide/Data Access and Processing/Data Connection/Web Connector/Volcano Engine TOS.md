---
title: "Volcano Engine TOS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Volcano_Engine_TOS"
---

<span id="fbea142e"></span>
# 1. Overview

Data connections support integration with BytePlus TOS.

<span id="853f11a9"></span>
# 2. Quick start

The following describes two methods for creating a BytePlus TOS data connection.

<span id="7b2e6e7b"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select BytePlus TOS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e75c21090a8a4bfc8cfde4b0cb085108~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b9bf05e65644a22b490ec9405adfeb2~tplv-goo7wpa0wc-image.image) </span>

**Data connection parameter description:** 


* Server: Corresponds to the access domain name of S3Endpoint, with https:// added at the beginning. For example, TOS Beijing corresponds to https://tos\-s3\-cn\-beijing.volces.com

* Username: Corresponds to accessId

* Password: Corresponds to accessKey

* Bucket name: Enter the name of the bucket.

* File format: Optional csv, txt

* Table type: Partitioned table (with yyyMMdd and yyyy\-MM\-dd as options), or non\-partitioned table.

* File directory: The path corresponding to the table. Note: Do not start with / when entering this value.


(4) Once you have confirmed the basic information, the data connection is complete.

(5) You can use this connection to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Enter keywords to search and select the previously created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a499671958e48699c864db0c7055e65~tplv-goo7wpa0wc-image.image" width="606px" /></div>


<span id="391566cc"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After completing the configuration, the pop\-up window for selecting a data connection for the dataset will remain open, allowing you to proceed directly to the next step to create the dataset.

<span id="b8e28e45"></span>
## 2.3 Directory structure description


* **Non\-partitioned table**


Table name: student_np

```Plain
student_np              // 表名对应的目录
├── student.txt         // 数据文件，类型在数据连接中指定，会读取到文件夹下所有该类型的数据文件
├── student2.txt 
└── student_np.yml      // schema文件，名字需要和表名一致
```



* **Partitioned table**


Table name: student_p1

```Plain
student_p1              // 表名对应的目录
├── 20240909            // 分区
│   ├── _SUCCESS        // 成功标志文件
│   ├── student.csv     // 数据文件，类型在数据连接中指定，会读取到文件夹下所有该类型的数据文件
│   ├── student2.csv
│   └── student3.csv    
├── 20240910
│   ├── _SUCCESS
│   ├── student.csv
│   ├── student2.csv
│   └── student3.csv
└── student_p1.yml      // schema文件，名字需要和表名一致
```


<span id="f60cc9de"></span>
## 2.4 Detailed rule description


1. **File directory format**: Required, for example data/student

   1. Rule 1: The name of the last\-level directory must be consistent with the table name, in the format data/{tableName}, for example data/student

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data files are located. If present, the system will automatically skip them.

   3. Rule 3: Changing the file directory is not recommended. Before making any changes, update the [DataWind\-data connection] configuration item to avoid data query exceptions.

   4. Rule 4: Each file directory represents a single table. Sharing a file directory among multiple tables is not supported, nor is assigning multiple directories to a single table.

2. **File directory contents:** 

   1. **Data files**: Required. Only CSV and TXT formats are supported. Multiple files are allowed, and there are no restrictions on file names.

      1. Rule: The column (field) order in the data files must be consistent with the metadata file, and the data files must not contain a header row (field names).

      2. Rule: For each query, all data is retrieved based on the file directory address (excluding files in subdirectories).

      3. Rule: The total size of files in a single file directory is recommended to be less than 500 GB.

      4. Rule: CSV files should preferably be exported directly from systems such as databases. Do not edit them a second time, as this may cause date type anomalies.

   2. **Metadata file**: Required. {tableName}.yml (if there are structural changes, modify this file), placed directly in the directory corresponding to the table name.

      1. Rule 1: Used to parse data files and map them to structured tables.

      2. Rule 2: {tableName} is the table name. Table name changes are not supported. {tableName} must match the directory name.

      3. Rule 3: For partitioned tables, partition fields do not need to be written in the metadata file. The system will automatically add the aeolus_partition field as the partition.

      4. Rule 4: See the appendix for file format.

   3. **Synchronization success marker file**: Required for partitioned tables. Do not provide for non\-partitioned tables. The file name is _SUCCESS, with no suffix, and it is placed in the corresponding partition directory.

      1. Logic: Used to indicate whether data has been fully pushed and to construct dependency logic for S3 tasks.

      2. Rule 1: The file must exist. When executing a task, the system reads _SUCCESS in the corresponding partition to determine whether the data for the relevant business date is ready.
