---
title: "Field adder"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Field_adder"
---

You can use the add_kvs plug\-in to specify that LogCollector adds specific fields to logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">LogCollector V1.0.18 and later support the add_kvs plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


   <div data-tips="true" data-tips-type="tip">The add_kvs plug\-in processor allows you to add environment variable fields of the host or container running LogCollector to a log. When you add an environment variable field, you can use a custom field name as the key and set the field value to <code>${ENV_NAME}</code>. Then, Torch Log Service (TLS) automatically reads the environment variable name and specifies it as the value. If the host or container running LogCollector does not have the environment variable ENV_NAME, the value is empty.   </div>
   


<span id="参数说明"></span>
## Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|fields |Map<String,Object\> |Yes |Specify the keys and values that you want to add.<br><br><br>* Use the key\-value pair format. You can add multiple fields.<br><br>* Make sure the keys are unique. In addition, do not leave this parameter empty or specify a period ( . ) for it. |
|when |Object |No |Specify the condition for executing the plug\-in. The plug\-in is executed only when the specified condition is true. For more information, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8). |


<span id="配置示例"></span>
## Configuration examples


* Logs

   ```Plain
   [1] [Dec 15, 2012 1:42:43 AM] com.dev.log.LoggingExample main
   ```
   

* Configuration for the LogCollector plug\-in processor

   ```json
   {
     "processors": [
       {
         "add_kvs": {
           "fields": {
             "name": "Jack",
             "path": "${PATH}",
             "cluster_id": "C02G64T1MD6R"
           }
         }
       }
     ]
   }
   ```
   

* Result

   ```Plain
   "__content__": "[1] [Dec 15, 2012 1:42:43 AM] com.dev.log.LoggingExample main"
   "name": "Jack"
   "path": "/Users/Jack/go/bin"
   "cluster_id": "C02G64T1MD6R"
   ```
