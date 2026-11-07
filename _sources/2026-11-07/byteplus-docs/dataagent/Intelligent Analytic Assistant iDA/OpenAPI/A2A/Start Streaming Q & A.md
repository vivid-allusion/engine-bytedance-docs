---
title: "Start Streaming Q & A"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Start_Streaming_Q_A"
---

<span id="f15c06b8"></span>
## A2A initiates streaming Q & A: `SendStreamingMessage`

<span id="qQiOTU2owe"></span>
### Request description


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/` |
|`method` |`SendStreamingMessage` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


The new version initiates data Q & A based on A2A (Agent\-to\-Agent) JSON\-RPC 2.0 protocol, initiates a round of **streaming questions** to the specified session through `SendStreamingMessage`methods, and the server level continuously pushes task status and products through **SSE (Server\-Sent Events)** .


1. Change imported parameters to JSON\-RPC 2.0 envelope structure ( `jsonrpc`/ `id`/ `method`/ `params`).

2. The response event is wrapped in an additional layer of `result`outside the original `task`/ `statusUpdate`/ `artifactUpdate`.

3. Create a session before calling and pass in the returned session ID as `message.metadata.sessionId`.


This protocol is only supported by the new version of IDA.

<span id="Zn7LmKhHu8"></span>
#### Authentication

**jwtToken** authentication.

<span id="wDRRjdRecM"></span>
### Request header


* `Authorization: Bearer ${JWT_TOKEN}`

* `Content-Type: application/json`


<span id="mr6dKKChC8"></span>
### Request parameters

The request body follows the JSON\-RPC 2.0 structure. `Message.metadata`**only supports the business fields listed in the following table** and does not inherit the full `TaskMetaData`of `executeTaskV2`; unlisted fields do not participate in task construction.


|Location |Parameter |Type |Is it required? |parameter transfer description |
|---|---|---|---|---|
|ROOT |jsonrpc |string |Yes |Fixed value `2.0` |
|ROOT |id |int/string |Yes |Request ID, which is backfilled to the response event as is |
|ROOT |method |string |Yes |Fixed value `sendStreamingMessage` |
|ROOT |params |object |Yes |JSON\-RPC parameter body |
|params |message |Message |Yes |user message body |
|params |sceneId |string/int |No |Scene ID; can also be placed in `message.metadata.sceneId`<br><br>Sources of data:[iDA - Acquiring Available Scenes and Skills](https://docs.byteplus.com/docs/dataagent/iDA_-_Acquiring_Available_Scenes_and_Skills) |
|params.message |role |string |No |Suggested `ROLE_USER`; bridge accepts `user`/ `agent`and `ROLE_ *`spelling |
|params.message |parts |List[Part] |Yes |Contains at least one non\-empty text part; no `kind`field on OpenAPI side |
|params.message |metadata |MessageMetadata |Yes |Session information and the following business fields |
|params.message.metadata |sessionId |string/int |Yes |`createSession`The session ID returned; recommended string<br><br>Sources of data:[iDA - Get Session List](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_Session_List) |
|params.message.metadata |type |string |No |Type of task, usually `deep_research` |
|params.message.metadata |version |string |No |Protocol version, usually `v5` |
|params.message.metadata |sceneId |string/int |No |Scene ID |
|params.message.metadata |traceContext |object |No |Business tracking context |
|params.message.metadata |enableWebSearch |bool |No |Enable web search |
|params.message.metadata |enableLarkQa / enableLarkQA |bool |No |Enable Lark Enterprise Q & A |
|params.message.metadata |enableConsultSearch |bool |No |Enable professional search |
|params.message.metadata |enableFastMode |bool |No |Enable fast mode |
|params.message.metadata |enableKnowledgeQA |bool |No |Enable data Q & A/knowledge Q & A mode |
|params.message.metadata |knowledgeQAType |string |No |Question and answer routing type; compatibility `knowledgeQA_type`, `knowledge_qa_type` |
|params.message.metadata |knowledgeContext |string |No |Knowledge recall context; compatibility `knowledge_context` |
|params.message.metadata |enableAeolusAssetSearch |bool |No |Enable Aeolus Asset Search |
|params.message.metadata |enableAssetLookup / enableAssetLookUp |bool |No |Enable AIDA asset lookup; both cases are supported |
|params.message.metadata |enableExplainChartDefinition |bool |No |Enable chart caliber interpretation |
|params.message.metadata |enableSlideGeneration |bool |No |Enable slide generation |
|params.message.metadata |enableWebApplicationGeneration |bool |No |Enable web app generation |
|params.message.metadata |enabledMCPServers |list |No |List of enabled MCP Servers |
|params.message.metadata |llmModel |string |No |specify model |
|params.message.metadata |imageAspectRatio |string |No |Image aspect ratio; compatible with `image_aspect_ratio`, `ratio` |
|params.message.metadata |skill |string |No |Explicitly specify a single Skill code |
|params.message.metadata |stepId |int |No |Step ID |
|params.message.metadata |templateId |int |No |Template ID; fill in when using the template[iDA - Get List of Prompt Templates](https://docs.byteplus.com/docs/dataagent/iDA_-_Get_List_of_Prompt_Templates) |
|params.message.metadata |templateShareToken |string |No |Template Share Token |
|params.message.metadata |templateVariables |list |No |Template variables; fill in when using templates |
|params.message.metadata |appIdList |list |No |Explicitly specify knowledge recall items; compatible `app_id_list` |
|params.message.metadata |kbIdList |list |No |Explicitly specified knowledge base; compatible `kb_id_list` |
|params.message.metadata |docIdList |list |No |Explicitly specifying knowledge documents; compatible `doc_id_list` |
|params.message.metadata |kbInfoMap |object |No |Specify knowledge base/document scope by project; compatible `kb_info_map` |


> **Session ID Contract**


1. A session must be created through `createSession`before calling. For details, see [iDA - Create Session](https://docs.byteplus.com/docs/dataagent/iDA_-_Create_Session).

2. It is recommended to pass the session ID as a string `to params.message.metadata.sessionId`.

3. The backend order of the bridge is: `params.sessionId`→ `params.metadata .sessionId`→ `params.message.metadata .sessionId`→ `params.contextId`→ `params.metadata .contextId`→ `params.message.metadata .contextId`. After getting it, it is uniformly converted to an integer; all are empty when sessionId is missing.


<span id="xPWAV2Wvyb"></span>
### Request example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "sendStreamingMessage",
  "params": {
    "message": {
      "role": "ROLE_USER",
      "parts": [
        { "text": "分析一下销售额趋势" }
      ],
      "metadata": {
        "sessionId": "8350",
        "type": "deep_research",
        "version": "v5",
        "enableKnowledgeQA": true,
        "enableWebSearch": true,
        "enableAssetLookUp": true
      }
    }
  }
}
```


