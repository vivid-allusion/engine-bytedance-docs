---
title: "DescribeChargeInfo"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeChargeInfo"
---

Call DescribeChargeInfo API to query the billing information of the workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|EngineType |String |Yes |PostgreSQL |Engine type. Values:<br><br><br>* `PostgreSQL`: PostgreSQL engine.<br><br>* `Supabase`: Supabase engine. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ChargeInfos |Array of [ChargeInfo](https://docs.byteplus.com/en/docs/330/106690#chargeinfo) |Refer to the sample response. |Billing information list. |


<span id="chargeinfo"></span>
### ChargeInfo


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ChargeMethod |String |SumHourly |Billing method. Range:<br><br><br>* `Unknown`: unknown type.<br><br>* `SumHourly`: cumulative hourly billing by usage. |
|ChargeType |String |CU |Billing method. The valid values for this parameter vary by engine type:<br><br><br>* For PostgreSQL engine, the valid values for this parameter are:<br><br>   * `CU`: PostgreSQL compute resource price.<br><br>   * `GiB`: PostgreSQL storage resource price.<br><br>* For Supabase engine, the valid values for this parameter are:<br><br>   * `SupabaseDBCU`: Supabase hosted database compute price.<br><br>   * `SupabaseDBGiB`: Supabase hosted database storage price.<br><br>   * `SupabaseTosGiB`: Supabase object storage price.<br><br>   * `SupabaseEdgeFunctionRequest`: Supabase edge function request price.<br><br>   * `SupabaseComponentCU`: Supabase general component compute price. |
|ChargeValue |Double |0.14 |Unit price. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeChargeInfo&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "EngineType": "Supabase"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeChargeInfo",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeInfos": [
            {
                "ChargeMethod": "SumHourly",
                "ChargeType": "SupabaseDBCU",
                "ChargeValue": 0.5
            },
            {
                "ChargeMethod": "SumHourly",
                "ChargeType": "SupabaseDBGiB",
                "ChargeValue": 0.00125
            },
            {
                "ChargeMethod": "SumHourly",
                "ChargeType": "SupabaseTosGiB",
                "ChargeValue": 0.0002
            },
            {
                "ChargeMethod": "SumHourly",
                "ChargeType": "SupabaseEdgeFunctionRequest",
                "ChargeValue": 0.14
            },
            {
                "ChargeMethod": "SumHourly",
                "ChargeType": "SupabaseComponentCU",
                "ChargeValue": 0.5
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
