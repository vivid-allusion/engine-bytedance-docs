---
title: "Description of JSON Model in Dashboard"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard"
---

Each dashboard has a corresponding JSON script that allows you to quickly copy a new dashboard through JSON script. To view JSON script, you can click the **settings** icon in the dashboard and then view it in **JSON Model** tab. You can also download it to your local device as a file.

This topic describes the dashboard JSON Model format and detailed field descriptions.

<span id="94da1362"></span>
## JSON Model Format

```JSON
{
        "DashboardId": "320eb084-d7fb-4ee0-a86c-93f04bb002b2",
        "DashboardName": "test",
        "Description": "",
        "Filters": [{
                "FilterName": "alb-id",
                "FilterType": "VARIABLE",
                "FilterKey": "id",
                "FilterKeyAlias": "",
                "StaticSearch": null,
                "DynamicSearch": {
                        "TopicId": "eb234d44-caec-461a-b902-cbe003d9ef73",
                        "Query": "*|select aaaa group by 1",
                        "StartTime": "now-1d",
                        "EndTime": "now"
                },
                "TopicFilter": null
        }],
        "ChartPanels": [{
                "ChartId": "f6d139cc58fff1716447417150",
                "ChartName": "QPS",
                "ChartType": "Line",
                "Display": {
                        "version": 2,
                        "layout": {
                                "lg": {
                                        "w": 8,
                                        "h": 8,
                                        "x": 0,
                                        "y": 0
                                }
                        },
                        "setup": {
                        },
                        "fieldConfig": {
                                "items": [],
                                "version": 2
                        },
                        "actions": {
                                "items": [],
                                "version": 1
                        },
                        "hideInRow": false,
                        "transformations": {
                                "version": 1,
                                "transformations": []
                        }
                },
                "SearchInfo": {
                        "StartTime": "now-1d",
                        "EndTime": "now",
                        "SearchTopicInfos": [{
                                "TopicId": "eb234d44-caec-461a-b902-cbe003d9ef73",
                                "Query": "* | select DATE_TRUNC('second', __time__/1000), count(1) as QPS where aaaa = '${{id}}' group by 1",
                                "DataSourceName": "A"
                        }]
                },
                "Description": ""
        }, ],
        "MetaInfo": {
                "GridVersion": 2
        }
}
```


<span id="9245a8fc"></span>
## JSON Model Description


