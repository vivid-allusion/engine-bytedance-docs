---
title: "Functions list"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/overview_of_functions"
---

This topic describes a list of functions related to the data transformation feature of Torch Log Service (TLS).

<span id="全局操作函数"></span>
## Global processing functions


|Function Type |Name |Description |
|---|---|---|
|[Flow control functions](https://docs.byteplus.com/docs/tls/flow_control_functions) |c_if |If the condition is met, the function performs the corresponding operation. If the condition is not met, the function does not perform the corresponding operation. Instead, it judges whether the next condition is met. |
||c_if_else |The function performs the corresponding operation based on the results of conditional judgment. |
||c_switch |If the condition is met, the function performs the corresponding operation and returns the result. If the condition is not met, the function does not perform the corresponding operation. Instead, it judges whether the next condition is met. |
||c_compose |This function is used to combine multiple operations. Set global processing functions as the operations. |
|[Event verification functions](https://docs.byteplus.com/docs/tls/event_verification_functions) |f_match |This function judges whether a specified log field value meets a regular expression. |
||f_search |This function judges whether log content that meets a query statement exists. |
|[Event processing functions](https://docs.byteplus.com/docs/tls/event_processing_functions) |e_output |This function outputs logs to a specified topic. |
||e_auto_output |This function distributes logs dynamically to different topics. |
||e_split |This function splits a log field value into multiple logs. |
||e_drop |This function judges whether to delete logs based on conditions. |
||e_keep |This function judges whether to retain logs based on conditions. |
|[Field processing functions](https://docs.byteplus.com/docs/tls/field_processing_functions) |v |This function gets the value of a specified field in a log. When multiple field names are passed, the function returns the first field value in the log. |
||f_drop |This function deletes a specified field. |
||f_keep |This function retains a specified field and deletes the other fields. |
||f_rename |This function renames a specified field. |
||f_set |This function adds a field or modifies the value of an existing field. |
|[Field verification functions](https://docs.byteplus.com/docs/tls/field_verification_functions) |f_has |This function judges whether a specified field exists. |
||f_not_has |This function judges whether a specified field does not exist. |
|[Key-value extraction functions](https://docs.byteplus.com/docs/tls/key_value_extraction_functions) |ext_sep |This function extracts field value content based on a delimiter that has one character. |
||ext_sepstr |This function extracts field value content based on a delimiter that has multiple characters. |
||ext_json |This function expands the JSON strings of a specified field. |
||ext_json_jmes |This function uses a jmes expression to extract field values. |
||ext_kv |This function extracts field values based on two\-level delimiters. |
||ext_regex |This function extracts the value of a specified field according to a specified regular expression, then assigns it to another field. |
||ext_grok |This function extracts a specific value based on a regular expression. |
|[Mapping and enrichment functions](https://docs.byteplus.com/docs/tls/mapping_and_enrichment_functions) |f_dict_map |This function performs mapping based on a specified dictionary and maps an input field to a new field according to the mapping relationship. |
||f_table_map |The f_table_map function is used to map table data. |


<span id="表达式函数"></span>
## Expression functions


|Function Type |Name |Description |
|---|---|---|
|[Date value processing functions](https://docs.byteplus.com/docs/tls/date_value_processing_functions) |dt_str |This function converts the value of a time expression into a string. The value of a time expression can be a timestamp and a string. |
||dt_to_timestamp |This function converts a field value of the time type into a UTC timestamp based on a specified time zone. |
||dt_from_timestamp |This function converts a timestamp field of the time type into a time string that uses a specified time zone. |
||dt_now |This function gets the local time at which transformation is performed. |
|[String processing functions](https://docs.byteplus.com/docs/tls/string_processing_functions) |str_join |This function concatenates multiple strings with delimiters. |
||str_len |This function calculates the length of a string. |
||str_replace |This function replaces a string. |
||str_format |This function formats a string. |
|[Type conversion functions](https://docs.byteplus.com/docs/tls/type_conversion_functions) |ct_int |This function converts the base number of an integer value. You can specify an original base number from 2 through 36. The default original base number is 10, and the returned result is a decimal number. |
||ct_float |The function converts a value of an original data type to the floating point number data type. |
||ct_str |The function converts a value of an original data type to a string. |
||ct_bool |The function converts a value of an original data type to Boolean. |
|[Logical expression functions](https://docs.byteplus.com/docs/tls/logical_expression_functions) |op_if |If the condition is true, the value of the first expression is returned. If the condition is false, the value of the second expression is returned. |
||op_and |This function performs a logical AND operation. |
||op_or |This function performs a logical OR operation. |
||op_not |This function performs a logical NOT operation. |
||op_eq |This function performs a "logical equal to" operation. It supports strings and numeric values. |
||op_ge |This function performs a "greater than or equal to" operation. |
||op_gt |This function performs a "greater than" operation. |
||op_le |This function performs a "less than or equal to" operation. |
||op_lt |This function performs a "less than" operation. |
|[Arithmetic expression functions](https://docs.byteplus.com/docs/tls/arithmetic_expression_functions) |op_add |This function accumulates or calculates the sum of multiple values. |
||op_sub |This function performs a subtraction operation. |
||op_mul |The function performs a multiplication operation. |
||op_div |The function performs a division operation. |
||op_sum |The function performs an addition operation. |
||op_mod |This function calculates a remainder. |
||op_null |This function determines whether a value is empty. If the value is empty, it returns true. Otherwise, it returns false. |
|[Regular expression functions](https://docs.byteplus.com/docs/tls/regular_expression_functions) |regex_replace |This function matches and replaces a string based on a regular expression. |
|[Dictionary functions](https://docs.byteplus.com/docs/tls/dictionary_functions) |dict_make |This function constructs a dictionary. |
||dict_update |This function uses one dictionary to update the values of another dictionary. |
|[Encoding and decoding functions](https://docs.byteplus.com/docs/tls/encoding_and_decoding_functions) |md5_encoding |This function encodes a specified field in MD5. This means the function calculates the MD5 value of the string. |
||base64_encoding |This function encodes specified data in Base64. This means the function calculates the Base64 value of the string. |
||base64_decoding |This function decodes data in Base64. |
||str_encoding function |This function encodes a string according to a specified encoding format. |
||str_decoding function |This function decodes a string according to a specified encoding format. |
|[IP address parsing functions](https://docs.byteplus.com/docs/tls/ip_address_parsing_functions) |geo_parsee |This function parses an IP address into the corresponding geographical location and administrative division. |
|[Parsing functions](https://docs.byteplus.com/docs/tls/parsing_functions) |ua_parse_device |This function parses device information in a UA string. |
||ua_parse_os |This function parses operating system information in a UA string. |
||ua_parse_agent |This function parses browser information in a UA string. |
|[Data structuring functions](https://docs.byteplus.com/docs/tls/data_structuring_functions) |if_json function |This function determines whether a string is in standard JSON format. |
|[list functions](https://docs.byteplus.com/docs/tls/list_functions) |lst_make |This function is used to create a list. |
||lst_append |This function is used to append elements to the end of the list. |
||lst_delete_at |This function is used to delete elements at the specified position in the list. |
|[Resource functions](https://docs.byteplus.com/docs/tls/Resource-functions) |res_rds_mysql |The res_rds_mysql function is used to pull table data from BytePlus RDS for MySQL database and self\-built public MySQL database. |
