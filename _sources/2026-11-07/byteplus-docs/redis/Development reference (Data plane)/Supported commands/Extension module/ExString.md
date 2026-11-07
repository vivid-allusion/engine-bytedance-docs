---
title: "ExString"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/exstring"
---

Cache for Redis supports the ExString extension module, a versioned string data type. This topic describes the commands supported by the ExString extension module.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance version must meet the following requirements simultaneously to use the ExString module:

   * The database version must be Redis 7.0.

   * The minor version of proxy must be greater than or equal to 1.22.0.

   * The minor version of server must be greater than or equal to 7.17.3.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the database version and minor version information of an instance on the <strong>Summary</strong> tab. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).


<span id=".5Yqf6IO954m55oCn"></span>
## Features

The ExString provided by Cache for Redis is based on the native Redis String data structure and supports the following additional features:


* Supports carrying version information, and version information allows modification.

* ExString supports boundary settings based on the Redis String addition and subtraction function, which can limit the results of INCRBY and INCRBYFLOAT to a certain range, and prompt an error if it exceeds the range.


<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax

<span id=".5ZG95Luk5YiX6KGo"></span>
### Command list

The commands supported by ExString are shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the command syntax in the following table, the definitions are as follows:</div>



* <div data-tips="true" data-tips-type="tip"><code>UPPERCASE KEYWORD</code>: Command keyword, such as <code>EXSET</code>.</div>


* <div data-tips="true" data-tips-type="tip"><code>lowercase keyword</code>: Customizable parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code>[]</code>: The content within <code>[]</code> is an optional parameter, and the content outside <code>[]</code> is a required parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code><Option 1>|<Option 2>|<Option n></code>: A set of mutually exclusive parameter options, meaning only one parameter can be selected from the options for setting.</div>




