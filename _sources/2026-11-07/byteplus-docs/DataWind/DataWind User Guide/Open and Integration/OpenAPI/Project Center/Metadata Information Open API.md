---
title: "Metadata Information Open API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Metadata_Information_Open_API"
---

<span id="3b29ef2c"></span>
# 1. Retrieve dataset list

Caution: Before using the interfaces described in this document, please first understand the invocation method. For details, refer to [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

**Request description**


* Request URL: `POST /aeolus/api/v3/open/metadata/dataSetList`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|appId |int |Yes |Project ID |1 |
|dataSetIdList |array |No |If not provided, all datasets under the project will be returned |[1] |
|needSyncInfo |bool |No |Whether the latest synchronization time is needed. The default value is true. false can improve interface performance |true |
|needSyncInfo |bool |No |Whether data source information is needed. The default value is true. false can improve interface performance |true |


**Response example**

```JSON

{
    "data": [
        {
            "id": 1,                                数据集id
            "name": "",                             数据集name
            "url": "",                              数据集链接
            "owner": "",                            数据集所有者
            "upstreamInfo": [
                {"dbName": "a", "tableName": "b"}     上游表列表
            ],
            "type": {"code": 2, "name": "hive数据集"},  类型，code为标志码，name为可读名称
            "ctime": "2020-01-01 13:00:00",         创建时间
            "mtime": "2020-01-01 13:00:00"          更新时间
            "lastSyncTime": "2020-01-01 13:00:00"   最近同步时间
        }
    ]
}
```


<span id="_2-获取数据集所用数据源信息"></span>
# 2. Retrieve data source information used by the dataset

> Caution: This API is available starting from version V2.46.0


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68a00a53d767c5a412aff7827339abbf.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3070942bfb8c1bec79ae7891d5330aa2.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19112380b35728ebb2825b55561ab7a2.png) </span>

**Request description**


* Request URL: `GET /aeolus/api/v3/open/openDataFactory/getDataModelInfo?dataSetId=1`


Request parameters


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|dataSetId |int |Yes |Resource ID |1 |


**Request example**

?dataSetId=xxx

**Response example**

