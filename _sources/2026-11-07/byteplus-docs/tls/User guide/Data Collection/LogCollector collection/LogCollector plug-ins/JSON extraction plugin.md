---
title: "JSON extraction plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/JSON_extraction_plugin"
---

You can use LogCollector's json_extract plugin to specify a JSONPath expression to extract one or more values from the specified JSON content and add them as a new JSON array to the log.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.2.5 and later versions support this plugin. To check the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">2 Check software version</a>.</div>


<span id="662d21b1"></span>
## json_extract plugin parameter description


|Name |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |The field name containing the JSON string.<br><br>If the content of the `field` does not contain a valid JSON string, parsing is considered to have failed. |
|new_field |String |Yes |The name of the new field for storing the extracted values. |
|json_path |String |Yes |JSONPath expression to extract value from `field`.<br><br>If the `json_path` expression does not match any value, it is considered a parsing failure. |
|keep_source |Boolean |No |Whether to retain the original `field` value. |


<span id="62860b43"></span>
## JSONPath expression example


* For example, JSON content:

   ```JSON
   {
     "name": {"first": "Tom", "last": "Anderson"},
     "age":37,
     "children": ["Sara","Alex","Jack"],
     "fav.movie": "Deer Hunter",
     "friends": [
       {"first": "Dale", "last": "Murphy", "age": 44, "nets": ["ig", "fb", "tw"]},
       {"first": "Roger", "last": "Craig", "age": 68, "nets": ["fb", "tw"]},
       {"first": "Jane", "last": "Murphy", "age": 47, "nets": ["ig", "tw"]}
     ]
   }
   ```
   

* JSONPath expressions and their matching values:

   
   |JSONPath expression |matching value |
   |---|---|
   |name.last |"Anderson" |
   |name.first |"Tom" |
   |age |37 |
   |children |["Sara","Alex","Jack"] |
   |children.0 |"Sara" |
   |children.1 |"Alex" |
   |friends.1 |{"first": "Roger", "last": "Craig", "age": 68, "nets": ["fb", "tw"]} |
   |friends.1.first |"Roger" |
   |friends.#.age |[44,68,47] |
   


<span id="c509471a"></span>
## json_extract plugin configuration example


* The log content is as follows, where the value of the `request_body` field is a JSON string:

   ```JSON
   {
       "timestamp": "2023-10-26T10:30:00Z",
       "level": "INFO",
       "source_ip": "192.168.1.100",
       "request_body": "{\"user\": {\"id\": \"usr_123\", \"username\": \"alice\", \"attributes\": {\"roles\": [\"administrator\", \"power_user\"], \"department\": \"engineering\"}}, \"action\": \"update_profile\"}"
   }
   ```
   

* LogCollector's json_extract plugin processor configuration:

   Extract values from the JSON content in the `request_body` field using the JSONPath expression `user.attributes.roles`, and store the values in the `user_roles` field.

   ```JSON
   {
       "processors": [
           {
               "json_extract": {
                   "field": "request_body",
                   "json_path": "user.attributes.roles",
                   "new_field": "user_roles"
               }
           }
       ]
   }
   ```
   

* Processing results:

   ```JSON
   {
       "timestamp": "2023-10-26T10:30:00Z",
       "level": "INFO",
       "source_ip": "192.168.1.100",
       "user_roles": ["administrator","power_user"]
   }
   ```
