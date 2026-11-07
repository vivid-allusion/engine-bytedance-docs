---
title: "Filter log plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Filter-log-plugin"
---

The drop_log plugin of LogCollector supports matching log field names with regular expressions to filter out logs that do not meet the criteria.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.0.0 and later support this plug\-in. For more information on how to view the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC">View software version</a>.</div>


<span id="984ca837"></span>
## Parameter description

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The value of the <code>drop_log</code> field is of array type, and it supports the addition of multiple array objects. In the same array object, <code>keep_regex</code> and <code>drop_regex</code> cannot be configured simultaneously, but at least one of them should be configured.</div>



|Parameter |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |The field name. |
|keep_regex |String |No |The regular expression used to retain logs.<br><br>If the field name does not match any of the regular expressions for retaining logs, then discard the log. |
|drop_regex |String |No |The regular expression used to discard logs.<br><br>If there is a field name that exactly matches the regular expression for discarding logs, then discard the log. |


<span id="8026863a"></span>
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
               "drop_log":[
                   {
                       "field":"alignment",
                       "keep_regex":"center"
                   },
                   {
                       "size":"data",
                       "drop_regex":"\d+"
                   }
               ]
           }
       ]
   }
   ```
   

* Result

   Discard this log and do not collect it.
