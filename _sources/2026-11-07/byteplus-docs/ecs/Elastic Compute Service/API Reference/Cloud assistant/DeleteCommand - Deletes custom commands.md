---
title: "DeleteCommand - Deletes custom commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteCommand_-_Deleting_a_custom_command"
---

Call the DeleteCommand operation to delete a custom command.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCommand&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|VvRleS">必选</span> `Sample value: DeleteCommand`

The action that you want to perform. Value: DeleteCommand.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|tV13vg">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**CommandId** <span data-label="purple">string</span> <span data-api-tag="require|R3BE8F">必选</span> `Sample value: cmd-4302d02424c5c8e10281e3a31****`

The custom command ID. You can call the [DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) operation to query and obtain custom command IDs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CommandId** <span data-label="purple">string</span> `Sample value: cmd-4302d02424c5c8e10281e3a31****`

The custom command ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteCommand&Version=2020-04-01&CommandId=cmd-ydckta****HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2023082415303301022514515207C4****",
        "Action":"DeleteCommand",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "CommandId":"cmd-ydckta****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |MissingParameter.CommandId |The required parameter CommandId is not supplied. |The command ID cannot be empty. |
|404 |InvalidCommand.NotFound |The specified Command does not exist. |The specified command does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