```JSON

nodeConf": [
            {
                "children": [  children代表该节点为union类型，children对应的value为参与union的所有数据源的信息
                    {  union 1
                        "advanceSettings": [],
                        "clusterName": "cn",
                        "dataSourceType": "hive",  数据源类型
                        "dbName": "dw_aeolus",  库名（部分数据源类型有实际意义，如hive ck）
                        "displayDbName": "dw_aeolus",
                        "fields": [  数据源的字段列表
                            {
                          
                                "alias": "`source_table[dw_aeolus_slowpoke_hive_test_txt]`", 
                                "dsColumnNames": ["source_table1"]，  该底表字段对应在数据集中的名称，list
                                "comment": "",
                                "isSelect": false,  👈🏻该数据源自带的字段是否被选用
                                "isSourceTableField": true,
                                "name": "source_table",  👈🏻字段名称（非维度指标；为原始字段）
                                "prepType": "string",
                                "type": "string"  👈🏻字段类型
                            },
                            ....
                        ],
                        "nodeType": "table",
                        "schemaName": "slowpoke_hive_test_txt",  表名
                        "tableAlias": "slowpoke_hive_test_txt",  表别称，当有多个相同表时，alias会加后缀进行区分
                        "tbId": "cn//dw_aeolus//slowpoke_hive_test_txt",
                        "tbName": "slowpoke_hive_test_txt"
                    },
                    {  union 2
                        "clusterName": "cn",
                        "dataSourceType": "hive",
                        "dbName": "dw_aeolus",
                        "displayDbName": "dw_aeolus",
                        "fields": [
                            {
                                "alias": "`source_table[dw_aeolus_slowpoke_hive_test_txt_1]`",
                                "comment": "",
                                "isSelect": true,
                                "isSourceTableField": true,
                                "name": "source_table",
                                "prepType": "string",
                                "type": "string"
                            },
                            .....
                        ],
                        "nodeType": "table",
                        "schemaName": "slowpoke_hive_test_txt_1",
                        "tableAlias": "slowpoke_hive_test_txt_1",
                        "tableRowFilter": {},
                        "tbId": "cn//dw_aeolus//slowpoke_hive_test_txt_1",
                        "tbName": "slowpoke_hive_test_txt"
                    }
                ],
                "fields": [  该fileds代表union 之后作为一个union table节点时，该节点所对应的字段
                    {
                        "alias": "map_store",
                        "comment": "map类型",
                        "dataSourceType": "hive",
                        "fieldMap": [
                            {
                                "fieldName": "map_store",
                                "tableId": "cn//dw_aeolus//slowpoke_hive_test_txt"
                            },
                            {
                                "fieldName": "map_store",
                                "tableId": "cn//dw_aeolus//slowpoke_hive_test_txt_1"
                            }
                        ],
                        "isPartition": false,
                        "isSourceTableField": false,
                        "name": "map_store",
                        "prepType": "string",
                        "type": "string"
                    },
                    ...
                ],
                "nodeType": "union_table"
            },
            {  没有children则代表该节点为单一节点，不存在union，下面为其全部信息，
               key对应内容含义与上面相同
                "clusterName": "cn",
                "dataSourceType": "hive",
                "dbName": "dw_aeolus",
                "displayDbName": "dw_aeolus",
                "fields": [
                    {
                        "alias": "`name[dw_aeolus_slowpoke_hive_two_partition]`",
                        "dsColumnNames": ["name_in_ds"]，  该底表字段对应的数据集字段名称，list
                        "comment": "名称",
                        "isSelect": true,
                        "isSourceTableField": false,
                        "name": "name",
                        "prepType": "string",
                        "type": "string"
                    },
                    ....
                ],
                "nodeType": "table",
                "schemaName": "slowpoke_hive_two_partition",
                "tableAlias": "slowpoke_hive_two_partition",
                "tbId": "cn//dw_aeolus//slowpoke_hive_two_partition",
                "tbName": "slowpoke_hive_two_partition"
            }
        ],
        "nodeNum": 2  该数据集画布上组成的节点总数，注意是节点数，union之后所有的内容是一个节点
    }
}
```


```plain
DataSourceType枚举值
DATA_SOURCE_TYPE_HIVE = "hive"
DATA_SOURCE_TYPE_CLICK_HOUSE = "click_house"
DATA_SOURCE_TYPE_MYSQL = "mysql"
DATA_SOURCE_TYPE_KAFKA = "kafka"
DATA_SOURCE_TYPE_DRUID = "druid"
DATA_SOURCE_TYPE_CSV = "csv"
DATA_SOURCE_TYPE_CH_CSV = "ch_csv"
DATA_SOURCE_TYPE_EXCEL = "excel"
DATA_SOURCE_TYPE_CH_EXCEL = "ch_excel"
DATA_SOURCE_TYPE_DOCS = "docs"
DATA_SOURCE_TYPE_ADB2 = "adb2"
DATA_SOURCE_TYPE_ADB3 = "adb3"
DATA_SOURCE_TYPE_FOREIGN = "foreign"
DATA_SOURCE_TYPE_MAXCOMPUTE = "maxcompute"
DATA_SOURCE_TYPE_RESTAPI = "restapi"
DATA_SOURCE_TYPE_LARK_SHEET = "lark_sheet"
DATA_SOURCE_TYPE_LARK_BITABLE = "lark_bitable"
DATA_SOURCE_TYPE_RDS = "rds"
DATA_SOURCE_TYPE_POSTGRESQL = "postgresql"
DATA_SOURCE_TYPE_IMPALA = "impala"
DATA_SOURCE_TYPE_ORACLE = "oracle"
DATA_SOURCE_TYPE_SQLSERVER = "sqlserver"
DATA_SOURCE_TYPE_PHOENIX = "phoenix"
DATA_SOURCE_TYPE_DB2 = "db2"
DATA_SOURCE_TYPE_HANA = "hana"
DATA_SOURCE_TYPE_VERTICA = "vertica"
DATA_SOURCE_TYPE_GREENPLUM = "greenplum"
DATA_SOURCE_TYPE_TERADATA = "teradata"
```


