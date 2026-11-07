---
title: "Reserved fields plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Reserved_fields_plugin"
---

You can use LogCollector's keep_fields plugin to retain specified fields and discard all other fields.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.2.5 and later versions support this plugin. To check the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">2 Check software version</a>.</div>


<span id="549a60ad"></span>
## keep_fields plugin parameter description


|name |type |required |Description |
|---|---|---|---|
|fields |Array |yes |List of field names to retain. |


<span id="cbcb2eea"></span>
## keep_fields plugin configuration example


* Logging content:

   ```JSON
   {
       "data": "Click Here",
       "size": "36",
       "style": "bold",
       "name": "text1",
       "hOffset": "250",
       "vOffset": "100",
       "alignment": "center",
       "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;",
       "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   }
   ```
   

* LogCollector's keep_fields plugin processor configuration:

   Retain only the `size`, `name`, and `time` fields in the log.

   ```JSON
   {
       "processors": [
           {
               "keep_fields": {
                   "fields": [
                       "size",
                       "name",
                       "time"
                   ]
               }
           }
       ]
   }
   ```
   

* Processing result:

   ```JSON
   {
       "size": "36",
       "name": "text1",
       "time": "Today is 2023-06-08. Tomorrow is 2023-06-09."
   }
   ```
