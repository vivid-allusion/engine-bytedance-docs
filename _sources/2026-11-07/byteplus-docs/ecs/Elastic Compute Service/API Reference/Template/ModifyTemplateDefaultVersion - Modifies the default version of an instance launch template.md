---
title: "ModifyTemplateDefaultVersion - Modifies the default version of an instance launch template"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyTemplateDefaultVersion"
---

Call the ModifyTemplateDefaultVersion operation to modify the default version of an instance launch template.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

When you start an instance by using an instance launch template, the default version is automatically used. We recommend that you specify the commonly used version of the instance launch template as the default version. This eliminates the repetitive task of manually selecting a version each time.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyTemplateDefaultVersion&groupName=%E5%90%AF%E5%8A%A8%E6%A8%A1%E7%89%88&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|A5dyS4">必选</span> `Sample value: ModifyTemplateDefaultVersion`

The action that you want to perform. Value: ModifyTemplateDefaultVersion.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|WTILz4">必选</span>   `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-ysxc16auaugh9zfy****`

The ID of the instance launch template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




**DefaultVersionNumber ** <span data-label="purple">integer </span><span data-api-tag="require|IQvruN">必选</span> `Sample value: 2`

Specifies the version number of the default version of the instance launch template.



**LaunchTemplateName ** <span data-label="purple">string </span>`Optional` `Sample value: templateNameDemo`

The name of the instance launch template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyTemplateDefaultVersion&Version=2020-04-01&LaunchTemplateId=lt-ysxc16auaugh9zfy****&DefaultVersionNumber=2 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220419160338010225133143077B****",
        "Action": "ModifyTemplateDefaultVersion",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified argument is invalid. |
