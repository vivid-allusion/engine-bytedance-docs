---
title: "Common errors in query and analysis"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/How_to_solve_the_problem_of_Query_results_are_inaccurate"
---

This article lists common errors and solutions encountered when querying and analyzing logs.

<span id="2bd55e24"></span>
## Sql syntax Error,details: line *:* \*\*: Cannot apply operator: bigint = varchar(10)


* Cause of error

   Use long or double data types and string types for comparison.

* Solution

   Convert a string type to a numeric type or a numeric type to a string type.


<span id="d91746d5"></span>
## Sql syntax Error,details: line *:* \*\*: Column \*\*\* cannot be resolved


* Cause of error

   No key\-value index has been created for the `batt` field, and the statistics feature has not been enabled.

* Solution

   Enable key\-value index for the target field, and enable statistics functionality. For detailed instructions, please refer to [Key-value index configuration](https://docs.byteplus.com/docs/tls/Configure-indexes-2#239ce868).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The new index only applies to new data that is collected after the modification. The index for existing data will not update.   </div>
   

<span id="37e6e763"></span>
## Sql syntax Error,details: line *:* \*\*: Function \*\*\* not registered


* Cause of error

   The objective function does not exist.

* Solution

   Check that the function name is spelled correctly. For SQL functions supported by TLS, please refer to the [function overview](https://docs.byteplus.com/docs/tls/Overview-of-functions-2).


<span id="f3329f10"></span>
## Sql syntax Error,details: line *:*  **: mismatched input '** \*'. Expecting: 'ALL', 'ANY', 'SOME',


* Cause of error

   The corresponding position is missing a keyword.

* Solution

   Check whether the grammar is correct and make corrections.


<span id="6858432e"></span>
## Sql syntax Error,details: Precheck failed: The key\-value index for field (\*\*\*) is not configured.


* Cause of error

   No key\-value index has been configured for the field.

* Solution

   Configure a key\-value index for the target field. For detailed instructions, refer to [Key-value index configuration](https://docs.byteplus.com/docs/tls/Configure-indexes-2#239ce868).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The new index only applies to new data that is collected after the modification. The index for existing data will not update.   </div>
   

<span id="11908d34"></span>
## Sql syntax Error,details: Table \*\*\* not found


* Cause of error

   The corresponding external data source or Topic does not exist.

* Solution

   1. Check whether the spelling is correct

   2. Check whether the external data source has been created successfully and the connection test has been successful.


<span id="936483fc"></span>
## Sql syntax Error,details: line *:* \*\*: Unexpected parameters (varchar(1), bigint) for function concat_ws. Expected: concat_ws(varchar, array(varchar)), concat_ws(varchar, varchar)


* Cause of error

   The type of the function parameter passed in does not match the function's expected type.

* Solution

   Modify SQL functions in query and analysis statements. To learn about the SQL functions supported by TLS, please refer to [Function overview](https://docs.byteplus.com/docs/tls/Overview-of-functions-2).
