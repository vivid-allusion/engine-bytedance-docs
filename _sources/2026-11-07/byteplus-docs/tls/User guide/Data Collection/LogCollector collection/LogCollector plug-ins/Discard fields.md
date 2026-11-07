---
title: "Discard fields"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Discard_fields"
---

You can use LogCollector's drop_fields plugin to discard unnecessary fields.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.2.0 and later versions support this plugin. To check the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">Check software version</a>.</div>


<span id="3e3a1d0a"></span>
### Parameter description


|Name |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Field name. |


<span id="8dfc8e38"></span>
### Configuration example

Delete the data and alignment fields from logs during collection.


* Key\-value pair logs after processing (such as collection mode or other processor plugins)

   ```Plain
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
   

* LogCollector plugin processor configuration

   ```JSON
   {
       "processors": [
           {
               "drop_fields": {
                   "fields": [
                       "data",
                       "alignment"
                   ]
               }
           }
       ]
   }
   ```
   

* Processing result

   ```Plain
   "size": "36"
   "style": "bold"
   "name": "text1"
   "hOffset": "250"
   "vOffset": "100"
   "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
   "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   ```
