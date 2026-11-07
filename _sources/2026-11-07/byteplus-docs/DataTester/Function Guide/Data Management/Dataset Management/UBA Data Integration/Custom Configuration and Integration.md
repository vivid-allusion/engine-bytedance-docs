---
title: "Custom Configuration and Integration"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Custom-Configuration-and-Integration"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Privatization V4.2.0 template supports UBA Data Transmission Service. Privatization V4.4.0 (inclusive) and above versions support user attribute Data Transmission Service.</div>


<span id="一、概述"></span>
# 1. Overview

When enterprises report UBA data from other factories to Volcano DataTester data service through Data Transmission Service, there may be some functional transformation requirements. Data import can be carried out through custom profiles and different conversion plug\-ins.

<span id="二、功能介绍"></span>
# 2. Function introduction

<span id="2e1fcdb8"></span>
### Custom file format

The custom configuration file uses the HOCON file format, which requires configuration including env, source, transform, and sink.

**Env:**  env is null by default, you can configure the task parallelism through executation.parallelism = 1, if you need to configure the abnormal restart strategy, you can also refer to the visual Data Transmission Service (4.4 integration task abnormal failure restart)

**Source:**  source is the data source, and only supports reading data from a single data source, generally kafka. For the specific data source configuration, see the Source plug\-in description

**Transform:**  transform is data conversion logic, multiple conversion logic can be configured, and the data is converted from top to bottom in sequence. For the specific conversion plug\-in configuration, see the Transform plug\-in description

**Sink:**  sink is a downstream data source, configured for DataTester side kafka, can be configured using Sink in the template

<span id="_2-1-配置模版"></span>
## 2.1 Configuration Template

<span id="_2-1-1uba数据demo模板"></span>
### 2.1.1 UBA Data Demo Template

```Plain
env {
  job.name = kafka_2_kafka
}

source {
    KafkaTableStream {
        # kafka address
        consumer.bootstrap.servers = "{ip1}:{port},{ip2}:{port}"
        # consumer group name
        consumer.group.id = "test"
        # topic name
        topics = kafka_source
        # temporary table name
        result_table_name = fake
        # json format
        format.type = json
        # data example
        schema = "{\"user_id\": \"ST_1\", \"event_name\": \"abtest_exposure\", \"app_name\": \"seatunel_test\", \"app_id\": 10000000, \"custom\": \"{\\\"A\\\":\\\"a\\\"}\", \"local_time_ms\": 1654831159493, \"ab_version\": 4, \"params\": \"{\\\"A\\\":\\\"a\\\"}\", \"server_time\": 1654831159, \"log_type\": \"mario_event\"}"
    }
}

transform {
    # If there is no SSID in the source data, a supplementary SSID plugin needs to be used
    SSID {
        source_id = user_id
        source_app_id = app_id
        ssid_psm = "vpc.device.idsvc"
    }

    # Use JSON formatting plugin to format data into downstream Kafka schema
    JsonTemplateFormat {
        # output field name
        json_result_name = event
        # json template        
        event = {
            "user":{
                "user_unique_id": user_id,
                "ssid": ssid
            },
            "header":{
                "app_id": app_id,
                "app_name": app_name,
                "custom": custom
                "ab_version":ab_version
            },
            "params": params,
            "event_name": event_name
            "server_time": server_time
            "log_type": log_type,
            "local_time_ms": local_time_ms
        }
    }
}

sink {
    # output data to sink Kafka
    Kafka {
        # No need to modify without special circumstances.
        row_field_name = "event"
        # Kafka cluster address of the DataTester cluster
        producer.bootstrap.servers = "{ip1}:{port},{ip2}:{port}"
        # No need to modify without special circumstances.
        topics = "behavior_event" 
    }
}
```


<span id="_2-1-2用户属性demo模板"></span>
### 2.1.2 User Properties Demo Template

