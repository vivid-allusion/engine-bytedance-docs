---
title: "StartWorkflow request examples"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/startworkflow-request-examples"
---

This article provides you with examples of common requests for the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) interface.

<span id="31eca005"></span>
## Trigger workflow in Vid mode

The following example demonstrates how to trigger the workflow `06853553c4d3402698a17ff5dff87fd7` via Vid with a GET method.

```HTTP
https://vod.byteplusapi.com?Action=StartWorkflow&Version=2023-01-01&Vid=v0d399g10001csunlgaljhtddi6hgvn0&TemplateId=06853553c4d3402698a17ff5dff87fd7
```


<span id="993bb45b"></span>
## Trigger workflow in DirectUrl mode

The following example demonstrates how to trigger the workflow `c3841b3122fd460db2bc99a6ec131cb8` with the file path `FileName` as a POST.

```JSON
{
    "DirectUrl": "{\"FileName\":\"vodtest.mp4\",\"SpaceName\":\"test-jinling\"}",
    "TemplateId": "c3841b3122fd460db2bc99a6ec131cb8"
}
```


<span id="00e858f2"></span>
## Dynamically set snapshot file path

The workflow `a378f66a5bc2495eb55fc14ac109625f` contains a snapshot task associated with the snapshot template `94c8d47c4c39440b8e6b4e0ce7a96776`. The following example demonstrates how to dynamically set the snapshot file path to `{{fileTitle}} _ {{templateId}}` using the `Snapshot` override parameter when triggering the workflow. For instance, if the source file name is `vodtest`, the generated file path for this snapshot would be `vodtest_ a378f66a5bc2495eb55fc14ac109625f`.

```JSON
{
    "Vid": "v0d399g10001csunlgaljhtddi6hgvn0",
    "TemplateId": "a378f66a5bc2495eb55fc14ac109625f",
    "Input": "{\"OverrideParams\": {\"Snapshot\": [{\"TemplateId\": [\"94c8d47c4c39440b8e6b4e0ce7a96776\"],\"FileName\": \"{{fileTitle}}_{{templateId}}\"}]}}"
}
```
