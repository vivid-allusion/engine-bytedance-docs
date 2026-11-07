---
title: "GetAuthorizationToken"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/getauthorizationtoken"
---

Obtain a temporary access key for logging into a Container Registry instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, we recommend selecting the service address according to the region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.ap\-southeast\-1.byteplusapi.com.cn?Action=GetAuthorizationToken&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Request parameter

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAuthorizationToken |The API name. The current API's name is `GetAuthorizationToken`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance. You can obtain the instance name from the **Instance List** page in the [Container Registry Console](https://console.byteplus.com/cr). |
|ExpiresAt |Long |No |1787565600 |The expiration time of the temporary access credential (Unix timestamp in seconds).<br><br><br>* The value range is from 10 minutes to 12 hours after the current time.<br><br>* If this parameter is not specified, the access credential expires 1 hour later by default. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://cr.ap-southeast-1.byteplusapi.com.cn?Action=GetAuthorizationToken&Version=2022-05-12
{
    "Registry": "registrya",
    "ExpiresAt": 1787565600
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Token |String |eyJ0eXAiOiJK\*\*\*\*\*\* |The temporary access key. |
|Username |String |dev_ops@\*\*\*\* |The username for logging into the Container Registry instance. |
|ExpireTime |String |2026\-08\-24T18:00:00Z |The expiration time of the temporary access key. It is a UTC+0 time in standard[ RFC3339 ](https://datatracker.ietf.org/doc/html/rfc3339)format. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260824143317****A98288BA4DE4B97",
        "Action": "GetAuthorizationToken",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Token": "eyJ0eXAiOiJK******",
        "Username": "dev_ops@****",
        "ExpireTime": "2026-08-24T18:00:00Z"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
