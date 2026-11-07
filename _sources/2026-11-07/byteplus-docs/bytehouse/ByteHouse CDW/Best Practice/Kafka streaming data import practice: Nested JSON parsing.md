---
title: "Kafka streaming data import practice: Nested JSON parsing"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/kafka-streaming-data-import-nested-json-parsing"
---

When using Kafka to import data into ByteHouse, if nested JSON is encountered in the source data, virtual columns and parsing functions can be used to help parse and import the source data. This article will provide a detailed description of the import methods for such scenarios.

Kafka table includes a virtual column (Virtual Column) _content (String). The contents of _content are the JSON strings of each row. The parsing approach is to use the JSONExtract function to extract individual columns from the complete _content string using JSON path.

<span id="json-数据样例"></span>
## JSON data example

```json
{  
        "npc_info": {       
                "npc":  "bedok"
        },
        "case_info": {    
                "time_info": {  
                      "year":"2021"
                      },
                        "offence":  "stealing",  
                        "case_no":  123       
             }
}
```


<span id="导入需求说明"></span>
## Import requirements

This guide plans to import data into the target table using the following format


|Column |Target Type |Expression |Value |
|---|---|---|---|
|**npc** |String |JSONExtract(_content, '**npc_info**', '**npc**', 'String') |"bedok" |
|**year** |String |JSONExtract(_content, '**case_info**', '**time_info**', '**year**', 'String') |"2021" |
|**offence** |String |JSONExtract(_content,  **'case_info', 'offence',**  'String') |"stealing" |
|**case_no** |Int64 |JSONExtract(_content,  **'case_info', 'case_no',**  'Int64') |123 |


<span id="导入界面配置"></span>
## Configure data loading


1. Data Loading \-\> Create New Import Task \-\> Select "Kafka Data Stream".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00a87ec64b504bf4ae178f011e89630f~tplv-goo7wpa0wc-image.image) </span>

2. Select Kafka data source. You can select topic, consumption group, and offset according to your needs. Note that select "JSON_KAFKA" as the format.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c34defd1a2be4b3cb03aba8d40801581~tplv-goo7wpa0wc-image.image) </span>

3. Select the target table.

4. Define schema mapping. Click "Edit Target Table" to add a new column. Since the final column name is different from the JSON first layer format, if "analyze from datasource", some changes need to be made.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac998738bba649418d245a328bedf1e3~tplv-goo7wpa0wc-image.image) </span>

5. Create the target data table. Expression reference "Import Table" Expression content. Select "Create data table and proceed to the next step".

6. Set the data import task name. Select "Complete".

7. After creating the data import mission, click "Start".

8. Wait for the mission to run, then search the target table


Kafka data import and JSON analysis are complete.

<span id="关于-jsonextract-函数"></span>
## About the JSONExtract function

The usage of the JSONExtract function is consistent with the ClickHouse community

```undefined
JSONExtract(json[, indices_or_keys…], Return_type)
JSONExtractRaw(json[, indices_or_keys…])
```