|Field name |Field type |Required |Field description |
|---|---|---|---|
|DashboardId |String |Yes |Dashboard unique identifier. It is used to identify a specific dashboard. |
|DashboardName |String |Yes |The name of dashboard. It is the dashboard title that is displayed on the interface. |
|Description |String |No |Dashboard custom description information. It is used to describe the purpose or content of the dashboard. |
|Filters |[IDaoChartFilter](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#7c836474) |Yes |An array of filter configurations. It includes filter criteria such as dashboard levels. |
|ChartPanels |[PanelJsonModel](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#paneljsonmodel) |Yes |Array of chart panels containing configuration information for all chart components in the dashboard. |
|MetaInfo |[MetaInfo](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#metainfo) |Yes |Dashboard metadata. It includes the version and layout configuration of the dashboard. |


<span id="7c836474"></span>
## IDaoChartFilter


|Field name |Field type |Required |Field description |
|---|---|---|---|
|DynamicSearch |[IDaoSearchInfo](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#idaosearchinfo) |No |Dynamic search configuration for dynamically obtaining filtering options. |
|FilterKey |String |No |The key name of the filter field. It is used to specify the log field that needs to filter. |
|FilterKeyAlias |String |No |The alias of the filter field. It is used to display the field name on the interface. |
|FilterLogic |FilterLogic |No |Filter logic.<br><br><br>* AND: AND logic<br><br>* NOT: NOT logic |
|FilterName |String |Yes |The displayed name of the filter. |
|FilterType |FilterType |Yes |Filter type.<br><br><br>* NORMAL: normal filter<br><br>* VARIABLE: variable filter<br><br>* TOPIC: topic filter |
|MultiChoice |Boolean |No |Whether to support multiple selection. |
|StaticSearch |[IDaoSelectKey](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#idaoselectkey) |No |Static search option configuration. It is the predefined selection list. |
|TopicFilter |[IDaoTopicFilter](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#idaotopicfilter) |No |Subject filter configuration. It is the parameter for the data source filter. |


<span id="e9ba1004"></span>
## IDaoSearchInfo


|**Field name** |**Field type** |**Required** |**Field description** |
|---|---|---|---|
|EndTime |String |Yes |Query end time. |
|Query |String |Yes |Query statement. |
|SearchOnTime |Boolean |No |Whether to search based on time |
|StartTime |String |Yes |Query start time. |
|TopicId |String |Yes |Subject ID. |


<span id="1712ce9a"></span>
## PanelJsonModel


|Field name |Field type |Required |Field description |
|---|---|---|---|
|ChartId |String |Yes |The unique device identifier of the chart. |
|ChartName |String |Yes |Name of the chart. |
|ChartType |String |Yes |Type of chart, such as bar chart, line chart, etc.<br><br>For value details, refer to [ChartType chart type](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#charttype-chart-type). |
|Description |String |No |Chart description information. |
|SearchInfo |[IDaoChartSearchInfo](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#idaochartsearchinfo) |No |Search configuration information for charts. |
|Display |[DisplayConfig](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#displayconfig) |Yes |Display configuration of charts. It includes version, layout, settings, and other information. |


<span id="89ea5d86"></span>
## DisplayConfig


|Field name |Field type |Required |Field description |
|---|---|---|---|
|Version |Number |Yes |Displays the configuration version number. |
|Layout |{lg: [GridPos](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#gridpos)} |Yes |Layout configuration |
|Setup |Record < string, any \> |No |Chart settings configuration. It is the specific configuration parameter for storing charts. |
|fieldConfig |Record < string, any \> |No |Field configuration. It defines the display method of chart fields. |
|Actions |Record < string, any \> |No |Operation configuration. It defines the interaction behavior of the chart. |
|hideInRow |Boolean |No |You can choose whether to hide in a row group to control the display state of the chart when the group is folded. |
|Transformations |[TransformationMangerForStorage](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#transformationmangerforstorage) |No |Data transformation configuration. It defines processing and transformation rules for the original data source. |


<span id="155a679f"></span>
## TransformationMangerForStorage


|Field name |Field type |Required |Field description |
|---|---|---|---|
|Version |Number |Yes |The version number of converted configurations. The current version is version 1. |
|Transformations |[TransformationItem](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#transformationitem) |Yes |An array of conversion rules. Conversion operations can be performed according to the sequence. |


<span id="2a5b3584"></span>
## TransformationItem


|Field name |Field type |Required |Field description |
|---|---|---|---|
|Type |String |Yes |Conversion type, such as "GroupingToMatrix", "Fallback", etc. |
|Disabled |Boolean |Yes |Whether to disable the conversion rule. |


<span id="00b89024"></span>
## GridPos


|Field name |Field type |Required |Field description |
|---|---|---|---|
|W |Number |Yes |Layout width, in grid units. |
|H |Number |Yes |Layout height, in grid units. |
|X |Number |Yes |Layout horizontal position. It is the grid units starting from the left. |
|Y |Number |Yes |Layout vertical position. It is the grid units starting from the top. |


<span id="043079b1"></span>
## MetaInfo


|Field name |Field type |Required |Field description |
|---|---|---|---|
|GridVersion |Number |Yes |Grid version number. It is used for versioning and compatibility handling of layout systems. |


<span id="7b35df1f"></span>
## IDaoChartSearchInfo


|Field name |Field type |Required |Field description |
|---|---|---|---|
|EndTime |String |Yes |Query end time. Supports quering relative time formats (such as now) and absolute time. |
|Query |String |No |Query statement, SQL or retrieval statement for searching. |
|SearchOnTime |Boolean |No |Choose whether to search based on time. It controls the search within a certain range of time. |
|SearchTopicInfos |[IDaoSearchTopicInfos](https://docs.byteplus.com/en/docs/tls/Description_of_JSON_Model_in_Dashboard#idaosearchtopicinfos) |No |Search for an array of topic information. Supports multiple data source queries. |
|StartTime |String |Yes |Query start time. Supports relative time format and absolute time. |
|TopicId |String |No |Log topic ID. |


<span id="8cb6cd9f"></span>
## IDaoSearchTopicInfos


|Field name |Field type |Required |Field description |
|---|---|---|---|
|DataSourceName |String |No |Data source name to distinguish between different data sources. |
|Query |String |Yes |Query statement, a query statement for a specific topic. |
|TopicId |String |Yes |Log topic ID. |


<span id="54b14ffa"></span>
## IDaoSelectKey


|Field name |Field type |Required |Field description |
|---|---|---|---|
|Alias |String |No |Option alias, the name used to display on the interface. |
|Name |String |Yes |Option name, the actual value. |
|Selected |Boolean |Yes |Whether it is selected. It is used to indicate whether the option is selected by default. |


<span id="5149115c"></span>
## IDaoTopicFilter


|Field name |Field type |Required |Field description |
|---|---|---|---|
|Regex |String |No |Regular matching topic pattern. It is used when TopicType is REGEX. |
|Selected |String |No |The default selected theme ID. It can be set as empty. |
|TopicType |TopicType |Yes |The log topic type. It determines how to choose a log topic.<br><br><br>* ALL: All log topics<br><br>* REGEX: Regex matching log topics.<br><br>* TOPICS: Specifies a list of log topics. |
|Topics |String |No |List of specified topic IDs. It is used when TopicType is TOPICS. |


<span id="688c1183"></span>
## ChartType chart type


|Field value |Field description |
|---|---|
|SingleValue |Single Value Chart |
|Pie |Pie chart |
|Table |Table |
|Line |Line chart |
|Histogram |Histogram |
|ChinaMap |Map of China |
|WorldMap |World map |
|Row |Row layout |
|CrossTable |Cross table |
|Statistical |Statistical chart |
|Timeline |Timeline chart |
|HistogramV2 |Histogram chart (V2 version) |
|HeatMap |Heat map |
|Progress |Progress chart |
|TreeMap |Tree map |
|Gauge |Dashboard |
|Flow |Flow chart |
|Radar |Radar map |
|Text |Text |
|Funnel |Funnel graph |
|Scatter |Scatter plot |
|Sankey |Sankey diagram |
|Topology |Topology diagram |
|Fallback |Fallback chart (for exceptions) |
|WordCloud |Highchart |