```Plain
env {
  execution.parallelism = 1
}
source {
    #KafkaSource Sample
    KafkaTableStream {
        #kafka server address
        consumer.bootstrap.servers = "192.168.0.197:9192"
        #consumer group id
        consumer.group.id = "ab"
        A topic that requires consumption
        topics = sunday
        #After consuming the data, the generated flink table name can be filled in fake by default
        result_table_name = fake
        #Scheam of data in topic, supports json, csv
        You need to list all possible data
        format.type = json
        schema = "{\"user\":\"test_123\",\"ssid\":\"b0354d33-413a-4a98-9e27-c8676f0579ae\",\"params\":{\"ab_profile_20_custom\":20,\"ab_profile_21_custom\":21,\"ab_profile_22_custom\":\"22\"},\"app_id\":10000000,\"time_ms\":1676258783123}"
        format.field-delimiter = ","
        format.allow-comments = "true"
    }
}
transform {
    #Supplement ssid plugin, if only user_unique_id, you must use this plugin
    #Do not use this plugin if you already maintain user_unique_id and ssid
    SSID {
        source_id = user
        source_app_id = app_id
        #Privatized id service psm, no need to modify it without special circumstances
        ssid_psm = "vpc.device.idsvc"
    }
    #JSON formatting plugin, in this example, the JSON format does not need to be modified without special circumstances
    JsonTemplateFormat {
      #output field name
        json_result_name = event
        event = {
            #__profile_set, set user properties
            #__profile_set_once, set the user property if the property does not exist
            #__profile_unset, remove user attributes
            #__profile_append, add a property to an array (only array types are supported)
            #__profile_remove, remove a property from an array (only array types are supported)
            #__profile_increment, accumulating attributes (only numeric types supported)
            #There is no need to write dead here. You can configure it in source kafka to do different operations. The supported operations are listed above
            "event_name": "__profile_set", 
            "user": {
                #user id
                "user_unique_id": user,
                #user ssid
                "ssid": ssid
            },
            "header": {
                #application id
                "app_id": app_id,
                #No need to modify without special circumstances
                "custom": "{}",
            },
            #The specific content of the user properties that need to be set
            #Key should be a user attribute that has been registered in the tester, such as age
            #value should be the json path of the key that needs to be taken from the input
            "params": {
                #Explanation: Take the value ab_profile_20_custom this key from the input side of kafka and assign it to the user property age in the tester
                "age": "params.ab_profile_20_custom"
            },
            #No need to modify without special circumstances
            "extras": "{}",
            #Set timestamp, in milliseconds, the data stream will discard the timestamp 7 days ago, it is recommended to set it to the current time
            "local_time_ms": time_ms,
        }
    }
}
sink {
    Kafka {
        If there are no special requirements, no modification is required
        row_field_name = "event"
        If there are no special requirements, no modification is required
        topics = "user_profile"
        #Kafka cluster address of DataTester cluster
        producer.bootstrap.servers = "192.168.0.197:9192"
    }
}
```


<span id="11fcf86d"></span>
### 2.1.3 New template for UBA data

> The new template is only supported in versions greater than or equal to 4.10.0 that are sent downstream to sdk_origin_event without the need for a Data Transmission Service task to supplement the SSID


