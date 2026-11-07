---
title: "Rules for setting ordered instance names"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Batch_setting_ordered_instance_names"
---

To facilitate instance management, RDS for MySQL allows you to specify ordered instance names. When you create instances in batches on the console or by calling an OpenAPI, you can specify ordered instance names for the created instances. This topic describes the detailed rules for specifying ordered instance names.

<span id="命名规则"></span>
## Naming rules

To enable ordered instance names, MySQL supports the specific syntax `name_prefix[begin_number,bits]name_suffix` for instance names. This syntax is based on the standard naming rules and adds an ordered field to the instance name. The fields in this syntax are described in the following table.


|Field |Type |Is it required? |description |
|---|---|---|---|
|name_prefix |String |Yes |The prefix of the instance name. The prefix must meet the following rules:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores ( _ ), and hyphens ( ). |
|begin_number |Integer |No |The starting number for the sequential instance names.<br><br><br>* Value range: [0,9999].<br><br>* Default value: 0. |
|bits |Integer |No |Specifies the number of digits for the ordered field in the instance name.<br><br><br>* Value range: [1,4].<br><br>* Default value: 4. |
|name_suffix |String |No |The suffix of the instance name can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The instance name specified by using the <code>name_prefix[begin_number,bits]name_suffix</code> syntax must be 1 to 128 characters in length.</div>


* <div data-tips="true" data-tips-type="tip">The separator between [begin_number,bits] must be a comma (,), with no spaces before or after it.</div>


* <div data-tips="true" data-tips-type="tip">If you specify <code>[]</code> or <code>[,]</code>, the value of begin_number starts from 0, and the default value of bits is 4.</div>


* <div data-tips="true" data-tips-type="tip">If the number of digits in the sum of begin_number and the number of instances to be created in batches is greater than the value of bits, the number of digits in the sum is used for creation. The sum of `begin_number` and the number of instances created in the batch cannot have more than 4 digits. Otherwise, the creation fails.</div>



<span id="使用示例"></span>
## Examples


|description |Input parameters |Number of instances |Instance name |
|---|---|---|---|
|Standard format |Prefix[1,3]Suffix |3 |prefix001suffix, name002suffix, name003suffix |
|Standard format, the number of digits for begin_number + number of instances \> specified bits |Prefix[99,2]suffix |3 |prefix099suffix, prefix100suffix, prefix101suffix |
|Standard format, begin_number + number of digits for the instance count \> 4 |Prefix[9999,4]suffix |2 |Failed to create |
|begin_number and bits are not specified |Prefix[]suffix or Prefix[,]suffix |3 |prefix0000suffix, prefix0001suffix, prefix0002suffix |
