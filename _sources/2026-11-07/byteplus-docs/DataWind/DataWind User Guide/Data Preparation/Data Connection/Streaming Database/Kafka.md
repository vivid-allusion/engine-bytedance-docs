---
title: "Kafka"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Kafka"
---

This article describes how to integrate Kafka to create datasets, in order to support real\-time data analytics scenarios for products.

<span id="ee49e9c3"></span>
# Notes

The Kafka data source is only supported in private deployment mode. To use the Kafka data source in the SaaS version, contact your company's customer success manager to submit a request.

<span id="ad3b0285"></span>
# Create from data connection


1. Log in to Byteplus, go to a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select Kafka on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18b61f160ff34a3192cc47df073a89e2~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after the connection is successful.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe536c25de184c0cb10e2eb8919f18fd~tplv-goo7wpa0wc-image.image) </span>

Kafka provides four authentication methods. The parameter configuration instructions for each authentication method are as follows. Users need to select the appropriate method based on their actual scenario:


|Authentication methods |Note |
|---|---|
|No authentication |Extremely low security, suitable for development testing or local environments.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3df4fa588d64a1aabb6df340c43151d~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Data connection name: The name of the new data connection, used to distinguish between different database connections in the system. The default is Kafka_timestamp. The name can be modified, but please enter a valid name. Only combinations of Chinese characters, English letters, digits, and underscores are allowed. Spaces are not allowed at the beginning or end.<br><br>* Version: Specify the Kafka version for the connection.<br><br>* Server: The server address and port number, in the format `ip:port`. For multiple entries, use commas to separate them. |
|SASL_PLAINTEXT |Low security (authentication only), suitable for internal trusted networks and lightweight authentication.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec13f4cf7c784680af33c0a06ad79c75~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Data connection name: The name for the new data connection, used to distinguish different database connections in the system. The default is Kafka_timestamp. The name can be modified, but please enter a valid name. Only combinations of Chinese characters, English letters, digits, and underscores are allowed. Spaces are not allowed at the beginning or end.<br><br>* Username: SASL username.<br><br>* Password: SASL password.<br><br>* Version: Specify the Kafka version for the connection.<br><br>* Server: The server address and port number, in the format `ip:port`. For multiple entries, use commas to separate them.<br><br>* Encryption method: The encryption method for the connection. Depending on the SASL user type, you can choose from three methods: PLAIN, SCRAM\-SHA\-256, or SCRAM\-SHA\-512. |
|Built\-in Kerberos for cluster |High security, suitable for enterprise production environments and multi\-tenant clusters.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/604368a2c0d74e36895ad428c44648ab~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Data connection name: The name for the new data connection, used to distinguish different database connections in the system. The default is Kafka_timestamp. The name can be modified, but please enter a valid name. Only combinations of Chinese characters, English letters, digits, and underscores are allowed. Spaces are not allowed at the beginning or end.<br><br>* Version: Specify the Kafka version for the connection.<br><br>* Server: The server address and port number, in the format `ip:port`. For multiple entries, use commas to separate them. |
|Custom Kerberos |High security (scalable), suitable for cross\-domain authentication and integration with existing Kerberos architectures.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0858ef7b832b4f52b11f3f095b9f182e~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Data connection name: The name for the new data connection, used to distinguish different database connections in the system. The default is Kafka_timestamp. The name can be modified, but please enter a valid name. Only combinations of Chinese characters, English letters, digits, and underscores are allowed. Spaces are not allowed at the beginning or end.<br><br>* Version: Specify the Kafka version for the connection.<br><br>* Server: The server address and port number, in the format `ip:port`. For multiple entries, separate them with commas.<br><br>* Krb5 file: The configuration file for Kerberos, which contains the address of the Kerberos server, the realm, and other information. The client requires this file to interact with the Kerberos server in order to obtain tickets and other authentication information.<br><br>* Keytab file: Contains the key information for the client or server, used for identity authentication during the Kerberos authentication process.<br><br>* serviceName: The name of the Kafka service in Kerberos authentication. This name must correspond to the service name configured on the Kafka server and is used to register and verify the service identity on the Kerberos server.<br><br>* Principal: Represents the identity of the client or server in the Kerberos realm, usually as a string in the format `{username}/{hostname}@{REALM}`. During authentication, the Kerberos server verifies the legitimacy of the identity based on the Principal. |


<span id="df3a0c80"></span>
# Create from dataset


1. Log in to Byteplus, click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click Create Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 in **Create from data connection**. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, where you can proceed directly to the next step of dataset creation.


