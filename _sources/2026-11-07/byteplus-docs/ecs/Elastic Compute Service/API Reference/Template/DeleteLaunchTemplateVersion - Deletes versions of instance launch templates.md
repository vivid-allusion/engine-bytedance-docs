---
title: "DeleteLaunchTemplateVersion - Deletes versions of instance launch templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteLaunchTemplateVersion"
---

Call the DeleteLaunchTemplateVersion operation to delete a version of an instance launch template. You cannot delete the default version.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteLaunchTemplateVersion&groupName=%E5%90%AF%E5%8A%A8%E6%A8%A1%E7%89%88&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ArqLVi">必选</span> `Sample value: DeleteLaunchTemplateVersion`

The action that you want to perform. Value: DeleteLaunchTemplateVersion.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|mH1882">必选</span>  ` Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-ysxc16auaugh9zfy****`

The launch template ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




**LaunchTemplateName ** <span data-label="purple">string </span>`Optional` `Sample value: templateNameDemo`

The launch template name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




**DeleteVersions.N ** <span data-label="purple">integer[] </span><span data-api-tag="require|RyxKKb">必选</span> `Sample value: 2`

The version number of the instance launch template.


* Argument \- N: indicates the serial number of the version. Valid range: 1\-29.

* Separate multiple version numbers with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteLaunchTemplateVersion&Version=2020-04-01&LaunchTemplateId=lt-ysxc16auaugh9zfy****&DeleteVersions.1=1 HTTP/1.1
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
        "Action": "DeleteLaunchTemplateVersion",
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
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
