---
title: "Upload the File which is Used to Create the Cohorts"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Upload_the_File_which_is_Used_to_Create_the_Cohorts"
---

<span id="7f5f2182"></span>
## Request description

This interface uploads local files to the DataFinder and generates uuid_file_key that can be used to create clusters based on uploaded files later via OpenAPI.

**Path**:/openapi/v1/{app_id}/cohorts/upload_uuid

**Method**: POST

**Content\-type**: multipart/form\-data

<span id="1fc6908c"></span>
## Request parameters

**Path\-parameters** : reference test[API Description and Public Parameters](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters__)

**Body**:

```json
{
    "file": {二进制文件}, //binary file
}
```



|**Parameter** |**Type** |**Is it required?**  |**Describe** |
|---|---|---|---|
|file |form\-data |Yes |* The binary file to be uploaded, the file is in multipart/form\-data encoding format, where key: must be `'file '`.<br><br>* The file requirements to be uploaded are as follows:<br><br>   * The maximum file limit is 200m.<br><br>   * The supported file format is csv.<br><br>   * Supported headers are user_unique_id, and the second row starts with specific data |


<span id="72dc2b1a"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "uuid_file_key": "{file_key}"
    }
}
```


Field meaning description


|**Parameter** |**Type** |**Sample value** |**Describe** |
|---|---|---|---|
|uuid_file_key |string |upload_uuid/164314/20220819/1eb8f3c6\-4447\-4e9c\-a538\-c1b33a1cd0e4.csv |file_key after successful upload |


<span id="44915d8e"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
#For example, app_id = 164314

#For example, upload uuids.csv
method = 'POST'
service_url = '/datafinder/openapi/v1/164314/cohorts/upload_uuid'
headers = {}  #headers do not need to explicitly add the'Content-Type 'property, otherwise an error will be reported
files = {  #form-data format file
    'file': ('uuids.csv', open('uuids.csv', 'rb'))  #key must be'file ', value is uploaded csv file
}

resp = bc.request(method=method, service_url=service_url, headers=headers, files=files)
print(resp.content.decode('utf-8'))
```


<span id="689c0f35"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "uuid_file_key": "upload_uuid/164314/20220819/1eb8f3c6-4447-4e9c-a538-c1b33a1cd0e4.csv"
    }
}
```


<span id="9fa28c47"></span>
## The next step is to create a cluster

After uploading the file, you can then call the Create Cluster OpenAPI to create a cluster based on the uploaded file. The creation example is as follows. See the OpenAPI details for creating a cluster [Create a Cohort](https://docs.byteplus.com/docs/DataFinder/Create_a_Cohort).

```JSON
{
    "cohort_name": "文件创建分群-openapi", //file creation cohorts-openapi
    "description": "",
    "refresh_rule": 0, // It must be 0, which means does not support refresh.
    "cohort_type": 2, // Fixed as 2, which means file creation cohorts.
    "dsl_content": {
        "uuid_file_key": "upload_uuid/164314/20220819/1eb8f3c6-4447-4e9c-a538-c1b33a1cd0e4.csv", 
        //uuid_file_key need to upload the file through the upload file interface to obtain
        "file_list": [
            {
                "name": "user_unique_id_template (3).csv" The name of the uploaded file
            }
        ],
        "dsl_type": "user_unique_id" //Support user_unique_id, ssid, device_id, web_id
    }
}
```
