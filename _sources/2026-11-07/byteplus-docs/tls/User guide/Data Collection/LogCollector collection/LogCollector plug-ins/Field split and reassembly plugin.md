---
title: "Field split and reassembly plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Field_split_and_reassembly_plugin"
---

You can use LogCollector’s split_select plugin to split the value of a specified field by a designated delimiter. Then select elements by their index positions to concatenate into a new field added to the log.


* Delimiter: used to split the original field and concatenate the selected fields.

* Index: used to select elements after field splitting. The index is zero\-based and inclusive.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.2.5 and later versions support this plugin. To check the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">2 Check software version</a>.</div>


<span id="fdbac4d2"></span>
# split_select plugin parameter description


|Name |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Name of the field containing the value to split. |
|new_field |String |Yes |New field name for storing concatenated values. |
|separator |String |Yes |Delimiter for splitting the `field` value. |
|index |Object |Yes |Select the index range of split elements. |
|keep_source |Boolean |No |Keep the original `field` value or not. |


Index parameter description:


|Name |Type |Required |Description |
|---|---|---|---|
|start_index |Integer |Yes |Starting position of the index. |
|end_index |Integer |Yes |End position of the index.<br><br>`-1` means selecting up to the last element. |


<span id="a8773aac"></span>
# Example of selecting intermediate elements from fields


* Log content:

   ```Plain
   {
       "path_info": "/usr/local/bin/app"
   }
   ```
   

* LogCollector's split_select plugin processor configuration:

   Keep the original field `path_info` value and split it by delimiter`/`Select elements at index positions [1,2] and save them to the `selected_path` field.

   ```Plain
   {
       "processors": [
           {
               "split_select": {
                   "field": "path_info",
                   "new_field": "selected_path",
                   "separator": "/",
                   "index": {
                       "start_index": 1,
                       "end_index": 2
                   },
                   "keep_source": true
               }
           }
       ]
   }
   ```
   

* Processing result:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Index positions start after the specified delimiter "/" .   </div>
   

   ```Plain
   {
       "path_info": "/usr/local/bin/app",
       "selected_path": "usr/local"
   }
   ```
   


<span id="6f7878a6"></span>
# Example of selecting field positions from the specified index to the end


* Key\-value pair log as follows:

   ```Plain
   {
       "tags": "apple,banana,orange,grape"
   }
   ```
   

* LogCollector's split_select plugin processor configured as follows:

   Do not keep the original field `tags` value, split by delimiter`,`Select the index positions after splitting the field starting from`2`Save the last element to the `last_two_fruits` field.

   ```Plain
   {
       "processors": [
           {
               "split_select": {
                   "field": "tags",
                   "new_field": "last_two_fruits",
                   "separator": ",",
                   "index": {
                       "start_index": 2,
                       "end_index": -1
                   },
                   "keep_source": false
               }
           }
       ]
   }
   ```
   

* Processing result:

   ```Plain
   {
       "last_two_fruits": "orange,grape"
   }
   ```
   


<span id="a8d3f048"></span>
# Example of selecting the first element of a field


* Key\-value pair log as follows:

   ```Plain
   {
       "file_name": "report.final.docx",
   }
   ```
   

* The split_select plugin processor configuration for LogCollector is as follows:

   Keep the original value of the `file_name` field and split it by the delimiter`.`Split and select the first element after splitting, then save it to the `base_name` field.

   ```Plain
   {
       "processors": [
           {
               "split_select": {
                   "field": "file_name",
                   "new_field": "base_name",
                   "separator": ".",
                   "index": {
                       "start_index": 0,
                       "end_index": 0
                   },
                   "keep_source": true
               }
           }
       ]
   }
   ```
   

* Processing result:

   ```Plain
   {
       "file_name": "report.final.docx",
       "base_name": "report"
   }
   ```