<span id="9bef57ea"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the drop\-down list the previously created data connection.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afa764b835fd4715832a9a35ab24031a~tplv-goo7wpa0wc-image.image" width="687px" /></div>



3. Select the required fields and their corresponding data types.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Aggregation results cannot be written to tables, and overwriting historical data is not supported.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Kafka topic does not currently support join associations; only single\-table dataset creation is supported.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the topic data volume is too small, please manually input the JSON extraction expression.   </div>
   

   * The configuration supports nested JSON. Use jsonpath to extract fields. For details, see [Explanation of nested field extraction rules](https://docs.byteplus.com/docs/DataWind/Kafka#f4401782).

      Example: `outter.inner.cnt` indicates extracting 0 from `{"outter": {"inner": {"cnt": 0}}}`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20e3f283f18c44c2afe51f6597106e1d~tplv-goo7wpa0wc-image.image" width="610px" /></div>


```Plain Text
  :::warning
  Field names starting with an underscore are not supported, nor are field names containing the '-' character.
  :::
```



* Kafka dataset data type mapping. For the rules of Kafka partition keys, see [Explanation of partition key rules](https://docs.byteplus.com/docs/DataWind/Kafka#4735fb8f).

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35d47ded5a7d40e5b0b4848fb05a69a8~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

   Since the underlying integration of the Kafka data source depends on ClickHouse, when creating a dataset, select the corresponding ClickHouse field type according to the Kafka data type (JSON) to ensure compatibility and processing efficiency of the data format.

   The following is the mapping relationship between the two, which can guide you to correctly select the mapped field type during field configuration:

   
   |JSON type |ClickHouse alternative types |
   |---|---|
   |long |Int64 |
   |string |String, Date, Datatime |
   |float |Float64 |
   |boolean |Int64 |
   |array |Array(Int64), Array(Float64), Array(String) |
   |map |Map(Int64, Int64), Map(Int64, Float64), Map(Int64, String)<br><br>Map(String, Int64), Map(String, Float64), Map(String, String) |
   


<span id="4c66b673"></span>
# Related references

<span id="f4401782"></span>
## **Explanation of nested field extraction rules**

When there are multiple levels of nesting, you can enter a JSON path to extract fields.

Example:

```plain
{
  "body": {
    "cost": {
      "city": "Shanghai",
      "country": "China"
    }
  }
}
```


To extract the field city, set the json.path to body.cost.city.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">json.path cannot be modified, nor can a field that did not originally define json.path be changed to define json.path.</div>


   * <div data-tips="true" data-tips-type="warning">To modify such fields, first delete them and save the dataset. After the modification is complete, edit again to add the required field with the same name.</div>


   * <div data-tips="true" data-tips-type="warning">If the added field has a different name from the original field definition, you can delete the old field and add the new field in a single edit.</div>



**Example operation path I**


1. When creating a dataset, specify the field test as a non\-nested field (without json.path), with the type Nullable(Int64).

2. To change test to a nested field (with json.path), delete the test field and click Save. Then edit again, add the test field and json.path, and save.

   **Example operation path II**

3. When creating a dataset, specify the field test as a non\-nested field (without json.path), with the type Nullable(Int64).

4. To change the type of test to Nullable(String), modify it directly and save.

   **Example operation path III**

5. When creating a dataset, specify the field test as a nested field (with json.path), with the type Nullable(Int64).

6. To change test to a non\-nested field (without json.path), delete the test field, click Save, then edit again, add the test field and specify the type, and save.

    &nbsp;


<span id="explanation-of-partition-key-rules"></span>
## Explanation of partition key rules

The Kafka partition key must be convertible to date (toDate) or datetime (toDateTime) format to support subsequent time\-related operations based on the partition key, such as partitioning by day or querying by time range.

Currently, Kafka only supports the following two formats:


* int\-type timestamp (supports seconds or milliseconds). It is recommended to use int\-type timestamp.

* String\-type date, in the format '2020\-01\-01' (date) or '2020\-01\-01 00:00:00' (datetime).


If creating a table via JSON, the value of the partition key in JSON must also follow the above rules:


* int\-type timestamp: select field type `Int64` (for example, 1672531200000 represents 2023\-01\-01 00:00:00).

* string\-type date (format 'YYYY\-MM\-DD'): select field type `Date` (for example, '2020\-01\-01').

* string\-type datetime (format 'YYYY\-MM\-DD HH:MM:SS'): select field type `DateTime` (for example, '2020\-01\-01 00:00:00').