```Shell
env {
  job.name = kafka_2_kafka
  execution.restart.attempts = "10"
  execution.restart.delayBetweenAttempts = "300000"
  execution.restart.strategy = "fixed-delay"
}

source {
    KafkaTableStream {
        # kafka address
        consumer.bootstrap.servers = "{ip1}:{port},{ip2}:{port}"
        # consumer group name
        consumer.group.id = "test"
        # topic name
        topics = "datatester_seatunnel_source"
        # temporary table name. No need to modify
        result_table_name = fake
        # json format. No need to modify
        format.type = json
        format.allow-comments = "true"
        format.ignore-parse-errors = "true"
        format.field-delimiter = ","
        # data example
        schema = ""{\"user_id\":\"test\",\"event_name\":\"purchase\",\"time\":1729910736000,\"app_id\":10000000}""
    }
}

transform {
    # Use JSON formatting plugin to format data into downstream Kafka schema
    JsonTemplateFormat {
        # output field name No need to modify
        json_result_name = event
        # json template        
        event = {
            // Mandatory. No need to modify with default as server.
            "applog_type": "server",
            // Mandatory. No need to modify with default as app.
            "app_type": "app",
            "event_v3":
            [
                {        
                    // Mandatory. event name
                    "event": "event_name",
                    // Mandatory. 13 millisecond timestamp, event happen time
                    "local_time_ms": time,
                    //Not mandatory. If you need to map event properties, you can add the corresponding mapping relationship below
                    "params":
                     {
                         "amout":"amout"
                     }
                }
            ],
            "header":
            {
                // Mandatory. app id
                "app_id": app_id,
                // Not mandatory, event common properties. If you need to map event common properties, you can add the corresponding mapping relationship below
                "custom":
                {
                 },
                // Mandatory. 用户id
                "user_unique_id": "user_id",
                // Non mandatory, user ID type in multi criteria scenarios. If an ID type needs to be specified, fill in the corresponding ID type, such as iphone_id
                "user_unique_id_type":"iphone_id"
            }
        }
    }
}

sink {
    # output data to sink Kafka
    Kafka {
        # No need to modify, corresponding to the event value of json_result_ name in the JsonTemplateFormat plugin
        row_field_name = "event"
        # Kafka cluster address of the DataTester cluster
        producer.bootstrap.servers = "{ip1}:{port},{ip2}:{port}"
        # No need to modify, default is sdk_origin_event
        topics = "sdk_origin_event" 
    }
}
```


<span id="63ed52f6"></span>
## 2.2 Source plug\-in description

<span id="573b0aa5"></span>
### 2.2.1 Kafka


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|topics |string |The topic of consumption |
|result_table_name |string |Temporary table name, default fake |
|consumer.group.id |string |Consumer group id |
|consumer.bootstrap.servers |string |Kafka cluster address, by `,`delimited |
|schema |string |Data JSON format example |
|format.type |string |Data format, JSON |
|format.field\-delimiter |string |Data splitting symbol, comma |
|format.allow\-comments |string |Default "true" |
|format.ignore\-parse\-errors |string |Default "true" |


**Example**

```Plain
KafkaTableStream {
        consumer.bootstrap.servers = "{ip1}:{port},{ip2}:{port}"
        consumer.group.id = "test"
        schema = "{\"user_id\": \"ST_1\", \"event_name\": \"abtest_exposure\", \"app_name\": \"test\", \"app_id\": 10000000, \"custom\": \"{\\\"A\\\":\\\"a\\\"}\", \"local_time_ms\": 1654831159493, \"ab_version\": 4, \"params\": \"{\\\"A\\\":\\\"a\\\"}\", \"server_time\": 1654831159, \"log_type\": \"mario_event\"}"
        topics = kafka_source
        result_table_name = fake
        format.type = json
        format.allow-comments = "true"
        format.ignore-parse-errors = "true"
        format.field-delimiter = ","
}
```


<span id="c9244a11"></span>
### 2.2.2 MySQL and Hive

> Versions greater than 491 are available


MySQL and Hive are both connected through JDBC


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|driver |string |driver name<br><br>MySQL is com.mysql.cj.jdbc. Driver<br><br>Hive is org.apache.hive.jdbc. HiveDriver |
|url |string |JDBC connection address<br><br>Mysql reference "jdbc: mysql:// localhost/test "<br><br>Hive reference jdbc: hive2:// localhos/default |
|username |string |Database user name, if not available, fill in " |
|password |string |Database password, if not available, fill in " |
|query |string |Query statement, the SQL of the hive query needs to indicate all the required column names, which are provided to the downstream transform plug\-in |


**Example**

```Plain
// hive example
JdbcSource {
      driver = org.apache.hive.jdbc.HiveDriver
      url = "jdbc:hive2://192.168.0.45:9998/default"
      //Currently, there is no password set for Hive in the privatization environment
      username = "datarangers"
      password = ""
      query = "select user_id, event_name, app_id, time from abtest_event"
 }
 // mysql example
 JdbcSource {
        driver = com.mysql.cj.jdbc.Driver
        url = "jdbc:mysql://localhost/test"
        username = root
        password = xxxx
        query = "select * from abtest_test"
}
```


<span id="71328af0"></span>
### 2.2.3 HDFS

> Version greater than 4.9.2 available



