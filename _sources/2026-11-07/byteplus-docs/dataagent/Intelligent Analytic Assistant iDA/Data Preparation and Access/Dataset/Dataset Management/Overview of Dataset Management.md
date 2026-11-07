---
title: "Overview of Dataset Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Dataset_Management_"
---

The dataset interface includes dataset creation, dataset management, and dataset list. Among these, "dataset management" is the detail management module, supporting operations such as data preview, synchronization status monitoring, viewing model information, and setting row and column permissions. This article introduces the usage of some features in the overview section of dataset management.

<span id="_1-数据集管理概述"></span>
# Feature overview

The entire dataset interface can be divided into three modules: 1. Dataset creation, 2. Dataset management, 3. Dataset list. As shown in the figure below, the green area 2 is dataset management. In this dataset detail management area, users can perform various operations on the dataset, including data preview, synchronization status, model information, and row and column permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5548d5b3cf1f4402835d0b3770f5b533~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-数据集信息"></span>
# Dataset information

Basic dataset information: owner, dataset size, access popularity (number of visitors in the past 7 days).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3de630d30c0946cf835db1f5a14198cd~tplv-goo7wpa0wc-image.image) </span>

The following operations are available at the top:


* Permission assignment: Assign permissions to the dataset

* Edit: Edit and modify dataset configuration

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
   |Switch priority |Supports setting the synchronization priority for datasets. Tasks with higher priority will be synchronized first during system peak periods. For details, see [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Settings__).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/240335c82ec14e909e5557556b02a0d3~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only data with a extract connection supports switching priority.</div><br> |
   

* Move, copy, and delete datasets.


<span id="_2-2-数据预览"></span>
# Data preview

<span id="399229c1"></span>
## View data


* Supports two preview structures: detailed data and table structure.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">No data preview is available when synchronization fails.   </div>
   

   * Detailed data


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60a9394e69ab4dc2a588f44d3b52e9d1~tplv-goo7wpa0wc-image.image) </span>


* Table structure


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fac61f150624a5d9954f1b24c0efce7~tplv-goo7wpa0wc-image.image) </span>


* Supports entering keywords to search for field names


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7687859ce1374590a72a9760e56e37f0~tplv-goo7wpa0wc-image.image) </span>


* Supports specifying filter conditions to preview target data

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dafd619cfc349259269d459decc681d~tplv-goo7wpa0wc-image.image) </span>


<span id="bc883af7"></span>
## Edit data


* Supports editing field information. Click "Modify field" to enter the field information editing mode. For more operation guidelines, see [Field Configuration](https://docs.byteplus.com/docs/dataagent/Field_Configuration_).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc6ddc162c02447c804e7d2f7b97de78~tplv-goo7wpa0wc-image.image) </span>


* Supports batch editing fields in Excel.

   1. Click the "More" button next to "Edit field", then click "Excel batch modify".

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73a80bc080a84e60b9342b80ca68eb10~tplv-goo7wpa0wc-image.image) </span>

   2. Support downloading the latest field list as an Excel file. Users can modify field names, dimensions/metrics, field expressions, descriptions, remarks, and other content in Excel. After making changes, upload the modified Excel file. Once confirmed, the changes will be applied.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7164202ff8648d9a574080861a78582~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Do not fill in the ID for new fields. If modifying existing fields, ensure the ID matches the downloaded file.      </div>
      

<span id="_2-3-同步状态"></span>
# Synchronization status

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only "extracted" data allows viewing its synchronization status. For an introduction to direct connection and extraction, refer to <a href="https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview#a7cf7826">Supported connection methods</a>.</div>



* Support viewing the execution view and logs of historical synchronization tasks to monitor progress in real time.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb240a075cdd4b2f8040855a5595bb26~tplv-goo7wpa0wc-image.image) </span>

Support filtering tasks by specific business date, synchronization status, and data result equal to 0. The filtering criteria are explained as follows:


|Filtering criteria |Note |
|---|---|
|Business date |You can specify a particular date range for filtering. By default, synchronization tasks from the past six months are displayed. |
|Synchronization status |Includes statuses such as not ready, pending execution, in progress, successful, failed, terminated, and system canceled. All statuses are displayed by default. |
|The number of result rows is 0. |Filter tasks with a data synchronization result of 0 separately to facilitate troubleshooting data anomalies or null value issues. |



* Support single instance resynchronization and batch data synchronization.

   * Single instance resynchronization

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4770d90170334680af47c68186330f4b~tplv-goo7wpa0wc-image.image) </span>

   * Batch data synchronization

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9405381521954f688dd27d689c342586~tplv-goo7wpa0wc-image.image) </span>

      The parameter configuration instructions are as follows:

      
      |Parameters |Description |
      |---|---|
      |Selection range |* Select the start and end time for the business date to be synchronized. The data within this business date range will be synchronized in bulk immediately.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/034edac11d374569a1b4d0c8b4f7073f~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Select "After synchronization is enabled, the synchronization status list displays this time range." The execution information for this time period will be displayed in the list.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b63a59fdc994cea86ae7b85592e3a39~tplv-goo7wpa0wc-image.image) </span> |
      |Dependency check |You can choose to execute the data synchronization task based on dependencies or execute it immediately. For an introduction to dependency configuration, please refer to [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Settings__). |
      

* Click "Synchronization configuration" to view and modify detailed synchronization configuration. For more operation instructions, see [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Settings__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5d7897d294343efb9b4aef0830c32fd~tplv-goo7wpa0wc-image.image) </span>


<span id="895871eb"></span>
# Model information

View model settings: model composition, filtering criteria, and performance settings. Click the capsule icon to view detailed field information. For more operation instructions, see [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration_).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/322f05d8c8c941fba1cd61de933ab808~tplv-goo7wpa0wc-image.image) </span>

<span id="177c6d21"></span>
# Row and column permissions

Set dataset row and column permissions. For details, refer to [Data Row and Column Permissions](https://docs.byteplus.com/docs/dataagent/Data_Row_and_Column_Permissions_).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8b53332b3c44171be871aa941fc7690~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3df6cd5da1d2457196cf03b63b3c4a59~tplv-goo7wpa0wc-image.image) </span>

&nbsp;
