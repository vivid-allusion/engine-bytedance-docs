---
title: "Alibaba Cloud OSS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Alibaba_Cloud_OSS"
---

<span id="a26b0727"></span>
# 1. Overview

Data connections support integration with Alibaba Cloud OSS.

<span id="ffc09798"></span>
# 2. Quick start

The following describes two methods for creating an Alibaba Cloud OSS data connection.

<span id="9ae98239"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, navigate to a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select OSS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c2174cb5fe641068c8f83eb284c6683~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a72ed282a3a24d45a1db679aa2aa8b06~tplv-goo7wpa0wc-image.image) </span>

**Description of data connection parameters:** 


* Server: The access domain name corresponding to the S3 endpoint, with https:// added in front. For example, OSS Beijing corresponds to http://oss\-cn\-beijing.aliyuncs.com

* Username: Corresponds to accessId

* Password: Corresponds to accessKey

* Bucket name: The bucket name

* File format: Optional csv or txt

* Table type: Optional partitioned table (with yyyMMdd and yyyy\-MM\-dd formats), or non\-partitioned table

* File directory: The path corresponding to the table. Note that when filling in this field, do not start with /


(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection to create a dataset: Click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b8e7d901fe748cbaad45f2ded1cbb1b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Enter keywords to search, and select the previously created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e33939676b934884801484803e19f555~tplv-goo7wpa0wc-image.image" width="551px" /></div>


<span id="a242482a"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0170127572df4e6c8eef8afea9335c67~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) in 2.1**. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, and can proceed directly to the next step of dataset creation.

<span id="6d7ad71d"></span>
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


<span id="4c62e8de"></span>
## 2.4 Detailed rule description


1. **File directory format**: Required, for example data/student

   1. Rule 1: The name of the final directory must be consistent with the table name, in the format data/{tableName}, for example data/student

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data files are located. If present, the system will automatically skip them.

   3. Rule 3: It is not recommended to change the file directory. Before making any changes, please update the [DataWind\-data connection] configuration item to avoid data query exceptions.

   4. Rule 4: Each file directory represents a single table. Sharing a file directory among multiple tables is not supported, nor is assigning multiple directories to a single table.

2. **File directory contents:** 

   1. **Data files:**  Required. Only CSV and TXT formats are supported. Multiple files are allowed, and there are no restrictions on file names.

      1. Rule: The order of columns (fields) in the data files must be consistent with the metadata file, and the data files must not include a header row (field names).

      2. Rule: For each query, all data is retrieved based on the file directory address (excluding files in subdirectories).

      3. Rule: The total size of files in a single file directory is recommended to be less than 500 GB.

      4. Rule: CSV files should preferably be exported directly from database or similar systems. Do not edit them a second time, as this may cause date type anomalies.

   2. **Metadata file:**  Required. {tableName}.yml (If there are structural changes, this file must be modified). Place it directly in the directory corresponding to the table name.

      1. Rule 1: Used to parse data files and map them to structured tables.

      2. Rule 2: {tableName} is the table name. Table name changes are not supported. {tableName} must match the directory name.

      3. Rule 3: For partitioned tables, partition fields do not need to be written in the metadata file. The system will automatically add the aeolus_partition field as the partition.

      4. Rule 4: See appendix for file format.

   3. **Synchronization success marker file:**  Required for partitioned tables. Do not include for non\-partitioned tables. The file name is _SUCCESS, with no suffix, and it should be placed in the corresponding partition directory.

      1. Logic: Used to indicate whether data has been successfully pushed and to build dependency logic for S3 tasks.

      2. Rule 1: The file must exist. When executing a task, the system reads the _SUCCESS file in the corresponding partition to determine whether the data for the relevant business date is ready.
