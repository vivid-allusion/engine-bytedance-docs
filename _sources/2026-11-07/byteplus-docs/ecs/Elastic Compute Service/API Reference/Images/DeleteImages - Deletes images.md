---
title: "DeleteImages - Deletes images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteImages"
---

Call the DeleteImages operation to delete custom images.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

For prerequisites and precautions for calling this operation, see [Operation instructions](https://docs.byteplus.com/en/docs/ecs/Deleting-custom-images#.5pON5L2c6K-05piO).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteImages&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|lxdWM0">必选</span> `Sample value: DeleteImages`

The action that you want to perform. Value: DeleteImages.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|0jYaIG">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**DeleteBindedSnapshots** <span data-label="purple">boolean</span> `Optional` `Sample value: true`

Specifies whether to delete the corresponding snapshot or the snapshot consistency group when the image is deleted. Value:


* true (default value): Deletes.

* false: Does not delete.



**ImageIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|Pawcts">必选</span> `Sample value: ImageIds.1=image-ebgy1og99tfct0******&ImageIds.2=image-2asdv4n6ay3vj0******`

The ID of the custom image. A maximum of 100 IDs are supported. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and configure the `Visibility=private` parameter to query and obtain the ID of the custom image.


* Argument \- N: specifies the serial number of the image.

* Separate multiple image IDs with `&`.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters specific to this operation. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following <a href="https://docs.byteplus.com/en/docs/49/12931#.6ZSZ6K-v56CB">error codes for the operation</a> are returned only when invalid values are specified for request parameters. If valid values are specified for the request parameters, no error code is displayed, and a status code of <code>200</code> is returned. However, this does not mean that the operation on all images is successful. To view the operation result on one image, see the information in the following response parameters.</div>




**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details on the custom image.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error information for the failure to delete a specific image.


**Code** <span data-label="purple">string</span> `Sample value: InvalidImage.NotFound`

The error code for the failure of a specific request during batch request processing. Value:


* `InvalidImage.NotFound`: Indicates that the specified image does not exist.

* `InvalidImageStatus`: Indicates that the image in the current status does not support this operation.

* `InvalidImage.Shared`: Indicates that the specified image has been shared with other users.

* `OperationDenied.ImageIsCopying`: Indicates that the specified operation is denied because the image is being copied.

* `OperationDenied.ImageIsExporting`: Indicates that the specified operation is denied because the image is being exported.

* `InternalError`: Indicates an internal error. Try again. If multiple attempts fail, submit a ticket.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified image does not exist.`

The error information of an individual request during batch request processing. Value:


* `The specified image does not exist.`: Indicates that the specified image does not exist.

* `The specified image is not in the correct status for the request.`: Indicates that the image in the current status does not support this operation.

* `The specified image has already been shared and may be in use by other users.` : Indicates that the specified image has been shared with other users.

* `The specified operation is denied as your image is copying.`: Indicates that the specified operation is denied because the image is being copied.

* `The specified operation is denied as your image is exporting.`: Indicates that the specified operation is denied because the image is being exported.

* `An internal error has occurred.`: Indicates an internal error. Try again. If multiple attempts fail, submit a ticket.




**ImageId** <span data-label="purple">string</span> `Sample value: image-ebgy1og99tfct0******`

The image ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteImages&Version=2020-04-01&ImageIds.1=image-ebgy1og99tfct0****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20210611144510010225243100005******",
        "Action": "DeleteImages",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "ImageId": "image-ebgy1og99tfct0******",
                "Error": {
                    "Code": "InvalidImage.NotFound",
                    "Message": "The specified image does not exist."
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |LimitExceeded.MaximumImageIds |You've reached the limit on the number of ImageIds that you can set. |The specified number of image IDs exceeds the limit. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
