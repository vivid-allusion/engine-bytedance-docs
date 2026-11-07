---
title: "Set plug-in execution conditions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Set_plug-in_execution_conditions"
---

The LogCollector plug\-in feature allows you to set execution conditions. Torch Log Service (TLS) executes a plug\-in if the log content meets the set execution conditions. This topic offers a list of plug\-in execution conditions and describes how to set them.

<span id="功能概述"></span>
## Feature overview

By default, TLS processes specified log fields using the corresponding method in the order of plug\-ins. To judge whether to execute a specific plug\-in based on the log content, add a plug\-in condition to your plug\-in configuration. Before executing a plug\-in, TLS judges fields based on the plug\-in conditions. For example, the equals condition is used to judge whether the value of a specified field is equal to a given value. If the field value meets the plug\-in condition, this condition is considered true, and TLS executes the corresponding plug\-in. Otherwise, TLS skips the plug\-in.

You can configure basic execution conditions for each LogCollector plug\-in, and TLS allows you to add combined conditions to plug\-ins. Combined conditions are set based on the syntax for basic conditions. If you add combined conditions, TLS judges whether to execute a plug\-in according to the judgment results of the specified basic conditions. Assume that you add the and condition. In this case, if all specified conditions are true, TLS executes the plug\-in.

TLS offers various plug\-in execution conditions. For example, these conditions can check whether a field value is equal to a given value or contains a specified string.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V1.0.38 and later support plug\-in execution conditions. We recommend that you confirm the version of your LogCollector in advance.</div>


<span id="设置插件执行条件"></span>
## Set plug\-in execution conditions