|**Parameter name** |**Type** |**Description** |
|---|---|---|
|path |string |File path hdfs file path needs to start with hdfs:// |
|format.type |string |File format, HDFS files currently only support the parquet format |
|schema |string |File schema, the file schema is automatically read when "is filled in, or it can be filled in manually. Manual filling must be an Avro schema string.<br><br>For example<br><br>```Plain```<br>```{\"type\":\"record\",\"name\":\"hive_schema\",\"fields\":[{\"name\":\"id\",\"type\":[\"null\",\"long\"],\"default\":null},{\"name\":\"event_name\",\"type\":[\"null\",\"string\"],\"default\":null},{\"name\":\"time\",\"type\":[\"null\",\"long\"],\"default\":null},{\"name\":\"user_id\",\"type\":[\"null\",\"string\"],\"default\":null},{\"name\":\"amount\",\"type\":[\"null\",\"long\"],\"default\":null},{\"name\":\"city\",\"type\":[\"null\",\"string\"],\"default\":null}]}"```<br> |


**Example**

```JSON
FileSource {
    path="hdfs://192.168.0.32:5060/user/test/a"
    format.type=parquet
    schema=""
}
```


<span id="f4b2172e"></span>
## 2.3 Transform plugin description

<span id="87c71f19"></span>
### 2.3.1 JsonTemplateFormat

Use the json template to process the data, and fill in the upstream kafka schema or other field names added after creation processing

> If the field name does not exist or is not a string, it is directly filled with the value value of the template


Support getting fields in nested data through a.b.c, params and custom fields will be specially converted to json escape strings.

**This plugin needs to be the last transform plugin to execute, and the json string of the generated event is directly sent to the downstream kafka.** 


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|json_result_name |string | |
|event |json |The value of name and the value of json_result_name are equal, do not need to be modified, both are event |


**Example**

```Plain
JsonTemplateFormat {
    json_result_name = event     //output field name, specify event
    event = {
        "log_type": "mario_event",
        "user": {
            "user_unique_id": "user_id",
            "ssid": "ssid"
        }
        "header": {
            "app_id": 10000000，
            // public property
            "custom": "custom"
        },
        // event name, mandatory
        "event_name": "event_name",
        // event happen time，mandatory
        "local_time_ms": local_time_ms
        // event property, mandatory
        "params": {
            "number": "number"
        }
    }
}
```


<span id="bc5b8f41"></span>
### 2.3.2 SSID

Supplement ssid according to the specified user_unique_id field name


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|source_id |string |Field names user_unique_id data |
|source_app_id |int |appid field name in data |
|ssid_psm |string |Fill in "vpc.device.idsvc" |
|uid_type |string |If you need to report multi\-caliber, you need to fill in the multi\-caliber id type, such as "phone_id", otherwise you do not need to fill in |


**Example**

```Plain
SSID {
        source_id = user_id
        source_app_id = app_id
        ssid_psm = "vpc.device.idsvc"
    }
