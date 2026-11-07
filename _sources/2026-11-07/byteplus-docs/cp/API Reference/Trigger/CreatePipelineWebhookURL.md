---
title: "CreatePipelineWebhookURL"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CreatePipelineWebhookURL"
---

Create a Webhook URL for the pipeline

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreatePipelineWebhookURL&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreatePipelineWebhookURL |The API name. The name of the current API is `CreatePipelineWebhookURL`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7815d4783edc47c5bbd7df024ab9\*\*\*\* |Workspace ID. |
|PipelineId |String |Yes |c3afa3f27d754ac8b6052bf3dc0b\*\*\*\* |Pipeline ID. |
|Type |String |no |Webhook |Trigger types.<br><br><br>* Webhook: General trigger<br><br>* CRWebhook: Image source trigger<br><br>* GitWebhook: Trigger for the Git code source |
|ResourceId |String |no | |Code source ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When Type is set to GitWebhook, you must enter the code source ID.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreatePipelineWebhookURL&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7815d4783edc47c5bbd7df024ab9****",
    "PipelineId": "c3afa3f27d754ac8b6052bf3dc0b****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|WebhookURL |String |https://cp.volces.com/v2/webhook/scm/eQKcyKfa7s02maKXrR_VoJi\*\*\*\* |WebhookURL |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "5202404071710430739950998FB2847****",
        "Action": "CreatePipelineWebhookURL",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "WebhookURL": "https://cp.volces.com/v2/webhook/scm/eQKcyKfa7s02maKXrR_VoJi****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have independent error codes. If an exception occurs during the API call, you can refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
