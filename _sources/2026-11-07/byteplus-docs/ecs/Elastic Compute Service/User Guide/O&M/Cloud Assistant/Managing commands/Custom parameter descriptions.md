---
title: "Custom parameter descriptions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Custom-argument-description"
---

When creating a custom command, you can set custom parameters in the command content and configure usage rules for those parameters. After setting custom parameters, you can specify custom parameter values as needed before executing custom commands.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* You can create a maximum of 60 custom parameters in each custom command. Parameter names can contain numbers, letters, and underscores, but must not be empty strings. The maximum length of the parameter name is 64 bytes.

* The size of the command content must not exceed 16 KB.

* For custom parameters in public commands, you can only use them, but can not change their configurations.

   > If you need to use a public command and change its custom parameter configuration, you can clone the public command into a custom command first, then change the configuration. For details, refer to [Cloning into custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#cloning-a-custom-command).   
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Create a custom command. For detailed operations, refer to [Creating custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands).

2. In the content of a custom command, set a custom parameter in the `{{parameterName}}` format.

3. Enable the "Use argument" option. After this, you can view custom parameters in the command content that are automatically displayed under this option.

4. (**Optional**) You can configure the default value of the target parameter in the "Default value" column.

5. In the "Rule" column of the target parameter, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d9b7f0beb94b94aa7522a5f55b98218.png) </span> icon. Then, you can specify rules for custom parameter values in the pop\-up window, with rule details as follows.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Required |Select whether the custom parameter value is required. |Yes |
   |Argument Type |Select the type of the custom parameter value. Currently, only "String" and "Value" are supported. |String |
   |Minimum length |Configure the minimum length of this custom parameter value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Valid range of the minimum length: 1 \- 1000. The minimum length value must be less than the maximum length value.</div><br> |1 |
   |Maximum length |Configure the maximum length of this custom parameter value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Valid range of the maximum length: 1 \- 1000. The maximum length value must be more than the minimum length value.</div><br> |100 |
   

6. Click the "Confirm" button to complete the configuration.

7. When using this command afterwards, you need to provide the actual value for `{{parameterName}}`.