|command |Syntax |Description |
|---|---|---|
|[EXSET](https://docs.byteplus.com/en/docs/redis/exstring#exset) |`EXSET key value [EX\|PX\|EXAT\|PXAT time] [NX\|XX] [VER\|ABS\|GT version] [KEEPTTL]` |Create a new key with value, or a new value for existing key settings. |
|[EXGET](https://docs.byteplus.com/en/docs/redis/exstring#exget) |`EXGET key` |Query the value and version information of the specified key. |
|[EXSETVER](https://docs.byteplus.com/en/docs/redis/exstring#exsetver) |`EXSETVER key version` |Specify the version of the key. |
|[EXINCRBY](https://docs.byteplus.com/en/docs/redis/exstring#exincrby) |`EXINCRBY key num [MIN minval] [MAX maxval] [EX\|PX\|EXAT\|PXAT time] [NX\|XX] [VER\|ABS version][KEEPTTL]` |Perform increment or decrement operations on the value of the specified key, and the data type of `num` is LONG. |
|[EXINCRBYFLOAT](https://docs.byteplus.com/en/docs/redis/exstring#exincrbyfloat) |`[EXINCRBYFLOAT key num [MIN minval] [MAX maxval] [EX\|PX\|EXAT\|PXAT time] [NX\|XX] [VER\|ABS version] [KEEPTTL]` |Perform increment or decrement operations on the value of the specified key, and the data type of `num` is DOUBLE. |
|[EXCAS](https://docs.byteplus.com/en/docs/redis/exstring#excas) |`EXCAS key newvalue version` |When the input version is consistent with the version of the specified key, use the input `newvalue` to overwrite the original value. If the versions are inconsistent, return the current value and version information of the key. |
|[EXCAD](https://docs.byteplus.com/en/docs/redis/exstring#excad) |`EXCAD key version` |When the passed version is consistent with the version already set for the specified key, the key is deleted. |


<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* To use the ExString feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to technical support to apply for usage.

* After the application is completed, accounts with the Administrator role will have all permissions for ExString related commands by default. You can also create a new role that allows the use of all ExString commands according to business needs (that is, the ACL rule of this role needs to be set to `+@exstring`). After creating the role, you need to log in to Redis with an account that has this role to use ExString related commands. For specific procedures about creating a role, refer to [Creating role](https://docs.byteplus.com/en/docs/redis/create-role).

* The Cache for Redis supports big and hot key analysis for the ExString data type. It can help timely discover and analyze the details of hot keys and big keys in the database, providing data references for you to optimize hot keys and big keys. For specific procedures, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).

* After successfully applying for the use of the ExString function, the instance will no longer support any data recovery functions, including:

   * [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set)

   * [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point)

   * [Recovery from deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance)

* The Cache for Redis does not provide a command to delete ExString. However, you can use the following native Redis commands to achieve the purpose of deleting ExString.

   
   |command |Syntax |Description |
   |---|---|---|
   |[EXPIRE](https://redis.io/docs/latest/commands/expire/) |`EXPIRE key seconds [NX \| XX \| GT \| LT]` |Set the timeout for ExString. ExString that exceeds this time will be automatically deleted. |
   |[UNLINK](https://redis.io/docs/latest/commands/unlink/) |`UNLINK key [key ...]` |Asynchronously delete one or more ExString. When deleting an ExString with the `UNLINK` command, this ExString is marked as pending deletion, and the actual delete actions are carried out in the background thread without blocking the current Redis process. |
   |[DEL](https://redis.io/commands/del) |`DEL key [key ...]` |Synchronously delete one or more ExString. When deleting ExString with the `DEL` command, the delete action immediately blocks the current Redis thread until the memory space corresponding to ExString is completely withdrawn. If the amount of ExString data to be deleted is too large, it may affect the overall performance of Redis. |
   


<span id="exset"></span>
### EXSET


|Category |Description |
|---|---|
|Command syntax |`EXSET key value [EX\|PX\|EXAT\|PXAT time] [NX\|XX] [VER\|ABS\|GT version] [KEEPTTL]` |
|Time complexity |O(1). |
|Command description |Create a new key with value, or a new value for existing key settings. |
|Option |* `key`: The name of the key, used to specify the ExString as the object of the command call.<br><br>* `value`: The value set for the key.<br><br>* `EX time`: Specify the relative expiration time of the key. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `EXAT time`: Specify the absolute expiration time of the key in Unix timestamp format. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PX time`: Specify the relative expiration time of the key. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PXAT time`: Specify the absolute expiration time of the key in Unix timestamp format. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `NX`: Write data only if the key does not exist.<br><br>* `XX`: Write data only if the key exists.<br><br>* `VER version`: Version number. The value range is from 0 to the maximum value allowed by the Integer data type. Different scenarios have different version numbers in effect. Among which:<br><br>   * If the key exists:<br><br>      * And the incoming version number is equal to the current version number of the key, then write the value directly, and the version number will add 1 to the original version number.<br><br>      * But the incoming version number and the current version number of the key are not equal, then refuse to write the value and return the exception message.<br><br>   * If the key does not exist, then ignore the incoming version number and write the value directly. After the writing is successful, the version number becomes 1.<br><br>* `ABS version`: Absolute version number. The value range is from 0 to the maximum value allowed by the Integer data type. After setting, the value will be written directly, and the key's version number will be updated to the version number set by this option.<br><br>* `GT version`: Compare version numbers. The value range is from 0 to the maximum value allowed by the Integer data type. After setting, if the version number of the specified key is greater than the specified `GT` version, the value will be written, and the version number will increase by 1 from the original.<br><br>* `KEEPTTL`: Extend the expiration time of the key settings (Time to live, TTL information).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>KEEPTTL</code> cannot be set concurrently with <code>EX time</code>, <code>PX time</code>, <code>EXAT time</code>, <code>PXAT time</code> parameters.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If neither the <code>KEEPTTL</code> parameter is set, nor parameters for setting expiration time such as <code>EX time</code>, <code>EXAT time</code>, <code>PX time</code>, <code>PXAT time</code> are set, then the expiration time already set for the key will be deleted, meaning the key will not expire.   </div><br>    |
|Response |* `OK`: Execution succeeded.<br><br>* `nil`: `XX` argument is specified but key does not exist, or `NX` argument is specified but key already exists.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `update version is stale` and so on). |
|Example |* Command example 1<br><br>   Creates an ExString with a key name of t`est_exstring` and a value of `test_value1`, and sets the relative expiration time of the ExString to 10 seconds and the absolute version number to 100, specifying that it is written only if the key does not exist.<br><br>   ```Bash```<br>```   EXSET test_exstring test_value1 EX 10 NX ABS 100```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   OK```<br>```   ```<br>   <br><br>* Command example 2<br><br>   Assigns a new value `test_value2` to an existing ExString t`est_exstring` and sets the absolute expiration time of that ExString to 100 milliseconds with a version number of 100, specifying only writes if key exists.<br><br>   ```Bash```<br>```   EXSET test_exstring test_value2 PXAT 1739455218750 XX VER 100```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   OK```<br>```   ```<br>    |


<span id="exget"></span>
### EXGET


|Category |Description |
|---|---|
|Command syntax |`EXGET key` |
|Time complexity |O(1). |
|Command description |Query the value and version information of the specified key. |
|Option |`key`: The name of the key, used to specify the ExString as the object of the command call. |
|Response |* When the execution succeeds, the value and version information of the specified key will be returned.<br><br>* The corresponding exception information in other cases (such as `nil`, `wrong number of arguments for command`, and so on). |
|Example |Command example.<br><br>```Bash```<br>```EXGET test_exstring```<br><br><br>Response example.<br><br>```Bash```<br>```1) test_value1```<br>```2) 100```<br> |


<span id="exsetver"></span>
### EXSETVER


|Category |Description |
|---|---|
|Command syntax |`EXSETVER key version` |
|Time complexity |O(1). |
|Command description |Specify the version of the key. |
|Option |* `key`: The name of the key, used to specify the ExString as the object of the command call.<br><br>* `version`: The version number that requires settings. The value range is from 0 to the maximum value allowed by the Integer data type. |
|Response |* `1`: Execution succeeded.<br><br>* `0`: The specified key does not exist.<br><br>* The corresponding exception information in other cases (such as `syntax error` and so on). |
|Example |Command example.<br><br>```Bash```<br>```EXSETVER test_exstring 66```<br><br><br>Response example.<br><br>```Bash```<br>```1```<br> |


<span id="exincrby"></span>
### EXINCRBY


|Category |Description |
|---|---|
|Command syntax |`EXINCRBY key num [MIN minval] [MAX maxval] [EX\|PX\|EXAT\|PXAT time] [NX\|XX] [VER\|ABS version][KEEPTTL]` |
|Time complexity |O(1). |
|Command description |Perform increment or decrement operations on the value of the specified key, and the data type of num is LONG. |
|Option |* `key`: The name of the key, used to specify the ExString as the object of the command call.<br><br>* `num`: The value that needs to be increased or decreased must be an integer, where the positive integer is the value that needs to be increased, and the negative integer is the value that needs to be reduced.<br><br>* `MIN minval`: Specifies the minimum value of the key.<br><br>* `MAX maxval`: Specifies the maximum value of the key.<br><br>* `EX time`: Specify the relative expiration time of the key. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `EXAT time`: Specify the absolute expiration time of the key in Unix timestamp format. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PX time`: Specify the relative expiration time of the key. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PXAT time`: Specify the absolute expiration time of the key in Unix timestamp format. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `NX`: Write data only if the key does not exist.<br><br>* `XX`: Write data only if the key exists.<br><br>* `VER version`: Version number. The value range is from 0 to the maximum value allowed by the Integer data type. Different scenarios have different version numbers in effect. Among which:<br><br>   * If the key exists:<br><br>      * And the incoming version number is equal to the current version number of the key, then add or subtract actions directly, and the version number will add 1 to the original version number.<br><br>      * But the incoming version number and the current version number of the key are not equal, then refuse to increase the actions and return the exception message.<br><br>* `ABS version`: Absolute version number. The value range is from 0 to the maximum value allowed by the Integer data type. After settings, it will directly increase or decrease the actions, and modify the version number of the key to the version number set by this option.<br><br>* `KEEPTTL`: Extend the expiration time of the key settings (Time to live, TTL information).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>KEEPTTL</code> cannot be set concurrently with <code>EX time</code>, <code>PX time</code>, <code>EXAT time</code>, <code>PXAT time</code> parameters.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If neither the <code>KEEPTTL</code> parameter is set, nor parameters for setting expiration time such as <code>EX time</code>, <code>EXAT time</code>, <code>PX time</code>, <code>PXAT time</code> are set, then the expiration time already set for the key will be deleted, meaning the key will not expire.   </div><br>    |
|Response |* When the execution succeeds, the value obtained after the increase or decrease actions will be returned.<br><br>* When `MAX maxval` or `MIN minval` is set and the value obtained after the increment or decrement actions exceeds the range, such messages as `increment or decrement would overflow` will be returned.<br><br>* The corresponding exception information in other cases (such as `update version is stale` and so on). |
|Example |Suppose you have created an ExString using the command `EXSET test_exstring1 25 ABS 100`.<br><br>You can add 15 to the original value by the following command.<br><br>```Bash```<br>```EXINCRBY test_exstring1 15 MIN 35 VER 100```<br><br><br>Response example.<br><br>```Bash```<br>```40```<br> |


<span id="exincrbyfloat"></span>
### EXINCRBYFLOAT


|Category |Description |
|---|---|
|Command syntax |`[EXINCRBYFLOAT key num [MIN minval] [MAX maxval] [EX\|PX\|EXAT\|PXAT time] [NX\|XX] [VER\|ABS version] [KEEPTTL]` |
|Time complexity |O(1). |
|Command description |Perform increment or decrement operations on the value of the specified key, and the data type of `num` is DOUBLE. |
|Option |* `key`: The name of the key, used to specify the ExString as the object of the command call.<br><br>* `num`: The value that needs to be increased or decreased must be a floating\-point number, where the positive floating\-point number is the value that needs to be increased, and the negative floating\-point number is the value that needs to be decreased.<br><br>* `MIN minval`: Specifies the minimum value of the key.<br><br>* `MAX maxval`: Specifies the maximum value of the key.<br><br>* `EX time`: Specify the relative expiration time of the key. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `EXAT time`: Specify the absolute expiration time of the key in Unix timestamp format. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PX time`: Specify the relative expiration time of the key. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PXAT time`: Specify the absolute expiration time of the key in Unix timestamp format. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `NX`: Write data only if the key does not exist.<br><br>* `XX`: Write data only if the key exists.<br><br>* `VER version`: Version number. The value range is from 0 to the maximum value allowed by the Integer data type. Different scenarios have different version numbers in effect. Among which:<br><br>   * If the key exists:<br><br>      * And the incoming version number is equal to the current version number of the key, then add or subtract actions directly, and the version number will add 1 to the original version number.<br><br>      * But the incoming version number and the current version number of the key are not equal, then refuse to increase the actions and return the exception message.<br><br>* `ABS version`: Absolute version number. The value range is from 0 to the maximum value allowed by the Integer data type. After settings, it will directly increase or decrease the actions, and modify the version number of the key to the version number set by this option.<br><br>* `KEEPTTL`: Extend the expiration time of the key settings (Time to live, TTL information).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>KEEPTTL</code> cannot be set concurrently with <code>EX time</code>, <code>PX time</code>, <code>EXAT time</code>, <code>PXAT time</code> parameters.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If neither the <code>KEEPTTL</code> parameter is set, nor parameters for setting expiration time such as <code>EX time</code>, <code>EXAT time</code>, <code>PX time</code>, <code>PXAT time</code> are set, then the expiration time already set for the key will be deleted, meaning the key will not expire.   </div><br>    |
|Response |* When the execution succeeds, the value obtained after the increase or decrease actions will be returned.<br><br>* When `MAX maxval` or `MIN minval` is set and the value obtained after the increment or decrement actions exceeds the range, such messages as `increment or decrement would overflow` will be returned.<br><br>* The corresponding exception information in other cases (such as `update version is stale` and so on). |
|Example |Suppose you have created an ExString using the command `EXSET test_exstring1 25 ABS 100`.<br><br>You can subtract 3.1415926 from the original value by the following command.<br><br>```Bash```<br>```EXINCRBYFLOAT test_exstring1 -3.1415926 MAX 100 VER 100```<br><br><br>Response example.<br><br>```Bash```<br>```21.8584074```<br> |


<span id="excas"></span>
### EXCAS


|Category |Description |
|---|---|
|Command syntax |`EXCAS key newvalue version` |
|Time complexity |O(1). |
|Command description |When the input version is consistent with the version of the specified key, use the input `newvalue` to overwrite the original value. If the versions are inconsistent, return the current value and version information of the key. |
|Option |* `key`: The name of the key, used to specify the ExString as the object of the command call.<br><br>* `newvalue`: If the version passed is the same as the version of the specified key, the original value is overwritten with the passed `newvalue`.<br><br>* `version`: The version value used to compare with the current version of the specified key. The value range is from 0 to the maximum value allowed by the Integer data type. |
|Response |* `OK`: The command is executed successfully, and an empty string will be returned at the same time, as well as the latest version information of the key.<br><br>* `CAS_FAILED`: The command fails, and both the current value and version versions of the key are returned.<br><br>* `-1`: The specified key does not exist.<br><br>* The corresponding exception information in other cases (such as `syntax error`, `version should be integer`, and so on). |
|Example |Suppose an ExString `test_exstring1` already exists and needs to change its value to 66, but is unsure of its current value and version.<br><br>You can enter an arbitrary version (e.g. 35) in the following command and try to change the original value to 66.<br><br>```Bash```<br>```EXCAS test_exstring1 66 35```<br><br><br>Response example.<br><br>```Bash```<br>```1) CAS_FAILED```<br>```2) 30```<br>```3) 100```<br><br><br>From the above reply, we can see that the current value of `test_exstring2` is 30 and version is 100, then you can modify the original value to 66 by the following command.<br><br>```Bash```<br>```EXCAS test_exstring1 66 100```<br><br><br>Response example.<br><br>```Bash```<br>```1) OK```<br>```2)```<br>```3) 101```<br> |


<span id="excad"></span>
### EXCAD


|Category |Description |
|---|---|
|Command syntax |`EXCAD key version` |
|Time complexity |O(1). |
|Command description |When the passed version is consistent with the version already set for the specified key, the key is deleted. |
|Option |* `key`: The name of the key, used to specify the ExString as the object of the command call.<br><br>* `version`: The version value used to compare with the current version of the specified key. The value range is from 0 to the maximum value allowed by the Integer data type. |
|Response |* `1`: Execution succeeded.<br><br>* `0`: Execution failed.<br><br>* `-1`: The specified key does not exist.<br><br>* The corresponding exception information in other cases (such as `syntax error`, `version should be integer`, and so on). |
|Example |Suppose an ExString `test_exstring1` with version 100 already exists:<br><br><br>* Deleting `test_exstring1` will fail when using the following command.<br><br>   ```Bash```<br>```   EXCAD test_exstring1 101```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   0```<br>```   ```<br>   <br><br>* You can successfully delete `test_exstring1` when using the following command.<br><br>   ```Bash```<br>```   EXCAD test_exstring1 101```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   1```<br>```   ```<br>    |
