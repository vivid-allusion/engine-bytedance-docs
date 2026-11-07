---
title: "ModifyImageAttribute – Modifies image information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyImageAttribute"
---

Call the ModifyImageAttribute operation to modify the name, description, boot mode, and other information of a custom image.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyImageAttribute&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|pO2UYC">必选</span> `Sample value: ModifyImageAttribute`

The action that you want to perform. Value: ModifyImageAttribute.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|VKq2Q8">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**BootMode** <span data-label="purple">string</span> `Optional` `Sample value: UEFI`

The image boot mode. If this parameter is left blank, the original configuration is retained. Value:


* BIOS: BIOS boot mode

* UEFI: UEFI boot mode


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">EBM instances only support the <code>UEFI</code> boot mode.</div>


* <div data-tips="true" data-tips-type="tip">For ARM images, the default value is <code>UEFI</code>, and this parameter can only be set to <code>UEFI</code>.</div>




**Description** <span data-label="purple">string</span> `Optional` `Sample value: This is my first image`

The image description.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), equal signs (=), English commas (,), English periods (.), Chinese commas (，), Chinese periods (。), and spaces.

* It must be 0 to 255 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is left blank, the original configuration is retained.</div>


* <div data-tips="true" data-tips-type="tip">When an empty string is passed in, the existing description information is cleared.</div>




**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|XV4Nfj">必选</span> `Sample value: image-ebgy1og99tfct0gw****`

You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and configure the `Visibility=private` parameter to query and obtain the ID of the custom image.



**ImageName** <span data-label="purple">string</span> `Optional` `Sample value: image-1`

The name of the image.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), and English periods (.).

* The name must be 1 to 128 characters in length.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyImageAttribute&Version=2020-04-01&ImageId=image-ebgy1og99tfct0gw****&ImageName=image1&Description= HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "ModifyImageAttribute",
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
|400 |InvalidBootMode.Malformed |The specified BootMode is malformed. |The specified boot mode is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified description is invalid. |
|400 |InvalidImageName.Malformed |The specified ImageName is malformed. |The specified image name is invalid. |
|400 |InvalidImageStatus |The specified image is not in the correct status for the request. |The current status of the image does not support this operation. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
