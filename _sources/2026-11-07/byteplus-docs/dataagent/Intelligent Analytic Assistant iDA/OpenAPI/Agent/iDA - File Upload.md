---
title: "iDA - File Upload"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_File_Upload"
---

<span id="81c5070f"></span>
### **Request description**

Request method: POST

Request address: https://{domain}/dataAgent/llm/openApi/v2/vieSearch/uploadFile

<span id="31d834b2"></span>
### **Request parameters**


|Location |Parameter |Type |Is it required? |Sample value |Describe |
|---|---|---|---|---|---|
|FORM\-DATA |file |file |Yes |binary file |Files to be uploaded<br><br>Support csv, xlsx, xls |
||fileType |string |Yes |xlsx |* csv<br><br>* xlsx<br><br>* xls |
||fileName |string |Yes |Merchandise sales list.xlsx |file name |
||fileSize |int |Yes |110000 |File size, in Bytes, cannot exceed 100MB. |


<span id="e9322bff"></span>
### Request example

```JSON
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/uploadFile" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --form 'file=@"/Users/yuean/Desktop/1/e-commerce platform sale data_test.xlsx"' \
  --form 'fileType="csv"' \
  --form 'fileName="e-commerce platform sale data_test.xlsx"' \
  --form 'fileSize=110000' \
  --silent | jq
```


<span id="0659a8ee"></span>
### Return parameters


|Location |Parameter |Type |Sample value |Description |
|---|---|---|---|---|
|ROOT |storageKey |string |agent\-upload\-20250919144414\-7a2bfb6f00994e5ebbef52dfabe4ff2f |The storageKey of the file, used to execute the fileList field in the task request metadata |
||fileType |string |xlsx |file type |
||fileName |string |Merchandise sales list.xlsx |file name |
||fileSize |int |110000 |File size in Bytes |


```JSON
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "data": {
      "sophonStorageKey": null
    },
    "fileName": "e-commerce platform sale data_test.xlsx",
    "fileSize": 65578,
    "fileType": "csv",
    "message": "success",
    "storageKey": "agent-upload-20260810183222-80446e56e8384158bf122a98a4c5f377",
    "success": true
  },
  "msg": {}
}
```
