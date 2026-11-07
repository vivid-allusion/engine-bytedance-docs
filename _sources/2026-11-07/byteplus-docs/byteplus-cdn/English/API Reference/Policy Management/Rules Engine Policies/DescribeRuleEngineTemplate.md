---
title: "DescribeRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_en-us"
---

Get the configuration details of a rules engine policy.


* If the policy has been published, the API returns the configuration details of the published version, which is the version with the status `running`.

* If the policy has not been published, the API returns the configuration details of the version with the status `draft`.


You can also specify a version of the policy to get the configuration details of that version.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeRuleEngineTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the ID of the rules engine policy you want to query.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to get the ID of the rules engine policy you want to query. |`tpl-sZRpwq` |
|TemplateVersion |String |No |Indicates a version of the policy. The API returns the configuration details of this version.<br><br>The default value of this parameter is as follows:<br><br><br>* If the policy has been published, the default value is the published version, which is the version with the status `running`.<br><br>* If the policy has not been published, the default value is `draft`.<br><br><br>You can call [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us) to get all versions of the policy. |`P-250414.89520` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|BoundDomains |Object[] |For the rules engine policy specified by `TemplateId`, this parameter indicates the list of domains bound to the policy.<br><br>If the rules engine policy is not bound to any domain, the value of this parameter is `null`. | |
|BoundTime |Long |Indicates the time when the rules engine policy was bound to the domain specified by `Domain`, in Unix timestamp format. |`1709174039` |
|Domain |String |Indicates a domain bound to the rules engine policy. |`www.example.com` |
|CreateTime |Long |Indicates the creation time of the rules engine policy, in Unix timestamp format. |`1709173909` |
|Exception |Boolean |Indicates whether there are special configurations in the rules engine policy. If special configurations exist, you cannot bind the policy to a domain. Please [submit a ticket](https://console.byteplus.com/workorder/create).<br><br>This parameter has the following values:<br><br><br>* `true`: Indicates that special configurations exist.<br><br>* `false`: Indicates that no special configurations exist. |`false` |
|Message |String |Indicates the description of the rules engine policy. |`This is a test` |
|ProdVersion |String |Indicates the published version of the rules engine policy, which is the version with the status `running`. If there is no version with the status `running`, the value of this parameter is empty (""). |`P-250414.89520` |
|Project |String |Indicates the project to which the rules engine policy belongs. |`default` |
|Rule |String |Indicates the content of the rule. You need to deserialize the rule content to extract the rule configuration. For a description of the rule configuration, see the description of the `Rule` parameter in [UpdateRuleEngineTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_en-us). | |
|Status |String |Indicates the status of the rules engine policy. This parameter has the following values:<br><br><br>* `locked`: Indicates that the status is "Published". For a published rules engine policy, you cannot modify its configuration.<br><br>* `editing`: Indicates that the status is "Draft". |`locked` |
|TemplateId |String |Indicates the ID of the rules engine policy. |`tpl-sZRpwq` |
|Title |String |Indicates the name of the rules engine policy. |`NetTVWeb001` |
|Type |String |Indicates the type of the rules engine policy. The value of this parameter is always `rule`. |`rule` |
|UpdateTime |Long |Indicates the last modification time of the rules engine policy, in Unix timestamp format.<br><br>If the rules engine policy has not been modified since its creation, the value of this parameter is the same as the value of `CreateTime`. |`1709173909` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025053003420680999F0B12D54B0FB5C8",
        "Action": "DescribeRuleEngineTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "BoundDomains": null,
        "CreateTime": 1748241181,
        "Exception": false,
        "Message": "test",
        "ProdVersion": "",
        "Project": "default",
        "Rule": "{\"IfBlock\":{\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Connective\":\"and\",\"Condition\":{\"Object\":\"always\"}}]}]},\"Actions\":[{\"Action\":\"redirect_request\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"redirect_request\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"source_path\",\"Values\":[\"^/docs/file1$\"]},{\"Name\":\"status_code\",\"Values\":[\"301\"]},{\"Name\":\"protocol\",\"Values\":[\"follow_client\"]},{\"Name\":\"target_host\",\"Values\":[\"www.example.com\"]},{\"Name\":\"target_path\",\"Values\":[\"^/cos1/file2$\"]},{\"Name\":\"target_query_action\",\"Values\":[\"include_all\"]}]}]}]},{\"Action\":\"allow_access\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"allow_access\",\"GroupParameters\":[{}]}]},{\"Action\":\"download_speed_limit\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"download_speed_limit\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"rate\",\"Values\":[\"100\"]},{\"Name\":\"rate_unit\",\"Values\":[\"B/s\"]},{\"Name\":\"after_size\",\"Values\":[\"15\"]},{\"Name\":\"after_size_unit\",\"Values\":[\"MB\"]}]}]}]},{\"Action\":\"request_header\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"request_header\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"action\",\"Values\":[\"set\"]},{\"Name\":\"header_name\",\"Values\":[\"myheader\"]},{\"Name\":\"header_value\",\"Values\":[\"myvalue\"]}]},{\"Parameters\":[{\"Name\":\"action\",\"Values\":[\"delete\"]},{\"Name\":\"header_name\",\"Values\":[\"myheader\"]}]}]}]},{\"Action\":\"deny_access\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"deny_access\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"status_code\",\"Values\":[\"465\"]}]}]}]},{\"Action\":\"cache_key\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"query_string\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"exclude_part\"]},{\"Name\":\"query_names\",\"Values\":[\"myparam1\",\"myparam2\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"include_part\"]},{\"Name\":\"query_names\",\"Values\":[\"ff\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"include_all\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"exclude_all\"]}]}]},{\"Dimension\":\"request_header\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"header_names\",\"Values\":[\"myheader\",\"myheader2\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]}]},{\"Dimension\":\"request_path\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"source_path\",\"Values\":[\"^/path1/$\"]},{\"Name\":\"target_path\",\"Values\":[\"^/path2/$\"]}]}]},{\"Dimension\":\"path_ignore_case\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"compression\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"compression\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"methods\",\"Values\":[\"gzip\",\"brotli\"]},{\"Name\":\"min_file_size\",\"Values\":[\"563\"]},{\"Name\":\"min_file_size_unit\",\"Values\":[\"KB\"]},{\"Name\":\"format\",\"Values\":[\"default\"]}]}]}]},{\"Action\":\"video_drag\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"video_drag\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"cache_time\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"cache_time\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"ttl\",\"Values\":[\"56\"]},{\"Name\":\"ttl_unit\",\"Values\":[\"day\"]},{\"Name\":\"cache_policy\",\"Values\":[\"origin_first\"]},{\"Name\":\"replenish\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_range\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_range\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_follow\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_follow\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_tcp_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"56\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]},{\"Action\":\"origin_http_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_http_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"read_timeout\",\"Values\":[\"58\"]},{\"Name\":\"read_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}]},\"ElseBlock\":{\"Actions\":[{\"Action\":\"redirect_protocol\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"redirect_protocol\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"status_code\",\"Values\":[\"301\"]},{\"Name\":\"protocol\",\"Values\":[\"https\"]}]}]}]}]}}",
        "Status": "editing",
        "TemplateId": "tpl-rejjo23",
        "Title": "rules-actions",
        "Type": "rule",
        "UpdateTime": 1748241181
    }
}
```


&nbsp;