<span id="cTvJuNziP1"></span>
### Curl example

```bash
curl -N -X POST "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --data-raw '{"jsonrpc":"2.0","id":1,"method":"SendStreamingMessage","params":{"message":{"role":"ROLE_USER","parts":[{"text":"分析一下销售额趋势"}],"metadata":{"sessionId":"6620","type":"deep_research","version":"v5"}}}}'
```


<span id="x4m1DJSrdo"></span>
### Example of a request using a template

When using templates, pass in `templateId`and `templateVariables`in `message.metadata`. `Parts [0] .text`still needs to provide non\-empty text; after the template is successfully rendered, the server level will perform the Q & A with the rendered full question. For template creation details, see [iDA -Create Prompt Template](https://docs.byteplus.com/docs/dataagent/iDA_-Create_Prompt_Template).

```json
{
  "jsonrpc": "2.0",
  "id": "req-template-demo-001",
  "method": "sendStreamingMessage",
  "params": {
    "message": {
      "role": "ROLE_USER",
      "parts": [
        { "text": "请使用指定模板生成营销活动日报" }
      ],
      "metadata": {
        "sessionId": "10001",
        "type": "deep_research",
        "version": "v5",
        "enableKnowledgeQA": true,
        "enableWebSearch": true,
        "templateId": 123,
        "templateVariables": [
          {
            "varId": "var_activity_name_demo",
            "value": { "text": "示例活动" }
          },
          {
            "varId": "var_activity_period_demo",
            "value": { "text": "2026-07-01 至 2026-07-31" }
          },
          {
            "varId": "var_data_source_demo",
            "value": {
              "text": "",
              "files": [
                {
                  "uid": "file_demo_001",
                  "name": "marketing_daily_demo.md",
                  "storageKey": "agent-public-upload-demo-redacted",
                  "fileName": "marketing_daily_demo.md",
                  "fileType": "md",
                  "fileSize": 2048,
                  "resourceType": "file"
                }
              ]
            }
          }
        ]
      }
    }
  }
}
```


**Field description:** 


* `TemplateId`: The template ID.

* `TemplateVariables [] .varId`: Must match the variable ID in the template definition.

* Text variables use `value.text`, file variables use `value.files`.

* The session ID, variable ID, file name, and storage key in the example are all desensitized placeholder values and cannot be used directly for real requests.



---



<span id="mEnwsmySJH"></span>
### Return parameters

The interface returns **SSE streaming responses** .

<span id="nihVLLsM4H"></span>
#### Response headers (recommended/required)


|Header |Is it required? |Example |Explain |
|---|---|---|---|
|Accept |Yes |`text/event-stream` |Streaming Response (SSE) |
|A2A\-Version |suggestion |`1.0` |A2A protocol version |


<span id="s9PmTbowoz"></span>
#### Return Data Format (SSE)


* `Content-Type: text/event-stream`

* Additional response headers: `X-Accel-Buffering: no`, `Cache-Control: no-cache, no-transform`

* Each line carries a JSON\-RPC result envelope prefixed with `data:`:


```text
data: {"jsonrpc":"2.0","id":1,"result":{ ... }}
```


The `result`is one of the following three types of events:


|Location |Parameter |Type |Description |
|---|---|---|---|
|result |task |DeepResearchTask |First Event, Task Initial Snapshot, Status `TASK_STATE_SUBMITTED` |
|result |statusUpdate |DeepResearchTaskStatusUpdateEvent |Task status update, `state`in order of `SUBMITTED → WORKING → COMPLETED` |
|result |artifactUpdate |DeepResearchTaskArtifactUpdateEvent |Product increment; `append = true`means `parts.text`is an additional increment (need to be spliced according to `artifactId`); `lastChunk = true`means the end of the fragment |


**Final state determination:**  `statusUpdate.status.state == TASK_STATE_COMPLETED`and `final == true`is the end of the round. The final conclusion text usually falls at the end of the `artifactUpdate parts.text`( `artifactId`of the form `final-fallback- *`).

<span id="qyPp3xroVh"></span>
#### SSE response example

```json
data: {"jsonrpc":"2.0","id":1,"result":{"task":{"id":"9105","contextId":"8350","status":{"state":"TASK_STATE_SUBMITTED"},"metadata":{"agentId":80,"phase":"submitted"}}}}

data: {"jsonrpc":"2.0","id":1,"result":{"statusUpdate":{"taskId":"9105","contextId":"8350","status":{"state":"TASK_STATE_WORKING"},"metadata":{"phase":"running"},"final":false}}}

data: {"jsonrpc":"2.0","id":1,"result":{"artifactUpdate":{"taskId":"9105","contextId":"8350","artifact":{"artifactId":"step-910504","name":"思考推理","parts":[{"text":"## 1. 简要结论","mediaType":"text/plain"}],"metadata":{"type":"deep_research_running_step","stepType":"executor_think"}},"append":true,"lastChunk":true}}}

data: {"jsonrpc":"2.0","id":1,"result":{"statusUpdate":{"taskId":"9105","contextId":"8350","status":{"state":"TASK_STATE_COMPLETED"},"metadata":{"phase":"completed"},"final":true}}}
```
