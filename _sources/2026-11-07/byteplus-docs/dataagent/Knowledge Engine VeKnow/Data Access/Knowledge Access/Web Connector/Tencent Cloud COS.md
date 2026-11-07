---
title: "Tencent Cloud COS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Tencent_Cloud_COS_"
---

Data connection supports access to Tencent Cloud COS. This article describes how to access Tencent Cloud COS.

<span id="8a30d13b"></span>
# Conditions of use

Users need to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to use this function.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="36bfab0a"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **Tencent Cloud COS** on the **data connection** interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec5dd55b58b6432f9a073a59a7c5b7b8~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0935a68fd3c49df8ac41a42faa132f4~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |explain |
   |---|---|
   |user name |Corresponding AccessID |
   |password |Corresponding AccessKey |
   |Region |Tencent cloud hosting room distribution area |
   |bucket name |bucket name |
   |file format |ocr |
   |Table type |Optional partitioned tables (divided into yyyMMdd and yyyy\-MM\-dd), non\-partitioned tables |
   |file directory |That is, the path corresponding to the table, be careful not to start with/when filling in here.<br><br><br>1. **File directory format** : Required, such as data/student<br><br>   1. Rule 1: The last directory name must be the same as the table name, in the format data/{tableName}, such as data/student<br><br>   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data file is located. If there is one, the system will automatically skip it.<br><br>   3. Rule 3: It is not recommended to change the file directory. Please update the [DataWind\- Data Connection] configuration item before changing to avoid abnormal data query.<br><br>   4. Rule 4: A file directory represents a table, and multiple tables sharing a file directory is not supported, nor is it supported to have multiple directories for a table<br><br>2. **File directory content:** <br><br>   1. **Data file** : Required, only ORC is supported, there can be multiple files, and the name is not limited<br><br>   2. **Synchronization success flag file** : partition table required, do not fill in the non\-partition table, the file name is _SUCCESS, no suffix, placed in the corresponding partition directory<br><br>      1. Logic: used to mark whether the data is pushed, used to build dependency logic on S3 tasks<br><br>      2. Rule 1: The file must exist. When the task is executed, read the _SUCCESS under the corresponding partition to determine whether the data of the corresponding business date is ready |
   

4. Click **Test Connection** and click **Save** after successful connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4538b34d3084b12ac397d6453421fce~tplv-goo7wpa0wc-image.image" width="2488px" />   </div>
   

5. After confirming that the basic information of the data connection is correct, the data connection is completed.


<span id="d3caafb9"></span>
# Directory structure description


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
│   ├── _SUCCESS        // Success file
│   ├── student.orc     // Data file, type specified in the data connection, will read all data files of that type in the folder
│   ├── student2.orc
│   └── student3.orc    
├── 20240910
│   ├── _SUCCESS
│   ├── student.orc
│   ├── student2.orc
│   └── student3.orc
```
