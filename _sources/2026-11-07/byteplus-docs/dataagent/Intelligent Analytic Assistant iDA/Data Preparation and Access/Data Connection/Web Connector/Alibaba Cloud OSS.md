---
title: "Alibaba Cloud OSS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Alibaba_Cloud_OSS__"
---

<span id="12941145"></span>
# 1. Overview

Data connections support integration with Alibaba Cloud OSS.

<span id="f02dea15"></span>
# 2. Quick start

The following describes two methods for creating an Alibaba Cloud OSS data connection.

<span id="75c7fa23"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select OSS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c2174cb5fe641068c8f83eb284c6683~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a72ed282a3a24d45a1db679aa2aa8b06~tplv-goo7wpa0wc-image.image) </span>

**Data connection parameter description:** 


* Server: The access domain name corresponding to the S3 endpoint, with https:// added in front. For example, OSS Beijing corresponds to http://oss\-cn\-beijing.aliyuncs.com

* Username: Corresponds to accessId

* Password: Corresponds to accessKey

* Bucket name: The name of the bucket

* File format: Optional csv, txt

* Table type: Optional partitioned table (with yyyMMdd and yyyy\-MM\-dd formats) or non\-partitioned table

* File directory: The path corresponding to the table. Note that when filling in this field, do not start with /


(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b8e7d901fe748cbaad45f2ded1cbb1b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Enter keywords to search and select the previously created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e33939676b934884801484803e19f555~tplv-goo7wpa0wc-image.image" width="551px" /></div>


<span id="975d5e01"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0170127572df4e6c8eef8afea9335c67~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After completing the configuration, you will stay in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step to create the dataset.

<span id="7cbd5d4e"></span>
## 2.3 Directory structure description


* **Non\-partitioned table**


Table name: student_np

```Plain
student_np              // The directory corresponding to the table name
├── student.txt         // Data file, type specified in the data connection, will read all data files of that type in the folder
├── student2.txt 
└── student_np.yml      // schema file, whose name must be consistent with the table name
```



* **Partitioned table**


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
└── student_p1.yml      // schema file, whose name must be consistent with the table name
```


<span id="562baf1a"></span>
## 2.4 Detailed rule description


1. **File directory format**: Required, for example data/student

   1. Rule 1: The name of the last\-level directory must be consistent with the table name, in the format data/{tableName}, for example data/student

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data files are located. If present, the system will automatically skip them.

   3. Rule 3: It is not recommended to change the file directory. Before making any changes, please update the [DataWind\-Data Connection] configuration item to avoid data query errors.

   4. Rule 4: One file directory represents one table. Multiple tables sharing a single file directory are not supported, nor is a single table having multiple directories supported.

2. **File directory contents:** 

   1. **Data files:**  Required. Only CSV and TXT formats are supported. Multiple files are allowed, and there are no restrictions on file names.

      1. Rule 1: The column (field) order in the data files must be consistent with the metadata file, and the data files must not contain a header row (field names).

      2. Rule 2: For each query, all data is retrieved based on the file directory path (excluding files in subdirectories).

      3. Rule 3: The total size of files in a single file directory is recommended to be less than 500 GB.

      4. Rule 4: CSV files should preferably be exported directly from database systems or similar systems. Do not edit them after export, as this may cause date type errors.

   2. **Metadata file:**  Required. {tableName}.yml (if there are structural changes, this file needs to be modified), placed directly in the directory named after the table.

      1. Rule 1: Used to parse data files and map them to a structured table.

      2. Rule 2: {tableName} is the table name. Table name changes are not supported. {tableName} must match the directory name.

      3. Rule 3: For partitioned tables, partition fields do not need to be specified in the metadata file. The system will automatically add the aeolus_partition field as the partition.

      4. Rule 4: For the file format, see the appendix.

   3. **Synchronization success marker file:**  Required for partitioned tables; do not include for non\-partitioned tables. The file name is _SUCCESS, with no extension, and it should be placed in the corresponding partition directory.

      1. Logic: Used to indicate whether data has been fully uploaded and to construct dependency logic for S3 tasks.

      2. Rule 1: The file must exist. When the task is executed, the system reads the _SUCCESS file in the corresponding partition to determine whether the data for the relevant business date is ready.
