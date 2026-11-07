---
title: "DeleteLaunchTemplateVersion - Deletes an instance launch template"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteLaunchTemplate"
---

Call the DeleteLaunchTemplate operation to delete an instance launch template. After you delete a template, all versions of the template are deleted.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteLaunchTemplate&groupName=%E5%90%AF%E5%8A%A8%E6%A8%A1%E7%89%88&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|OG2lSi">必选</span> `Sample value: DeleteLaunchTemplate`

The action that you want to perform. Value: DeleteLaunchTemplate.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|DgzyG6">必选</span>  ` Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LaunchTemplateName ** <span data-label="purple">string </span>`Optional` `Sample value: templateNameDemo`

The launch template name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-ysxc16auaugh9zfy****`

The launch template ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LaunchTemplateId ** <span data-label="purple">string </span>`Sample value: lt-ysxc16auaugh9zfy****`

The launch template ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteLaunchTemplate&Version=2020-04-01&LaunchTemplateId=lt-ysxc16auaugh9zfy**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202508011719557113C137BB09C2F24359",
        "Action": "DeleteLaunchTemplate",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "LaunchTemplateId": "lt-ysxc16auaugh9zfy****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
