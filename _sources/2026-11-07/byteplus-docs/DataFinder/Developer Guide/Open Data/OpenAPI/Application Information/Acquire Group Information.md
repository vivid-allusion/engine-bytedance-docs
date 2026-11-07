---
title: "Acquire Group Information"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Acquire_Group_Information"
---

<span id="bc666fbd"></span>
# Request description

**Path**:openapi/v1/orgs/{org_id}

**Method**:GET

**Content\-type**: application/json

<span id="9496e830"></span>
## Request parameters

**Body**: Refer to public parameter description

<span id="0caa222c"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": [
       
        {
            "org_id": 2100230837,
            "org_name": "Demo experience",
            "is_admin": false,
            "apps": [
                {
                    "project_id": 2111833,
                    "project_name": "e-commerce-demo",
                    "project_display_name": "E-commerce demo",
                    "role": "member",
                    "app_id": 20000341,
                    "app_name": "E-commerce demo"
                }
            ]
        }
    ]
}
```


Field meaning description


|**Parameter** |**Type** |**Sample value** |**Describe** |
|---|---|---|---|
|org_id |int |2100230837 |Group ID |
|org_name |str |Demo experience |Group name |
|is_admin |bool |false |Is it an administrator? |
|apps |list |See return example |application information |


App information related:

<span id="83206379"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
res = bc.data_finder('/openapi/v1/orgs/10052')
print(res.content)
```


<span id="a9090f30"></span>
## Back to example

Return result:

```python
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "org_id": 10052,
            "org_name": "test_role",
            "apps": [
                {
                    "app_id": 374683,
                    "app_name": "test_role",
                    "app_en_name": "test_role"
                }
            ]
        }
    ]
}
```
