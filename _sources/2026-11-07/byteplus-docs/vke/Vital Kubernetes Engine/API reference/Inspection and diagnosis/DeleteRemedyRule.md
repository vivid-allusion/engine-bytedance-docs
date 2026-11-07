---
title: "DeleteRemedyRule"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteRemedyRule"
---

Deletes a check and self\-healing rule.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteRemedyRule&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteRemedyRule&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteRemedyRule |The API name. The API name is `DeleteRemedyRule`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|Id |String |Yes |R202609\*\*\*\* |The ID of the check and self\-healing rule. You can view the check and self\-healing rule ID in the console. For details, see [Configuring node check and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair?lang=en#.5p-l55yL5qOA5p-l6Ieq5oSI6KeE5YiZ). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=DeleteRemedyRule&Version=2022-05-12
Content-Type: application/json
{
    "Id": "R202609****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no API\-specific response parameters. For details about common response parameters, see [Response results](https://docs.byteplus.com/en/docs/vke/Response).

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteRemedyRule",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