You can add the execution condition field `when` to the plug\-in configuration. The `when` field is optional and used to specify judgment conditions. Configure this field when you add execution conditions. For more information on how to use a plug\-in, refer to [Procedure](https://docs.byteplus.com/docs/tls/Use_LogCollector_plug-ins_to_process_logs#%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4).

For example, the following example adds an execution condition to the add_kvs plug\-in. If the `data` field value is `Click Here` and the `size` field value is `36`, insert the constant fields `name` and `cluster_id` into the log content.

```json
{
  "processors": [
    {
      "add_kvs": {
        "when": {
          "equals": {
            "data": "Click Here",
            "size": "36"
          }
        },
        "fields": {
          "name": "Jack",
          "cluster_id": "C02G64T1MD6R"
        }
      }
    }
  ]
}
```


<span id="执行条件列表"></span>
## List of execution conditions


|Condition Type |Condition Name |Description |
|---|---|---|
|Basic condition |[equals condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#equals-%E6%9D%A1%E4%BB%B6) |judges whether the value of a specified field is equal to a given value. |
||[contains condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#contains-%E6%9D%A1%E4%BB%B6) |judges whether a specified field contains a given string. |
||[regexp condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#regexp-%E6%9D%A1%E4%BB%B6) |judges whether a specified field matches a given regular expression. |
||[range condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#range-%E6%9D%A1%E4%BB%B6) |judges whether a specified field falls within a given numeric range. |
||[has_fields condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#has-fields-%E6%9D%A1%E4%BB%B6) |judges whether a log contains a given field. |
||[length condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#length-%E6%9D%A1%E4%BB%B6) |judges whether the length of a specified field is within a given numerical range. |
|Combined condition |[and condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#and-%E6%9D%A1%E4%BB%B6) |judges whether all specified basic conditions are true. |
||[or condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#or-%E6%9D%A1%E4%BB%B6) |judges whether at least one of the specified basic conditions is true. |
||[not condition](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#not-%E6%9D%A1%E4%BB%B6) |judges whether all specified basic conditions are false. |


<span id="基本条件"></span>
## Basic condition

<span id="equals-条件"></span>
### equals condition

The equals condition is used to judge whether the content of a specified field is equal to a given value. If the content of a specified field in a log is equal to a given value, the equals condition is true. Otherwise, it is false. When you configure multiple fields in the equals condition, the relationship between the judgment results of these fields is logical AND.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The precision of floating point numbers is affected by the used binary storage method. If you use the equals condition to compare two floating point numbers and the difference between the two numbers is less than 0.000001, TLS considers these two floating point numbers equal.</div>


**Parameter description**


|Parameter |Type |Required |Description |
|---|---|---|---|
|equals |Map<String, ?\><br><br>Supported value types:<br><br><br>* Integer.<br><br>* Float.<br><br>* String.<br><br>* Boolean. |Yes |Key is the name of a log field and Value is a field value.<br><br>Make sure Key is unique. In addition, do not leave it empty or specify a period ( . ) for it. |


**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "equals": {
               "data": "Click Here",
               "size": "36"
             }
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="contains-条件"></span>
### contains condition

The contains condition is used to judge whether a specified field contains a given string. If the specified field in the current log contains the given string, the contains condition is true. Otherwise, it is false. When you configure multiple fields for the contains condition, the relationship between the judgment results of these fields is logical AND.

**Parameter description**


|Parameter |Type |Required |Description |
|---|---|---|---|
|contains |Map<String, String\> |Yes |Key is the name of a log field and Value is a field value.<br><br>Make sure Key is unique. In addition, do not leave it empty or specify a period ( . ) for it. |


**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "contains": {
               "data": "Click",
               "onMouseUp": "sun1"
             }
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="regexp-条件"></span>
### regexp condition

The regexp condition is used to judge whether a specified field matches a given regular expression. If the specified field in the current log matches the given regular expression, the regexp condition is true. Otherwise, it is false. When you configure multiple fields for the regexp condition, the relationship between the judgment results of these fields is logical AND.

**Parameter description**


|Parameter |Type |Required |Description |
|---|---|---|---|
|regexp |Map<String, String\> |Yes |Key is the name of a log field and Value is a field value.<br><br>Make sure Key is unique. In addition, do not leave it empty or specify a period ( . ) for it. |


**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "regexp": {
               "data": "^Click.*",
               "onMouseUp": "^sun1.*"
             }
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="range-条件"></span>
### range condition

The range condition is used to judge whether a specified field falls within a given numeric range. If the specified field in the current log falls within the given numeric range, the range condition is true. Otherwise, it is false. When you configure multiple fields for the range condition, the relationship between the judgment results of these fields is logical AND.

**Parameter description**


|Parameter |Type |Required |Description |
|---|---|---|---|
|range |Map<String, Map<String, Number\>\> |Yes |Key is the field name and Values is a numeric range composed of operators and numeric values.<br><br>Make sure Key is unique. In addition, do not leave it empty or specify a period ( . ) for it.<br><br>Supported operators:<br><br><br>* lt: less than.<br><br>* lte: less than or equal to.<br><br>* gt: greater than.<br><br>* gte: greater than or equal to. |


**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "range": {
               "hOffset": {
                 "gte": 100,
                 "lte": 1000
               },
               "vOffset": {
                 "gte": 50,
                 "lte": 200
               }
             }
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="has-fields-条件"></span>
### has_fields condition

The has_fields condition is used to judge whether specified fields are included. If the current log contains all the specified fields, the has_fields condition is true. Otherwise, it is false. When you configure multiple fields for the has_fields condition, the relationship between the judgement results of these fields is logical AND.

**Parameter description**


|Parameter |Type |Required |Description |
|---|---|---|---|
|has_fields |List |Yes |List of fields.<br><br>Make sure Key is unique. In addition, do not leave it empty or specify a period ( . ) for it. |


**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "has_fields": [
               "alignment",
               "onMouseUp"
             ]
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="length-条件"></span>
### length condition

The length condition is used to judge whether the length of a specified field is within a given numeric range. If the length of the specified field in the current log is within the given numeric range, the length condition is true. Otherwise, it is false. When you configure multiple fields for the length condition, the relationship between the judgment results of these fields is logical AND.

**Parameter description**


|Parameter |Type |Required |Description |
|---|---|---|---|
|length |Map<String, Map<String, Number\>\> |Yes |Key is the field name and Values is a numeric range composed of operators and numeric values.<br><br>Do not specify periods ( . ), empty values, or duplicate values for this parameter.<br><br>Supported operators:<br><br><br>* lt: less than.<br><br>* lte: less than or equal to.<br><br>* gt: greater than.<br><br>* gte: greater than or equal to.<br><br>* eq: equal to. |


**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "length": {
               "hOffset": {
                 "eq": 3
               },
               "time": {
                 "gte": 10,
                 "lte": 50
               }
             }
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="组合条件"></span>
## Combined condition

<span id="and-条件"></span>
### and condition

The AND condition allows you to configure one or more basic conditions. When all these basic conditions are true, the AND condition is true. Otherwise, it is false.

**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "and": [
               {
                 "equals": {
                   "size": 36
                 }
               },
               {
                 "has_fields": [
                   "alignment",
                   "onMouseUp"
                 ]
               }
             ]
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="or-条件"></span>
### or condition

The OR condition allows you to configure one or more basic conditions. When at least one of these basic conditions is true, the OR condition is true. Otherwise, it is false.

**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "or": [
               {
                 "equals": {
                   "size": 37
                 }
               },
               {
                 "has_fields": [
                   "alignment",
                   "onMouseUp"
                 ]
               }
             ]
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
   


<span id="not-条件"></span>
### not condition

The NOT condition allows you to configure one basic condition. When this basic condition is true, the NOT condition is false. Otherwise, the NOT condition is true.

**Configuration examples**


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "when": {
             "not": {
               "equals": {
                 "size": 37
               }
             }
           },
           "fields": {
             "name": "Jack",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Processing result:

   ```json
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   "name": "Jack",
   "cluster_id": "C02G64T1MD6R"
   ```
