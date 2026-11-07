---
title: "Rename plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Rename-plugin"
---

You can use the rename plugin of LogCollector to rename field names.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.0.0 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


<span id="d514c10d"></span>
## Parameter description


|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |The name of the field to be renamed. |
|new_field |String |Yes |The new name of the field.<br><br>The new field name cannot be the same as an existing field name, cannot be empty, and does not support the English period (.). |
|ignore_missing |Boolean |No |Whether to ignore non\-existent fields.<br><br><br>* True (default): When the field does not exist, it is directly ignored.<br><br>* False: When the field does not exist, an error is reported directly. |


<span id="03ec00f6"></span>
## Configuration example


* Key\-value pair logs processed through a collection mode or other processor plug\-ins:

   ```JSON
   "data": "Click Here"
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "alignment": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
   

* Configuration for the LogCollector plug\-in processor:

   ```JSON
   {
       "processors":[
           {
               "rename":[
                   {
                       "field":"alignment",
                       "new_field":"address"
                   },
                   {
                       "field":"data",
                       "new_field":"message"
                   }
               ]
           }
       ]
   }
   ```
   

* Result

   ```Plain
   "message": "Click Here"
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "address": "center"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
