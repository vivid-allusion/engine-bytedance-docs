---
title: "Tencent Cloud COS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Tencent_Cloud_COS"
---

<span id="97b248a2"></span>
# 1. Overview

Data connections support integration with Tencent Cloud COS.

<span id="0576c405"></span>
# 2. Quick start

The following describes two methods for creating a Tencent Cloud COS data connection.

<span id="e8c3e61f"></span>
## 2.1 Create via data connection

(1) Log in to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select Tencent Cloud COS on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f36d1933da454267895ae5151314e83e~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4d4becbb36d4fdda64f38a6db7e8300~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


**Description of data connection parameters:** 


* Username: corresponds to accessId

* Password: corresponds to accessKey

* Region: The geographic location of Tencent Cloud's hosted data centers

* Bucket name: bucket name

* File format: ORC

* Table type: partitioned table (yyyMMdd or yyyy\-MM\-dd format) or non\-partitioned table

* File directory: the path corresponding to the table. Caution: Do not start with / when entering this value.


(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection to create a dataset: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e79529fb358a48a492e475f66634826c~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Enter keywords to search and select the previously created data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ecb2ad8f29a45c1ad6dbd90a642d5fc~tplv-goo7wpa0wc-image.image" width="568px" /></div>


<span id="d02dbe41"></span>
## 2.2 Create from dataset

(1) Log in to BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70b741b0f375400e9a5590f1d92d1b08~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the "Other" button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step to create the dataset.

<span id="7216d6b8"></span>
## 2.3 Directory structure description


* **Non\-partitioned table**


Table name: student_np

```Plain
student_np              // 表名对应的目录
├── student.orc         // 数据文件，类型在数据连接中指定，会读取到文件夹下所有该类型的数据文件
├── student2.orc
```



* **Partitioned table**


Table name: student_p1

```Plain
student_p1              // 表名对应的目录
├── 20240909            // 分区
│   ├── _SUCCESS        // 成功标志文件
│   ├── student.orc     // 数据文件，类型在数据连接中指定，会读取到文件夹下所有该类型的数据文件
│   ├── student2.orc
│   └── student3.orc    
├── 20240910
│   ├── _SUCCESS
│   ├── student.orc
│   ├── student2.orc
│   └── student3.orc
```


<span id="55d9bf4b"></span>
## 2.4 Detailed rule description


1. **File directory format**: Required, for example, data/student

   1. Rule 1: The name of the final directory must match the table name, with the format data/{tableName}, for example, data/student

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data files are located; if present, the system will automatically skip them.

   3. Rule 3: It is not recommended to change the file directory. Before making changes, update the [DataWind\-Data Connection] configuration item to avoid abnormal data queries.

   4. Rule 4: Each file directory represents a single table. Sharing a file directory among multiple tables is not supported, nor is assigning multiple directories to a single table.

2. **File directory contents:** 

   1. **Data files**: Required. Only ORC is supported. Multiple files are allowed, and there are no restrictions on file names.

   2. **Synchronization success marker file**: Required for partitioned tables; do not include for non\-partitioned tables. The file name is _SUCCESS, with no suffix, and it must be placed in the corresponding partition directory.

      1. Logic: Used to indicate whether data push is complete and to build dependency logic for S3 tasks.

      2. Rule 1: The file must exist. When the task is executed, the presence of _SUCCESS in the corresponding partition is checked to determine whether the data for the relevant business date is ready.
