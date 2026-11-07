---
title: "iDA - Acquisition Knowledge Base Project"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Acquisition_Knowledge_Base_Project"
---

GET dataAgent/llm/openApi/v2/deepresearch/tenantList

<span id="44d10179"></span>
### Interface description

Obtain the list of items (tenants) in the current organization under the knowledge engine, and must pass `org_id`.

<span id="49968430"></span>
### Request parameters (Query)


|Field |Type |Required |Default value |Explain |
|---|---|---|---|---|
|`org_id` |int/string |Yes |*  |Organization ID |


<span id="33f79787"></span>
### Return parameters


|Field |Type |Explain |
|---|---|---|
|`code` |string |Business code, success is `"llm/ok"` |
|`msg` |object |error message container |
|`data.total` |int |Total number of projects |
|`data.tenants` |array |List of items, including at least `app_id`/ `name`fields (returned by the pass\-through knowledge engine) |


<span id="fe084cb6"></span>
### Call example

Request:

```Bash
curl --location --request GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/tenantList?org_id=1" \
  --header "Authorization: Bearer ${JWT_TOKEN}" \
  --header 'Accept: application/json' \
  --silent | jq
```


Response:

```JSON
{
  "code": "llm/ok",
  "msg": {},
  "data": {
    "total": 2,
    "tenants": [
      {"app_id": 100, "name": "Data analysis project A"},
      {"app_id": 101, "name": "Data analysis project B"}
    ]
  }
}
```