<span id="_3-获取仪表盘列表"></span>
# 3. Retrieve dashboard list

**Request description**


* Request URL: `POST /aeolus/api/v3/open/metadata/dashboardList?appId=1`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|appId |int |Yes |Project ID |1 |
|dashboardIdList |array |No |If not provided, all dashboards under the project will be returned. |[1] |
|rootId |int |No |Specify whether to return public or personal dashboards. If not provided, all dashboards will be returned. 0 indicates a public dashboard, 1 indicates a personal dashboard. |0 |
|parentId |int |No |This parameter was added in version 2.64. |1 |


**Response parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|id |int |Yes |Dashboard ID |1 |
|name |string |Yes |Dashboard name |123 |
|url |string |Yes |Dashboard URL |xxx |
|owner |string |Yes |Dashboard owner |coco |
|ctime | |Yes |Creation time |2020\-01\-01 13:00:00 |
|mtime | |Yes |Update time |2020\-01\-02 13:00:00 |


**Response example**

```JSON

{
    "data": [
        {
            "id": 1,                                仪表盘id
            "name": "",                             仪表盘名称
            "url": "",                              仪表盘链接
            "owner": "",                            仪表盘所有者
            "ctime": "2020-01-01 13:00:00",         创建时间
            "mtime": "2020-01-01 13:00:00"          更新时间
        }
    ]
}
```


<span id="_4-获取图表列表"></span>
# 4. Retrieve chart list

**Request description**


* Request URL: `POST /aeolus/api/v3/open/metadata/reportList?appId=1`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|appId |int |Yes |Project ID |1 |
|reportIdList |array |No |If not provided, all charts associated with the project will be returned. |[1] |


**Response parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|id |int |Yes |Chart ID |2 |
|name |string |Yes |Chart name |234 |
|url |string |Yes |Chart URL |xxx |
|owner |string |Yes |Chart owner |coco |
|ctime | |Yes |Creation time |2020\-01\-01 13:00:00 |
|mtime | |Yes |Update time |2020\-01\-02 13:00:00 |


**Response example**

```JSON
{
    "data": [
        {
            "id": 1,                                图表id
            "name": "",                             图表名称
            "url": "",                              图表链接
            "owner": "",                            图表所有者
            "ctime": "2020-01-01 13:00:00",         创建时间
            "mtime": "2020-01-01 13:00:00"          更新时间
        }
    ]
}
```


<span id="_5-获取仪表盘包含的图表"></span>
# 5. Retrieve charts contained in the dashboard

**Request description**


* Request URL: `POST /aeolus/api/v3/open/metadata/dashboardReport`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|appId |int |Yes |Project ID |1 |
|dashboardIdList |array |No |If not provided, all charts contained in dashboards under the project will be returned. |[1] |


**Response parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|id |int |Yes |Chart ID |2 |
|name |string |Yes |Chart name |234 |
|url |string |Yes |Chart URL |xxx |
|owner |string |Yes |Chart owner |coco |
|ctime | |Yes |Creation time |2020\-01\-01 13:00:00 |
|mtime | |Yes |Update time |2020\-01\-02 13:00:00 |


**Response example**

```perl
{
    "data": {
        "1001": [
            {
                "id": 1,                                图表id
                "name": "",                             图表name
                "url": "",                              图表链接
                "owner": "",                            图表所有者
                "ctime": "2020-01-01 13:00:00"          创建时间
                "mtime": "2020-01-01 13:00:00"          更新时间
            }
        ],
        "1002": []
    }
}
```


<span id="_6-获取图表关联的数据集"></span>
# 6. Retrieve datasets associated with the chart

**Request description**


