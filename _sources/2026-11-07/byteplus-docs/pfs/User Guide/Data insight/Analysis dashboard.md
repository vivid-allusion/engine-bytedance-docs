---
title: "Analysis dashboard"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Analysis_dashboard"
---

Analysis dashboard for file storage PFS lets you view various metric analysis data for file systems, including  TOP dashboard, capacity dashboard  This article explains how to use the Analytics Dashboard feature.

<span id="fcc0a6b2"></span>
## View analytics dashboard data

<span id="xIqmHSax"></span>
### Notice

Data in the Analytics Dashboard is not real\-time. For data retrieval times, refer to the refresh times shown on each chart. You can also obtain near real\-time data by running Insight tasks. For more information, see [Manage data insight tasks](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks?lang=zh).

<span id="NzEMTVGl"></span>
### Prerequisites

Analytics Dashboard has been enabled for the target file system. For specific actions, see [Enable data insight service](https://docs.byteplus.com/en/docs/pfs/Enable_Data_Insight_Service).

<span id="fcc0a6b2"></span>
### Steps


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation bar, choose **Data Insight** \> **Dashboard**.

4. On the ** Dashboard** page, view data for the **Directory Tree**, **TOP dashboard**, **Capacity dashboard** or **Hot dashboard**.

   
   <Tabs>
   <Tab zoneid="Ep0xN2q9" title="Directory tree">
   <TabTitle>Directory tree</TabTitle>
   
   By default, show capacity data for directories from the most recently created file systems in all Availability Zones with the analysis dashboard enabled over the past seven days.
   
   
   * You can filter the directory data you want to view using the following methods:
   
      * Select a specific **Availability Zone** and **File System** from the dropdown menus to view data for the specified file system.
   
      * Enter the directory within the specified file system in the **Directory** text box to view its data. The requirements for filling in are as follows:
   
         * Enter the absolute path of the directory within the file system.
   
         * Start with a forward slash (/).
   
      * Select a specified time period or customize the time range to query data.
   
   * The data available on the **Directory** **tree** tab is shown in the following table.
   
      
      |Dashboard |Note |
      |---|---|
      |Directory tree |Includes two tabs: **Full directory tree** and **Favorite directory**.<br><br><br>* **Full directory tree**: Displays all directory names and used capacity based on the specified filter criteria.<br><br>   * Click the expand icon to the left of the directory name to view subdirectories.<br><br>   * Click the copy icon to the right of the directory name to copy the directory.<br><br>   * Click the favorite icon to the right of the copy icon to add the directory to favorites. When the icon appears yellow, the directory has been added successfully and will appear under the **Favorite directory** tab.<br><br>* **Favorite directory**: Displays favorited directory names based on the specified filter criteria. Click the favorite icon next to the directory name to remove it from favorites.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each file system supports up to 1000 favorite directories.   </div><br>    |
      |Directory Capacity |After selecting the target directory on the left **Directory tree** panel, you can view the used capacity of the target directory in this area.<br><br><br>* Click or hover over the line chart to view the used capacity data for the directory at the target time.<br><br>* Click the directory name below the line chart to hide or show the used capacity line for that directory. |
      | |After selecting the target directory in the **Directory tree** panel on the left, you can view the capacity trend for the target directory in this area. This includes the **Capacity change** and **Capacity change rate**.<br><br><br>* Click or hover over the chart to view the **Capacity change** and **Capacity change rate** for the directory at the selected time.<br><br>* Click the **Capacity change** or **Capacity change rate** below the chart to show or hide the corresponding chart. |
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="CyQowg8l" title="TOP dashboard">
   <TabTitle>TOP dashboard</TabTitle>
   
   By default, the dashboard displays data from all file systems that have enabled the analysis dashboard feature in all Availability Zones. You can select a specific Availability Zone and file system in the **Availability Zone** and **File System** dropdown menus to view corresponding data. On the **TOP dashboard** tab, you can view the following data.
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="tip">You can move and resize each dashboard area in the following ways. Click <strong>Reset Dashboard Layout</strong> in the upper right corner to restore the dashboard page layout.</div>
   
   
      * <div data-tips="true" data-tips-type="tip">To change the position: Place your cursor in the blank space above each data table and drag the cursor to move the dashboard area.</div>
   
   
      * <div data-tips="true" data-tips-type="tip">To resize: Place your cursor at the lower right corner of each dashboard area and drag the cursor to adjust its size.</div>
   
   
   * <div data-tips="true" data-tips-type="tip">The time when the current data was obtained will be shown in the upper left corner of each table. When the cursor is placed within the dashboard data area, the following icons appear in the upper right corner of the table:</div>
   
   
      * <div data-tips="true" data-tips-type="tip"><strong>Full Screen</strong>: Click the fullscreen icon to display the current dashboard table in fullscreen. Press the Esc key or click the minimize icon in the upper right corner to exit fullscreen mode.</div>
   
   
      * <div data-tips="true" data-tips-type="tip"><strong>Refresh</strong>: Click the refresh icon to update the current dashboard table data.</div>
   
   
      * <div data-tips="true" data-tips-type="tip"><strong>...</strong>：</div>
   
   
         * <div data-tips="true" data-tips-type="tip">Click <strong>...</strong> \> Download <strong>csv</strong> to get the statistics in a <code>.csv</code> file. For details on the download file fields, see <a href="https://docs.byteplus.com/en/docs/pfs/Analysis_dashboard#fVvWEIdG">Description of file download fields</a>.</div>
   
   
         * <div data-tips="true" data-tips-type="tip">(If available) Click <strong>...</strong> \> Click <strong>Preview Query Statement</strong>, then click <strong>Copy</strong> in the panel on the right to copy the query statement.</div>
   
   
   * <div data-tips="true" data-tips-type="tip">Click the <strong>filesystem name/ID</strong> of each data table to go to its <strong>overview</strong> tab. (If available) Click the <strong>Fileset name/ID</strong> of each data table to go to the <strong>Fileset</strong> tab in that filesystem.</div>
   
   
   * <div data-tips="true" data-tips-type="tip">The data is displayed in descending order. Click the sort icon to switch to ascending order.</div>
   
   
   
   
   |**Kanban** |**Note** |
   |---|---|
   |Fileset Capacity |Displays Fileset capacity information for all file systems under the filter conditions, including:<br><br><br>* **File system name/ID**.<br><br>* **Fileset name/ID**.<br><br>* **Used capacity**.<br><br>* **Capacity usage**. |
   |Fileset file count |Displays the number of Fileset files for all file systems under the filter criteria, including:<br><br><br>* **File System Name/ID**.<br><br>* **Fileset Name/ID**.<br><br>* **Used File Count**.<br><br>* **File Usage Rate**. |
   |Top 1000 directories with the fastest capacity growth |Displays information for the top 1,000 directories with the fastest recent capacity growth under the selected filters (the directories are root\-level subdirectories and Fileset\-level subdirectories), including:<br><br><br>* **File system name/ID**.<br><br>* **Directory**: Name of the directory with capacity growth<br><br>* **Capacity growth (past day)** : Amount of capacity increase in the past day for this directory.<br><br>* **Growth rate (past day)** : Capacity growth rate of this directory in the past day. |
   |Top 1000 directories with the fastest capacity decrease |Displays information for the top 1000 directories with the fastest capacity decline in the past two cycles under the filter criteria, including root\-level subdirectories and fileset\-level subdirectories:<br><br><br>* **File system name/ID**.<br><br>* **Directory**: Name of the directory with reduced capacity<br><br>* **Reduced capacity (past day)** : The amount of capacity reduction in this directory over the past day.<br><br>* **Reduction rate (past day)** : The rate of capacity reduction in this directory over the past day. |
   |Top 1,000 directories not accessed for a long time |Displays information of the top 1000 directories with the longest time since last access under the filter conditions (directory dimension refers to root directory first\-level subdirectories and Fileset first\-level subdirectories), including:<br><br><br>* **File System Name/ID**.<br><br>* **Directory**.<br><br>* **Last Access Time**: The last time this directory was accessed. |
   |Top 100 file extensions by proportion |Displays information of the top 100 file extensions by proportion under the selected filter, including:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you select multiple file systems, files from each file system are shown separately and are not aggregated.</div><br><br><br><br>* **File System Name / ID**.<br><br>* **File Type**.<br><br>* **Capacity**.<br><br>* **Proportion**. |
   |Top 1000 file sizes |Displays the file information for the top 1,000 files by size under the selected filter, including:<br><br><br>* **File System Name/ID**.<br><br>* **File**: File name with path included.<br><br>* **File Size**. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="bH5ZXTcc" title="Capacity dashboard">
   <TabTitle>Capacity dashboard</TabTitle>
   
   You can view the following data on the **Capacity Dashboard** tab:
   
   
   * **Storage Capacity**: This section displays file system storage capacity data.
   
      * By default, storage capacity data for all file systems with analysis dashboard enabled in all Availability Zones is displayed. You can select a specific file system within a specified **Availability Zone** using the **File System** dropdowns to run a query.
   
      * By default, storage totals from the past hour are shown. You can choose a specific time period or set a custom time range for your query.
   
      * Click or hover your cursor over the capacity line chart to view storage capacity data for each file system at a specific time point.
   
      * Click the file system ID under the line chart to hide or display the line for that file system.
   
   * **File System Capacity Change Trends**: This area shows the **capacity change** and **capacity change rate** for a single file system.
   
      * You can select a specific file system within a specified **Availability Zone** using the **File System** dropdowns to run a query.
   
      * By default, data from the past day is displayed. You can choose a specific time period or set a custom time range for your query.
   
      * Click **Capacity Change** or **Capacity Change Rate** under the line chart to hide or display the corresponding line.
   
   * **File Count/Capacity Statistics**: You can set filter criteria in this area to view the target directory's capacity and file count statistics.
   
      * The options are explained below:
   
         
         |Parameter |**Note** |
         |---|---|
         |Availability Zone |Select the availability zone where the target file system is located. |
         |File system |Select the target file system name. |
         |Directory |Enter the directory you want to view statistics for. The following requirements apply:<br><br><br>* Enter the absolute path of the directory in the file system.<br><br>* Must start and end with a forward slash (/).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Add row</strong> below to add multiple directories. You can add up to five.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click the delete icon on the right side of the directory to remove it.</div><br> |
         |Data insight policy |Select the data insight policy you want to use to define statistical rules For more information about data insight strategies, see [Manage data insight policies](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies). |
         
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The chart will display the following data based on your parameter settings:      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The <strong>total capacity</strong> and <strong>total number of files</strong> in this directory.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The <strong>filtered file capacity</strong> and <strong>filtered file capacity</strong> that meet the Data Insight policy in this directory.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Percentage of filtered files</strong>.      </div>
         
   
      * Executable actions are explained below:
   
         
         |Operation |Note |
         |---|---|
         |Download CSV |You can download the statistical results. Follow these steps:<br><br><br>1. Click **Download CSV**.<br><br>2. Check the status of the desired download task in the **Download Records** panel. If the **Status** shows **Completed**, the download task has been successfully created.<br><br>3. Click **Download** in the **Actions** column of the selected download task to download the statistical results as a `.csv` file.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details about the fields in the downloaded file, see <a href="https://docs.byteplus.com/en/docs/pfs/Analysis_dashboard#fVvWEIdG">Description of file download fields</a>.</div><br> |
         |Refresh statistics |Click this button to refresh statistics. |
         |Reset filter |You can click this button to clear all filters and set parameters again to filter. |
         |Query |After setting the relevant parameters, click this button to perform the search. |
         
   
      * **Current statistics rule**: You can confirm the statistics rule in this section. Specifically:
   
         
         |Parameter |Note |
         |---|---|
         |Availability Zone |The Availability Zone where the target file system is located. |
         |File system |Name and ID of the target file system. |
         |Directory |Directory for reviewing statistics. |
         |Indicator Rules |Details of data insight policy rules and the relationships between them. For more information, see [Indicator description](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies#LwSpj7L6). |
         |Rule Combination Relationship ||
         
   
      * **Capacity statistics**: Capacity chart for the target directory, including statistical data such as **total capacity**, **capacity of filtered files**, and **percentage of filtered files**.
   
         * Click or hover the cursor over the chart to view specific data.
   
         * Click **total capacity**, **capacity of filtered files**, or **percentage of filtered files** below the chart to hide or show the data.
   
      * **File count statistics**: File count chart for the target directory, including statistical data such as **total file count**, **filtered file count**, and **percentage of filtered files**.
   
         * Click or hover the cursor over the chart to view specific data.
   
         * Click **total file count**, **filtered file count**, or **percentage of filtered files** below the chart to hide or show the data.
   
   
   </Tab>
   <Tab zoneid="qyzkIUXe" title="Hotspot dashboard">
   <TabTitle>Hotspot dashboard</TabTitle>
   
   By default, shows the hotspot status for all file systems with audit log enabled in all Availability Zones in the last 10 minutes. The hotspot dashboard displays the following data:
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">You can filter and query hotspot data in the following ways:</div>
   
   
      * <div data-tips="true" data-tips-type="default">Select a specific file system within a specific <strong>Availability Zone</strong> and <strong>file system</strong> from the dropdowns to query.</div>
   
   
      * <div data-tips="true" data-tips-type="default">You can select a specific time period or customize the range in the time selector for your query.</div>
   
   
   * <div data-tips="true" data-tips-type="default">You can change the position and size of each dashboard area using the following methods. Click <strong>Reset Dashboard Layout</strong> in the upper\-right corner to restore the dashboard's page layout.</div>
   
   
      * <div data-tips="true" data-tips-type="default">Change position: Place the cursor in the blank area above each data table and drag to adjust the dashboard area's position.</div>
   
   
      * <div data-tips="true" data-tips-type="default">Change size: Place the cursor at the bottom right corner of each dashboard area and drag to adjust the dashboard area's size.</div>
   
   
   * <div data-tips="true" data-tips-type="default">When the cursor is inside the dashboard data area, the following icons will appear in the top right corner of the table:</div>
   
   
      * <div data-tips="true" data-tips-type="default"><strong>Full screen</strong>: Click the full screen icon to display the current dashboard data table in full screen. Press Esc or click the minimize icon in the upper\-right corner to exit full screen mode.</div>
   
   
      * <div data-tips="true" data-tips-type="default"><strong>Refresh</strong>: Click the refresh icon to update the current dashboard table data.</div>
   
   
      * <div data-tips="true" data-tips-type="default"><strong>...</strong>：</div>
   
   
         * <div data-tips="true" data-tips-type="default">Click <strong>...</strong> \> Download <strong>csv</strong> to save the statistical data of this table as a <code>.csv</code> file. For details about the fields in the downloaded file, see <a href="https://docs.byteplus.com/en/docs/pfs/Analysis_dashboard#fVvWEIdG">Description of file download fields</a>.</div>
   
   
         * <div data-tips="true" data-tips-type="default">(If applicable) Click <strong>...</strong> \> Click <strong>Preview query statement</strong> to open the <strong>Preview query statement</strong> panel. Click <strong>Copy</strong> to copy the query statement.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Click the <strong>File system name/ID</strong> for each data table to go to the <strong>Overview</strong> tab for that file system.</div>
   
   
   * <div data-tips="true" data-tips-type="default">Data is displayed in descending order by default. Click the sort icon to switch to ascending order.</div>
   
   
   
   
   |Dashboard |**Note** |
   |---|---|
   |Top 1000 hot directories |Display directory paths with the top 1,000 access counts under the filter criteria. |
   |Top 1000 hottest files |Displays the top 1000 file names by access times under the filter criteria. |
   |Top 1000 active clients |Display the top 1,000 client IDs by visits under the selected filter criteria. |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="uh7Vlihi"></span>
## Export analytics dashboard data

The Analytics Dashboard feature lets you track download task progress and download files. Click **Analytics Dashboard** in the upper right corner and then **Download Records** to view download task logs. Specifically:


|Parameter |Note |
|---|---|
|Task name |The download task name is generated automatically by the system. |
|Modules |The name of the kanban where the download task is located, including **Capacity Kanban**, **TOP Kanban**, and **Hotspot Kanban**. |
|State |The status of download tasks includes **Completed** and **Expired**.<br><br><br>* Completed: The download task has been created successfully. You can download the `.csv` file.<br><br>* Expired: The download task has expired. You cannot download the `.csv` file. |
|Creation time |Download task creation time. |
|Completion time |Completion time for the download task. |
|Expiration time |The expiration time of the download task.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Downloaded files will be saved for 30 days and automatically deleted after expiration. Download them in time.</div><br> |
|Operation |You can click **Download** to download files from download tasks where the **Status** is **Completed**. |


<span id="fVvWEIdG"></span>
### Description of file download fields


|Field |Note |
|---|---|
|FileSystemID |File System ID |
|FilesetID |Fileset ID |
|CapacityUsed |Used capacity |
|CapacityUtil |Capacity utilization |
|FileUsed |Used Inode |
|FileUtil |Inode utilization |
|Path |File path |
|CapacityGrowth |Capacity growth value used |
|CapacityGrowthRate |Used capacity growth rate |
|CapacityShrinkage |Decrease in used capacity |
|CapacityShrinkageRate |Reduction rate of used capacity |
|AccessTime |Last file access time |
|Extension |File extension |
|Percent |Percentage |
|Size |File size |
|CapacityUsedChange |Change in used capacity |
|CapacityUsedChangeRate |Capacity used change rate |
|CapacityUsedFiltered |Filter file size |
|CapacityUsedFilteredRatio |Filter by file capacity ratio |
|FileUsedFiltered |Filter by number of Inodes |
|FileUsedFilteredRatio |Filter by Inode usage ratio |
|ClietIP |Client IP |
|AccessCount |Number of visits |
