---
title: "Alibaba Cloud OSS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Alibaba_Cloud_OSS_"
---

The system supports access to Alibaba Cloud OSS. This article introduces how to access Alibaba Cloud OSS.

<span id="8cba1844"></span>
# Conditions of use

Users need to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to use this function.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="93e4a000"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **Alibaba Cloud OSS** on the **data connection** interface.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29627320b0744ab9ab280ed13073f248~tplv-goo7wpa0wc-image.image) </span>


3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ea712d03dc048c6a0515dd3ab7544b8~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |explain |
   |---|---|
   |server |Corresponding to the access domain name of S3Endpoint, and add https://in front of it, for example, OSS Beijing corresponds to http://oss\-cn\-beijing.aliyuncs.com |
   |user name |Corresponding AccessID |
   |password |Corresponding AccessKey |
   |bucket name |OSS bucket name |
   |file format |Optional csv, txt |
   |Table type |Optional partitioned tables (divided into yyyMMdd and yyyy\-MM\-dd), non\-partitioned tables |
   |file directory |That is, the path corresponding to the table, be careful not to start with/when filling in here.<br><br><br>1. **File directory format** : Required, such as data/student<br><br>   1. Rule 1: The last directory name must be the same as the table name, in the format data/{tableName}, such as data/student<br><br>   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data file is located. If there is one, the system will automatically skip it.<br><br>   3. Rule 3: It is not recommended to change the file directory. Please update the [DataWind\- Data Connection] configuration item before changing to avoid abnormal data query.<br><br>   4. Rule 4: A file directory represents a table, and multiple tables sharing a file directory is not supported, nor is it supported to have multiple directories for a table<br><br>2. **File directory content:** <br><br>   1. **Data file:**  Required, only support CSV, TXT, can have multiple files, name is not limited<br><br>      1. Rule: The order of columns (fields) in the data file must be consistent with the metadata file, and the data file does not contain a header (field name line).<br><br>      2. Rule: Each time you query, pull all the data according to the file directory address (excluding subdirectory files)<br><br>      3. Rule: The total file size in a single file directory is recommended to be less than 500G.<br><br>      4. Rule: CSV is best for databases and other systems to directly export files, do not re\-edit, which may cause abnormal date types<br><br>   2. **Meta information file:**  Required, {tableName} .yml (if there are structural changes, you need to change this file), directly in the directory corresponding to the table name<br><br>      1. Rule 1: Use to parse data files mapped to structured tables<br><br>      2. Rule 2: {tableName} is the table name, table name change is not supported, {tableName} needs to be consistent with the directory name<br><br>      3. Rule 3: If it is a partition table, the partition field does not need to be written in the meta information file, the system will automatically add aeolus_partition field as partition<br><br>      4. Rule 4: See Appendix for file format<br><br>   3. **Synchronization success flag file:**  Partition table is required, do not fill in the non\-partition table, the file name is _SUCCESS, no suffix, placed in the corresponding partition directory<br><br>      1. Logic: used to mark whether the data is pushed, used to build dependency logic on S3 tasks<br><br>      2. Rule 1: The file must exist. When the task is executed, read the _SUCCESS under the corresponding partition to determine whether the data of the corresponding business date is ready |
   

4. Click **Test Connection** and click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b40273ab8e947149458df7031058799~tplv-goo7wpa0wc-image.image) </span>

5. After confirming that the basic information of the data connection is correct, the data connection is completed.


<span id="0d0f96f9"></span>
# Directory structure description


* **Non\-partitioned table**


Table name: student_np

```Plain
student_np              // The directory corresponding to the table name
├── student.txt         // Data file, type specified in the data connection, will read all data files of that type in the folder
├── student2.txt 
└── student_np.yml      // schema file, whose name must be same as the table name
```



* **Partition table**


Table name: student_p1

```Plain
student_p1              // The directory corresponding to the table name
├── 20240909            // Partition
│   ├── _SUCCESS        // Success file
│   ├── student.csv     // Data file, type specified in the data connection, will read all data files of that type in the folder
│   ├── student2.csv
│   └── student3.csv    
├── 20240910
│   ├── _SUCCESS
│   ├── student.csv
│   ├── student2.csv
│   └── student3.csv
└── student_p1.yml      // schema file, whose name must be same as the table name
```
