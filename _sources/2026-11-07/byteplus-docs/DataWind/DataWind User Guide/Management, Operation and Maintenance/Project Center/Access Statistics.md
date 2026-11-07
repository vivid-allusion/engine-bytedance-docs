---
title: "Access Statistics"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Access_Statistics"
---

The access status of resources within a project is a concern for every data producer. In this module, users can monitor the usage of existing datasets, dashboards, and charts, and also evaluate the utilization rate of current resources to provide data support for resource reclamation.

<span id="bbab675a"></span>
# Feature entry points

Users can view the access status of each dataset, dashboard, and chart through the following feature entry points, including PV, UV, and 30\-day access volume. For information about viewing permissions and statistical criteria, see [Related references](https://docs.byteplus.com/docs/DataWind/Access_Statistics#0847f888).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">PV: Page View (page views), refers to the number of times users access a webpage during the statistical period. Each time a page is opened or refreshed, it is counted as 1.</div>


* <div data-tips="true" data-tips-type="tip">UV: Unique Visitor (number of unique visitors), refers to the number of unique visitors based on unique identifiers during the statistical period. Multiple visits by the same user within the period are counted as 1.</div>


* <div data-tips="true" data-tips-type="tip">30\-day access volume: refers to the total number of user accesses in the past 30 days, including repeated refreshes or visits by the same user.</div>




|Navigation path |Feature overview |
|---|---|
|"Project Center" \- "Access Statistics" |On the access statistics overview page, you can choose to view the access statistics (PV, UV) for dashboards, charts, datasets, and screens.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd4108e450624e9c9800a5aeec7adaaa~tplv-goo7wpa0wc-image.image) </span> |
|"Dashboard" \- "Dashboard List" \- "More" \- "Access Statistics" |You can view the access statistics (PV, UV) for dashboards.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77be9f863b9043a6beef8129a4e070ed~tplv-goo7wpa0wc-image.image) </span> |
|"Project Center" \- "Chart Management" \- "30\-day Access Volume" |You can view the 30\-day access volume for charts.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28f4dde03ede4c5399fcff182be7a89d~tplv-goo7wpa0wc-image.image) </span> |
|"Data Preparation" \- "Dataset" \- "30\-day Access Volume" |You can view the 30\-day access volume for datasets.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/847642d1a55a471897ef53bffee1853b~tplv-goo7wpa0wc-image.image) </span> |


<span id="ee5ef02f"></span>
# Access statistics

Users can set filter criteria to view the access trends, access times, usage summaries, access details, and perform operations such as downloading data for specific resources within a specified period.

<span id="0678b3dd"></span>
## Filter criteria

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fef34a7f00504f068295dad2e077a5cc~tplv-goo7wpa0wc-image.image) </span>


|Filter criteria |Description |
|---|---|
|Access date |Set the start and end time for the access date to view resource access statistics for a specific period. The default is "Past 30 days".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47154a30df1c457991bfcf5d0622cc7b~tplv-goo7wpa0wc-image.image) </span> |
|Resource type |Dashboards, charts, datasets, and screens are available options.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fdb1f9a39aa4c6daf8decfc21ef5a4f~tplv-goo7wpa0wc-image.image) </span> |
|Resource name |Supports searching by the name of dashboards, charts, datasets, and screens. |
|Resource ID |Each resource has a unique resource ID. For details, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625e4). |
|Owner |Search by username to view the access statistics of resources created by the owner. |
|Display range |You can select "Management Permission" or "Edit Permission and above" to display resource access statistics based on the user's permissions for the resource.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only users with resource edit permissions or higher can view detailed access records for dashboards and datasets.</div><br> |
|Exclude from PV/UV calculation |Search by username, name, or email to exclude certain special users from affecting the UV/PV calculation. |
|Folder location |Enter keywords to search for the folder where the resource is located. |


<span id="b77bf70d"></span>
## Access trends

Displays the trends of PV and UV over a specific period in the form of a line chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad837ff202cd4af2855b62721dd266d9~tplv-goo7wpa0wc-image.image) </span>

<span id="70890520"></span>
## Access times

Displays the values of PV and UV at specific times in a table format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae26f0f8448a4da2b7279ae0a2089a3b~tplv-goo7wpa0wc-image.image) </span>

<span id="47dcdc49"></span>
## Usage summary

Includes information such as all filtered resource IDs, resource names, folders, resource owner names, PV counts and PV trend charts, UV counts and UV trend charts, and the most recent access time. Users can view access details for individual resources, move or delete access information for individual resources, and download access data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f716d5cc13e14413a295843de924d0da~tplv-goo7wpa0wc-image.image) </span>

<span id="f4666c56"></span>
### View access details

Click "Access Details" to view the usernames and names of all users who accessed the resource, as well as the specific access times within a specified period.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In privatized environments version V2.87.0 and above, access details include "Department" information.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93b18ca6a53d49b5937274eeadb66dee~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3e909c8f0524a7aa431f0d03bacc8f6~tplv-goo7wpa0wc-image.image) </span>

<span id="bdc1bc4b"></span>
### Download access data

Click "Download Data" to download the usage summary data in XLSX, GBK\-encoded CSV, or UTF_8\-encoded CSV format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90d71ac91d374567902e91547b0d7d61~tplv-goo7wpa0wc-image.image) </span>

<span id="05ff9f4d"></span>
### Navigate to resource page

Click the resource name of an individual resource to navigate to its page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6c2c3e95ea94ad1a1714227db1f9d5e~tplv-goo7wpa0wc-image.image) </span>

<span id="0847f888"></span>
# Related references

<span id="4cb1b600"></span>
## Permission management

The table below describes the permission requirements for viewing the access status of each resource.


|Entry point |Permission requirements |
|---|---|
|Access statistics |* Project administrators: can view access statistics for all resources.<br><br>* Regular users: Can only view, and by default are shown, access statistics for dashboards and datasets for which they have edit permissions, and for charts for which they have manage permissions. |
|Dashboard |* Users with edit permissions for this dashboard can see this entry. |
|Chart management |* All users can view the 30\-day access volume for all charts. |
|Dataset |* All users can view the 30\-day access volume for all datasets. |


<span id="57f03fa6"></span>
## Statistical criteria

The table below describes under what circumstances each resource is counted as one access.


|Resource |Statistical criteria |
|---|---|
|Dashboard |* Each time the dashboard page is opened, it is counted as one access.<br><br>* Editing the dashboard is not counted, and only accesses when the dashboard is opened by authorized users are counted. |
|Chart |* If a chart with a chart ID is accessed through the visual query page or its associated dashboard is accessed, the chart is counted as one access.<br><br>* Only accesses by authorized users are counted for charts. |
|Dataset |* If an associated chart is accessed, it is counted as one access; if this dataset is accessed from the visual query page, it is also counted as one access.<br><br>* Attempts to access dashboards by users without permissions are not included. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If statistics are selected by day, only data from yesterday can be viewed.</div>


* <div data-tips="true" data-tips-type="warning">Data collection started on June 9, 2020, and full data is available starting from June 10.</div>