```


<span id="716035fa"></span>
### 2.3.3 FieldTypeTransform

Change the data type in the field, currently only between numbers and strings are supported. Support string, int, long, float, double

> If the conversion fails, the corresponding field value will be assigned the value null.



|**Parameter name** |**Type** |**Description** |
|---|---|---|
|source_field_names |string[] |Array of field names to be changed |
|result_field_types |string[] |Type array that needs to be changed |


**Example**

```Plain
FieldTypeTransform{
    source_field_names = ["A","B","C"]
    result_field_types = ["int","float", "string"]
}
```


<span id="5311efbf"></span>
### 2.3.4 FieldMap

Simple mapping of a Field of type String


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|change_field_name |string |Field name that needs to be changed |
|map |string |mapping relationship |


**Example**

```Plain
FieldMap{
    change_field_name = event
    map = "$AppStart : App_launch, $AppEnd : App_end"
}
Replace the data with $AppStart in the event field with App_launch and $AppEnd with App_end
```


<span id="3bc925ca"></span>
### 2.3.5 FieldMerge

According to the order of the specified fields, get the values of each field in order. If the value is obtained, it is assigned to the target field; if the value is not obtained or the value is null, determine the next field.


|**Name** |**Type** |**Description** |
|---|---|---|
|merge_field_names |string |The field names that need to be merged are separated by ',' and the priority is reduced in sequence |
|result_field_name |string |The field name of the merged value |
|result_field_type |string |Support int, long, float, double, string |
|defualt_value |string |If all fields have no value or are null, the default value of the last assignment; the value type needs to be the same as result_field_type |


**Example**

```Plain
FieldMerge {
    merge_field_names = "age1,age2,age3"
    result_field_name = "age"
    result_field_type = "int"
    default_value = 100
}
Attempt to obtain values from upstream data in the order of age1, age2, and age3. Once obtained, assign them to age; If none can be obtained, use the default value of 100.
age1 = 111，age2 = 222，age3 = 333
result = 111
（age1 = null，）age2 = 222，age3 = 333
result = 222
age1 = "abc"，age2 = 222，age3 = 333
result = 222, although age1 has the value abc, abc cannot be converted to an int value, so it will be discarded
```


<span id="4543dd9d"></span>
### 2.3.6 FieldValueRegex

According to the regular expression, match the field value that the specified field meets the requirements, and then modify the field in turn according to the defined processing actions


|**Name** |**Type** |**Description** |
|---|---|---|
|rules |list |Define processing rules, where the rule contains fields in the following table |
|fieldName |string |Field name, match and modify the value of the field |
|regex |string |Regular expression, need to escape, such as matching a string starting with $, after escape the expression is `"^\\ $"` |
|operation |list |* Operators that support `remove, replace, insert_head, insert_tail`<br><br>   * Remove: remove a specific character<br><br>   * Replace: replace characters separated by `,`such as `APPLaunch, app_launch`will replace `APPLaunch`with `app_launch`<br><br>   * insert_head: insert the specified string in the header<br><br>   * insert_tail: insert the specified string at the end |
|operationValue |list |The operation value corresponding to the operator |


**Example**

```Plain
FieldValueRegex{
rules=[{
       fieldName="event_name"
       regex="^\\$"
       operation=["remove", "replace"]
       operationValue=["$", "APPLaunch,app_launch"]
    },{
       fieldName="user_id"
       regex="^user"
       operation=["insert_head", "insert_tail"]
       operationValue=["integration_", "_001"]
    }]
}
```


**Description**

The original field is

```Plain
{
    "user_id": "user_510ec7",
    "event_name": "$APPLaunch",
    "app_id": 10000000
}
```


The fields processed by the rules in the above example are

```Plain
{
    "user_id": "integration_user_510ec7_001",
    "event_name": "app_launch",
    "app_id": 10000000
}
```


<span id="67457ab0"></span>
### 2.3.7 ExpressionFilter

> Only support configuration file use, **greater than 491 version**


Filter data according to filter_expression expression, filter_expression filter rule string

filter_keys is the key in the filter_expression that needs to be replaced with the actual data.

filter_keys, you need to fill in all the keys that need to be judged filter_expression, and the nested keys are connected with (.)


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|filter_expression |string |Filter expression string, supports logical expressions equal to (==), not equal to (! =), and (& &), or ( |
|filter_keys |List |In the filter expression, the list of fields to be extracted |


**Example**

```JSON
ExpressionFilter {
    filter_expression = "(event == 'exposure' && params.count == 5)||(event == 'buy' && params.amount == 'ab')"
    filter_keys = [event, params.count, params.amount]
}
Data that meets the condition of event is 'exposure' and params.comount value is 5
or, data with event is 'buy' and params.amount value is 'ab' can be filtered downstream.
Discard data that does not meet the conditions directly.
```


<span id="27d9591e"></span>
### 2.3.8 FieldFilter

Filter the data based on the value of the specified field

filter_field_name field name

filter_values is a comma\-separated string of values specified to filter downstream


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|filter_field_name |string |field name |
|filter_values |string |Specifies the number to filter downstream, multiple values comma\-separated string |


**Example**

```Plain
FieldFilter{
    filter_field_name = event
    filter_values = "purchase,buy"
}
Send data with values of purchase or buy in the event field downstream, and filter data with other values that cannot enter downstream.
```
