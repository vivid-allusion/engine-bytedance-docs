---
title: "Overview of Dataset Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Dataset_Management"
---

The dataset interface includes dataset creation, dataset management, and dataset list. Among these, "dataset management" is the details management module, supporting operations such as data preview, synchronization status monitoring, viewing model information, and setting row and column permissions. This document introduces how to use some features in the dataset management overview section.

<span id="_1-数据集管理概述"></span>
# Feature overview

The entire dataset interface can be divided into three modules: 1. Dataset creation, 2. Dataset management, 3. Dataset list. As shown in the figure below, the green area labeled '2' represents dataset management. In this dataset management area, users can perform various operations, including previewing data, monitoring synchronization status, viewing model information, and setting row and column permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5548d5b3cf1f4402835d0b3770f5b533~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-数据集信息"></span>
# Dataset information

Basic dataset information: owner, dataset size, number of accesses in the past 7 days.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3de630d30c0946cf835db1f5a14198cd~tplv-goo7wpa0wc-image.image) </span>

The top section supports the following operations:


* Enable DataAgent analysis capability for the dataset. Only datasets with this capability enabled can be used for agent configuration.

* Permission assignment: Assign permissions to the dataset.

* Edit: Edit and modify dataset configuration.

* More:

   * Basic information: Supports modifying the dataset name, description, and usage instructions.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7207402d93dd40bf982470d99b5c5bb9~tplv-goo7wpa0wc-image.image) </span>

   * Transfer owner: Supports transferring the owner of the dataset. For details, see [Resource-Based Authorization](https://docs.byteplus.com/docs/dataagent/Resource-Based_Authorization).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2a77272a0f247fb8afd15d1ad657498~tplv-goo7wpa0wc-image.image) </span>

   * More: Includes data preview configuration, setting tags, and switching priority.

      
      |Features |Introduction |
      |---|---|
      |Data preview configuration |Supports selecting whether the default data preview interface displays detailed data or table structure.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38c312d2b36d4e93a8482858979aae8a~tplv-goo7wpa0wc-image.image) </span> |
      |Set tags |Set dataset tags to facilitate dataset management. The assigned tags will be displayed next to the dataset name.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e5a2e6a84c64ffcb1503e1df68b3773~tplv-goo7wpa0wc-image.image) </span> |
      |Switch priority |Supports setting the synchronization priority for datasets. Tasks with higher priority will be synchronized first during system peak periods. For details, see [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Setting).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/240335c82ec14e909e5557556b02a0d3~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only data with a extract connection supports switching priority.</div><br> |
      

* Move, copy, and delete datasets.


<span id="_2-2-数据预览"></span>
# Data preview

<span id="399229c1"></span>
## View data


* Supports two preview types: detailed data and table structure.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">No data preview is available when synchronization fails.   </div>
   

   * Detailed data

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60a9394e69ab4dc2a588f44d3b52e9d1~tplv-goo7wpa0wc-image.image) </span>

   * Table structure

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fac61f150624a5d9954f1b24c0efce7~tplv-goo7wpa0wc-image.image) </span>

* Supports entering keywords to search for field names.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7687859ce1374590a72a9760e56e37f0~tplv-goo7wpa0wc-image.image) </span>

* Supports specifying filter conditions to preview target data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3c066871b8b48a4ab5e3d200f6c78a8~tplv-goo7wpa0wc-image.image) </span>

<span id="bc883af7"></span>
## Edit data


* Supports editing field information. Click "Edit field" to enter the field information editing mode. For more operation guidelines, see [Field Configuration](https://docs.byteplus.com/docs/dataagent/Field_Configuration).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dafd619cfc349259269d459decc681d~tplv-goo7wpa0wc-image.image) </span>


* Supports batch editing fields using Excel.

   1. Click the "More" button next to "Edit field", then click "Excel batch modify".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73a80bc080a84e60b9342b80ca68eb10~tplv-goo7wpa0wc-image.image) </span>


2. Supports downloading the latest field list as an Excel file. Users can modify field names, dimensions/metrics, field expressions, descriptions, remarks, and other content in Excel. After completing the modifications, upload the updated Excel file and confirm to apply the changes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7164202ff8648d9a574080861a78582~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  :::warning
  Do not fill in the ID for newly added fields. If modifying existing fields, ensure the ID matches the downloaded file.
  :::
```


<span id="_2-3-同步状态"></span>
# Synchronization status

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only "extracted" data can have its synchronization status viewed. For an introduction to direct connection and extraction, refer to <a href="https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection#b2925a8e">Supported connection methods</a>.</div>



* Supports viewing the execution view and logs of historical synchronization tasks to monitor progress in real time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb240a075cdd4b2f8040855a5595bb26~tplv-goo7wpa0wc-image.image) </span>

   Supports filtering tasks by specific business date, synchronization status, and tasks with data results equal to 0. The filtering criteria are explained as follows:

   
   |Filtering criteria |Note |
   |---|---|
   |Business date |A specific date range can be specified for filtering. By default, synchronization tasks from the past six months are displayed. |
   |Synchronization status |Includes statuses such as not ready, waiting for execution, in progress, successful, failed, terminated, and system canceled. By default, all statuses are displayed. |
   |The number of result rows is 0 |Filter out tasks whose data synchronization result is 0 to facilitate troubleshooting data anomalies or empty value issues. |
   

* Supports single instance resynchronization and batch data synchronization.

   * Single instance resynchronization


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c7e3e3dcf4e4d6b8b2f5bd16c4ff4a7~tplv-goo7wpa0wc-image.image) </span>


* Batch data synchronization

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9405381521954f688dd27d689c342586~tplv-goo7wpa0wc-image.image) </span>

   The relevant parameter configuration instructions are as follows:

   
   |Parameters |Description |
   |---|---|
   |Selection range |* Select the start and end time of the business date to be synchronized, and the data within this business date range will be synchronized in bulk immediately.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/034edac11d374569a1b4d0c8b4f7073f~tplv-goo7wpa0wc-image.image) </span><br><br>* If you select "After synchronization is enabled, the synchronization status list displays this time range", the execution information for this period will be shown in the list.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b63a59fdc994cea86ae7b85592e3a39~tplv-goo7wpa0wc-image.image) </span> |
   |Dependency check |You can choose to execute the data synchronization task based on dependencies or execute it immediately. For an introduction to dependency configuration, please refer to [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Setting). |
   

* Supports viewing and modifying detailed synchronization configurations. For more operation instructions, see [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Setting).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5d7897d294343efb9b4aef0830c32fd~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-4-模型信息"></span>
# Model information

View model settings: model composition, filtering criteria, and performance settings. Click the Capsule element to view specific field information. For more operation instructions, see [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/322f05d8c8c941fba1cd61de933ab808~tplv-goo7wpa0wc-image.image) </span>

<span id="177c6d21"></span>
# Row and column permissions

Set dataset row and column permissions. For details, refer to [Data Row and Column Permissions](https://docs.byteplus.com/docs/dataagent/Data_Row_and_Column_Permissions).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8b53332b3c44171be871aa941fc7690~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3df6cd5da1d2457196cf03b63b3c4a59~tplv-goo7wpa0wc-image.image) </span>
