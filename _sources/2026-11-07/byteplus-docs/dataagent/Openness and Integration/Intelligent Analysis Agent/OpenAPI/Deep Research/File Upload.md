---
title: "File Upload"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/File_Upload"
---

<span id="81c5070f"></span>
### **Request description**

Request method: POST

Request URL: https://{domain}/dataAgent/llm/openApi/v2/deepresearch/uploadFile

<span id="31d834b2"></span>
### **Request parameters**


|Location |Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|FORM\-DATA |file |file |Yes |Binary file |File to be uploaded<br><br>Supports csv, xlsx, xls |
||fileType |string |Yes |xlsx |* csv<br><br>* xlsx<br><br>* xls |
||fileName |string |Yes |Product sales details.xlsx |File name |
||fileSize |int |Yes |110000 |File size, in bytes. The file size must not exceed 100 MB. |


<span id="e9322bff"></span>
### Request example

```JSON
curl --location --request POST 'https://{domain}/dataAgent/llm/openApi/v2/deepresearch/uploadFile' \
--form 'file=@"/Users/bytedance/Downloads/商品销售明细表.xlsx"' \
--form 'fileType="csv"' \
--form 'fileName="维度表"' \
--form 'fileSize="110000"'
```


<span id="0659a8ee"></span>
### Response parameters


|Location |Parameter |Type |Example value |Description |
|---|---|---|---|---|
|ROOT |storageKey |string |agent\-upload\-20250919144414\-7a2bfb6f00994e5ebbef52dfabe4ff2f |The storageKey of the file, used for the fileList field in the metadata of the task request |
||fileType |string |xlsx |File type |
||fileName |string |Product sales details.xlsx |File name |
||fileSize |int |110000 |File size, in bytes |


```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "fileName": "商品销售明细表.xlsx",
        "fileSize": 1953875,
        "fileType": "csv",
        "storageKey": "agent-upload-20250919144414-7a2bfb6f00994e5ebbef52dfabe4ff2f"
    },
    "msg": {}
}
```