* Request URL: `POST /aeolus/api/v3/open/metadata/reportDataset`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|appId |int |Yes |Project ID |1 |
|reportIdList | |No |If not provided, all charts associated with the project will be returned. |[1] |
|needSyncInfo | |No |Whether to return the latest synchronization time. The default value is true. Setting this to false can improve API performance. |true |
|needUpstreamInfo | |No |Whether to return data source information. The default value is true. Setting this to false can improve API performance. |true |


**Response parameters**

**Response example**

```JSON
{
    "data": {
        "1001": [
            {
                "id": 1,                                数据集id
                "name": "",                             数据集name
                "url": "",                              数据集链接
                "owner": "",                            数据集所有者
                "ctime": "2020-01-01 13:00:00"          创建时间
                "lastSyncTime": "2020-01-01 13:00:00"   最近同步时间
            }
        ],
        "1002": []
    }
}
```


<span id="_7-获取图表所属的仪表盘"></span>
# 7. Retrieve the dashboard to which the chart belongs

**Request description**


* Request URL: `POST /aeolus/api/v3/open/metadata/reportDashboard`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|appId |int |Yes |Project ID |1 |
|reportIdList | |No |If not provided, all charts associated with the project will be returned. |[1] |


**Response parameters**

**Response example**

```JSON
{
    "data": {
        "1001": [
            {
                "id": 1,                                仪表盘id
                "name": "",                             仪表盘名称
                "url": "",                              仪表盘链接
                "owner": "",                            仪表盘所有者
                "ctime": "2020-01-01 13:00:00"          创建时间
            }
        ],
        "1002": []
    }
}
```


<span id="_8-批量鉴定目标用户是否拥有某些权限"></span>
# 8. Batch verification of whether target users have certain permissions

**Request description**


* Request URL: `POST /aeolus/api/v3/open/auth/batchCheckAuth`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|originId |int |Yes |Target username for authentication |user_1 |
|resType | |Yes |Resource type to be authenticated. Enumeration: app: project, data_set: dataset, data_set_folder: dataset folder, dashboard: dashboard, large_screen: Large Screen |data_set |
|resIdList | |Yes |List of resource IDs to be authenticated |[1, 2, 3] |
|requiredRole | |No |The required permission for the target user. The default is read_role. Enumeration: view_only_role: view only, read_role: read, write_role: write, admin: administrator |read_role |


**Response parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|permittedIdList |array |Yes |List of resource IDs for which the target user has the required role |[1, 2] |


**Response example**

```JSON
{
    "data": {
        "permittedIdList": [1, 2]  目标用户拥有requireRole的资源id列表
    }
}
```


<span id="_9-获取用户权限列表"></span>
# 9. Retrieve user permission list

Caution: The interface returns results that intersect with the identity of the caller to prevent unauthorized access to permissions. For example, if the token represents that user A has permission for dataset IDs [1, 2, 3], when retrieving datasets that other users have permission for, the returned ID set will not exceed [1, 2, 3].

It is recommended that the app administrator act as the token applicant (the app administrator has permission for all resources under the project).

**Request description**


* Request URL: `GET /aeolus/api/v3/authManagement/userPermittedRes`


**Request parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|originId |int |Yes |Target username for authentication |user_1 |
|resType | |Yes |Resource types requiring authentication. Enumeration: app: project, data_set: dataset, data_set_folder: dataset folder, dashboard: dashboard, large_screen: large screen |data_set |


**Response parameters**


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|id |int |Yes | |1 |
|actions |number |Yes |User permissions. Enumeration: view_only_role: view only (no download permission), read_role: view, write_role: edit, admin: manage |read_role |
|appid |int |Yes |int |Project ID |


**Response example**

```JSON
{
  "res_list": [
    {
      "id": 1,
       view_only_role：仅阅览（无下载权限），read_role：查看，write_role：编辑，admin：管理
      "actions": ["view_only_role", "read_role", "write_role", "admin"],
      "app_id": 123
    }
  ]
}
```
