---
title: "URL parsing plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/URL_parsing_plugin"
---

You can use LogCollector's url_parse plugin to parse the URL string in the specified field, extract each component of the URL string (such as scheme, host, port, path, query, fragment, username, password), and add them to the logging.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.2.5 and later versions support this plugin. For instructions to check the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">2 Check software version</a>.</div>


<span id="c525f7bc"></span>
# url_parse plugin parameters description


|Name |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Name of the field containing the URL string. |
|allow_decode |Boolean |No |Whether to perform URL decoding on the `field` value before parsing. |
|parse_query |Boolean |No |Whether to parse the query parameters in the URL string as separate fields and add them to the logs. |
|keep_source |Boolean |No |Whether to keep the original `field` value. |


<span id="229f0c6a"></span>
# url_parse plugin configuration example


* Logging content:

   ```Plain
   {
       "request_url": "https%3A%2F%2Fuser%3Apass%40example.com%3A8080%2Fpath%2Fto%2Fresource%3Fparam1%3Dvalue1%26param2%3Dvalue2%23section1"
   }
   ```
   

* Configuration of LogCollector's url_parse plugin processor:

   Without keeping the original field, decode the URL string in `request_url`, parse the query parameters into separate fields, and add them to the logging.

   ```Plain
   {
       "processors": [
           {
               "url_parse": {
                   "field": "request_url",
                   "allow_decode": true,
                   "keep_source": false,
                   "parse_query": true
               }
           }
       ]
   }
   ```
   

* Processing result:

   ```Plain
   {
       "url_scheme": "https",
       "url_username": "user",
       "url_password": "pass",
       "url_host": "example.com:8080",
       "url_port": "8080",
       "url_path": "/path/to/resource",
       "url_query": "param1=value1&param2=value2",
       "url_params_param1": "value1",
       "url_params_param2": "value2",
       "url_fragment": "section1"
   }
   ```
