---
title: "GetVideoLibraryFolderTree"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree"
---

Gets information about the default category or a specific category and their subcategories under your account.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calling this API with an IAM user, you can only get information about the video library categories visible to that IAM user. For more information on how to configure the classification range of IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div>


<span id="requirements"></span>
## Requirements


* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with **Media library** \> **Videos** \> **Video library** \> **Edit** or **View only** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=GetVideoLibraryFolderTree&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetVideoLibraryFolderTree` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|FolderId |Long |No |`0` |Category ID. The default value is `0`, indicating that all subcategories under the default category will be returned. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FolderNode |Object of [FolderNode](https://docs.byteplus.com/en/docs/11/47203#foldernode) |`-` |Category information. |


<span id="foldernode"></span>
### FolderNode


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FolderId |Long |`0` |Category ID. |
|FolderName |String |`Category 1` |Category name. |
|FolderTypeForSubAccount |Integer |`-` |Subcategory information. |
|Children |Array of [Children](https://docs.byteplus.com/en/docs/11/47203#children) |`0` |The operational permissions on the category for IAM users used to call this API. Valid values:<br><br><br>* `0`: Highest permission. The IAM user can view and operate on the category and its resources, such as deleting resources or editing the category.<br><br>* `1`: The IAM user can view and operate on resources under the category, but cannot perform operations on the category itself, such as editing the category or creating subcategories.<br><br>* `2`: The IAM user can only view the category, but cannot view or operate on resources under the category.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When calling this API with the BytePlus account, the value of this parameter is fixed at <code>0</code>.</div><br> |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=GetVideoLibraryFolderTree&Version=2023-08-01&FolderId=0
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVideoLibraryFolderTree",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "FolderNode": {
            "FolderId": 0,
            "FolderName": "All files",
            "Children": [
                {
                    "FolderId": 17959466895819,
                    "FolderName": "Subcategory 1",
                    "Children": [
                        {
                            "FolderId": 17959465298105,
                            "FolderName": "Subcategory 2",
                            "Children": []
                        }
                    ]
                }
            ],
            "FolderTypeForSubAccount": 0
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
