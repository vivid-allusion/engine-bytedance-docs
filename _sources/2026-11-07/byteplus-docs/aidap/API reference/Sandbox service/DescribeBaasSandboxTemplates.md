---
title: "DescribeBaasSandboxTemplates"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/describebaassandboxtemplates"
---

Call the DescribeBaasSandboxTemplates API to query sandbox templates.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBaasSandboxTemplates&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|TemplateName |String |No |python |Fuzzy match by template name. |
|TemplateId |String |No |rmtavlez953qnv7r\*\*\*\* |Match exactly by template ID. |
|TemplateSource |String |No |User |Match template source exactly; values are `System` or `User`. |
|Offset |Integer |No |0 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |10 |The number of returned items per page in paginated queries, ranging from 1 to 100; default is 10. Passing 0 uses the default value. |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of results matching the query criteria. |
|Templates |Array of [BaasSandboxTemplate](https://docs.byteplus.com/en/docs/330/124116#baassandboxtemplate) |Refer to the sample response. |Template list. |

### BaasSandboxTemplate

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TemplateDesc |String | <br><br>Python runtime environment |Template description; not returned if not configured. |
|TemplateId |String | <br><br>77gbcsv20q8kxklidjhe |Template ID. |
|TemplateName |String | <br><br>base\-python |Template name. |
|TemplateSize |String |800 |Template size. The unit is MB. |
|Tools |Array of String |[<br><br>                    "python",<br><br>                    "node",<br><br>                    "git",<br><br>                    "opencode"<br><br>                ] |Main preinstalled tool; returns nothing if not configured. |
|UpdateTime |String | <br><br>2026\-08\-01T02:30:00Z |Last update time (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`.<br><br>Not returned when there is no record. |

## Sample

Sample request

```JSON
POST /?Action=DescribeBaasSandboxTemplates&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```

Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202610261238568480E859D321E2D0F1BA-ff8dd7",
        "Action": "DescribeBaasSandboxTemplates",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Templates": [
            {
                "TemplateDesc": "e2b sandbox opencode template",
                "TemplateId": "rmtavlez953qnv7rsrsm",
                "TemplateName": "opencode",
                "TemplateSize": "800",
                "Tools": [
                    "python",
                    "node",
                    "git",
                    "opencode"
                ],
                "UpdateTime": "2026-08-25T12:43:38Z"
            },
            {
                "TemplateDesc": "e2b sandbox codex template",
                "TemplateId": "e7vtte6rsum0ch6ztol1",
                "TemplateName": "codex",
                "TemplateSize": "800",
                "Tools": [
                    "python",
                    "node",
                    "git",
                    "codex"
                ],
                "UpdateTime": "2026-08-25T12:43:12Z"
            },
            {
                "TemplateDesc": "e2b sandbox code-interpreter template",
                "TemplateId": "yp2zp7p8kigoi6p85z97",
                "TemplateName": "code-interpreter",
                "TemplateSize": "1024",
                "Tools": [
                    "python",
                    "node",
                    "git",
                    "jupyter"
                ],
                "UpdateTime": "2026-08-21T07:40:21Z"
            },
            {
                "TemplateDesc": "e2b sandbox base template",
                "TemplateId": "1pe3abjrt58t334kl283",
                "TemplateName": "base",
                "TemplateSize": "500",
                "Tools": [
                    "python",
                    "node",
                    "git"
                ],
                "UpdateTime": "2026-08-21T07:38:22Z"
            }
        ],
        "Total": 4
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
