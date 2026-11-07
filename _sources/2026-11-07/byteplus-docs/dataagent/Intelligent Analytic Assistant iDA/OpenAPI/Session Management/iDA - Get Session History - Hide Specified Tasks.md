---
title: "iDA - Get Session History/Hide Specified Tasks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_Get_Session_History_Hide_Specified_Tasks"
---

<span id="63e3a670"></span>
### Request description


|Project |Content |
|---|---|
|request method |`GET`/ `POST`: Get session history snapshot; `DELETE`: Hide specified history task |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/sessionHistory` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|compatibility authentication |Support `x-token`and JWT Token |


The interface gets the historical task list by the session dimension, which is suitable for page recovery and backtracking the complete question and answer track. Each task is returned in a standard A2A Task structure, and `includeEvents`controls whether to carry task inputs, event stream details, and summary tags.

`GET`has the same query parameters as `POST`: `GET`uses the Query parameter, and `POST`uses the JSON Body. `DELETE`is used to hide the specified history task; if the task is still running, the server level will try to cancel the task before hiding it.

<span id="63df712e"></span>
### Request parameters


|Parameter name |Type |Required |Applicable method |Explain |
|---|---|---|---|---|
|`sessionId` |string / int |Yes |GET / POST / DELETE |Session ID; allows access only to sessions that belong to the current user |
|`offset` |int |No |GET / POST |Offset, the default is `0`; `pageToken`can be used instead, and `pageToken`takes precedence when both are passed in at the same time |
|`pageSize` |int |No |GET / POST |Number of entries per page, default `20`, range `1~ 100`; `limit` |
|`includeEvents` |bool |No |GET / POST |Whether to return task event stream details events `events`and input `input`, default `true` |
|`taskId` |string / int |Yes |DELETE |History task ID to hide |


<span id="31f187e1"></span>
### Request example

GET to get a snapshot of the session history:

```Plain
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/sessionHistory?sessionId=14541&offset=0&pageSize=20&includeEvents=true" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --silent | jq
```


POST Get a snapshot of the session history:

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/sessionHistory" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --data-raw '{"sessionId":14541,"offset":0,"pageSize":20,"includeEvents":true}' \
  --silent | jq
```


DELETE hides the specified history task:

```Plain
curl -X DELETE \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/sessionHistory" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --data-raw '{"sessionId":2481,"taskId":"661"}' \
  --silent | jq
```


<span id="01481567"></span>
### Return parameters

<span id="7352098e"></span>
### Top\-level return field


|Field path |Type |Explain |
|---|---|---|
|`session` |object |Session meta information. |
|`tasks` |array |Session history task list, paged back by timeline. |
|`nextPageToken` |string |Next page cursor; returns only if there is more data. |


<span id="0b09791c"></span>
### session field


|Field path |Type |Explain |
|---|---|---|
|`session.contextId` |integer |Exposed session ID. |
|`session.name` |string |Session name. |
|`session.data_set_id` |integer |null |
|`session.create_time` |string |Session creation time. |
|`session.last_active_time` |string |The last active time of the session. |
|`session.is_expired` |boolean |Whether the session has expired. |
|`session.restrict_mode` |integer |Session Restriction Mode. |
|`session.session_type` |string |Session type, such as `deep_research`. |
|`session.latest_task_status` |string |null |
|`session.is_mixed` |boolean |Whether it is a mixed session. |
|`session.mcp_servers` |array |List of session\-associated MCP Servers. |
|`session.version` |string |Session context version, such as `v5`. |
|`session.customTag` |array |Session custom tags. |
|`session.is_knowledge_qa` |boolean |Whether it is a knowledge Q & A session. |
|`session.scene` |string |Conversation scenarios, such as `data_set`. |
|`session.report_id` |integer |null |
|`session.query_history_id` |integer |null |
|`session.storage_id` |string |null |
|`session.origin_report_storage_id` |string |null |
|`session.origin_data_preview_mode` |string |null |
|`session.related_query_id` |integer |null |
|`session.related_query_question` |string |null |
|`session.related_query_data_set_id` |integer |null |
|`session.related_query_data_set_id_list` |array |null |
|`session.x_page_url` |string |null |
|`session.is_backend_created` |boolean |Is it created by the backend? |
|`session.submitted_via_internal_a2a` |boolean |Whether to submit through internal A2A. |
|`session.server_time` |string |Server level current time. |
|`session.file_list` |array |Session upload file list. |
|`session.generalAgentInfo` |object |Universal Agent Extension Information. |
|`session.linkEmbed` |array |session\-associated linked resources. |
|`session.extraInfo` |object |Session extension information. |


<span id="d4473582"></span>
### tasks field


|Field path |Type |Explain |
|---|---|---|
|`tasks[].task` |object |A2A Task projection information. |
|`tasks[].input` |object |The input message corresponding to this task. |
|`tasks[].events` |array |Task history events; not returned or empty when `includeEvents = false`. |
|`tasks[].summary` |object |Task summary tag. |


<span id="66c49b19"></span>
### tasks[].task field


|Field path |Type |Explain |
|---|---|---|
|`tasks[].task.id` |string |A2A Task ID, usually corresponding to the DeepResearch task ID. |
|`tasks[].task.contextId` |integer |Session ID. |
|`tasks[].task.status` |object |Task status object. |
|`tasks[].task.status.state` |string |A2A task state, such as `TASK_STATE_COMPLETED`. |
|`tasks[].task.metadata` |object |Task extension meta\-information. |
|`tasks[].task.metadata.version` |string |AIDA A2A extended version, such as `v5`. |
|`tasks[].task.metadata.sequence` |integer |Serial number. |
|`tasks[].task.metadata.phase` |string |Task phases such as `running`, `completed`, `failed`, `canceled`. |
|`tasks[].task.metadata.planStatus` |string |Scheduled states, such as `running`, `success`, `failed`, `canceled`. |
|`tasks[].task.metadata.agentId` |integer |Agent ID。 |
|`tasks[].task.metadata.deepResearchTaskId` |integer |DeepResearch mission ID. |
|`tasks[].task.metadata.messageId` |integer |Agent reply message ID. |
|`tasks[].task.metadata.relativeMessageId` |integer |The user enters the message ID. |
|`tasks[].task.metadata.createTime` |integer |Task creation timestamp in milliseconds. |
|`tasks[].task.metadata.timing` |object |Task time\-consuming information. |
|`tasks[].task.metadata.timing.createTime` |integer |Create timestamp in milliseconds. |
|`tasks[].task.metadata.timing.startTime` |integer |Start timestamp in milliseconds. |
|`tasks[].task.metadata.timing.endTime` |integer |End timestamp in milliseconds. |
|`tasks[].task.metadata.timing.durationMs` |integer |Task time (milliseconds). |


<span id="c7011434"></span>
### tasks[].input.message field


|Field path |Type |Explain |
|---|---|---|
|`tasks[].input.message.role` |string |Enter message roles; user input is usually `ROLE_USER`. |
|`tasks[].input.message.parts` |array |Message content snippet. |
|`tasks[].input.message.parts[].text` |string |Text content. |
|`tasks[].input.message.messageId` |string |Enter the message ID. |
|`tasks[].input.message.metadata` |object |Raw message metadata. |
|`tasks[].input.message.metadata.content.content.config` |object |Enter message configuration. |
|`tasks[].input.message.metadata.content.content.config.source` |string |Request source, such as `normal_chat`. |
|`tasks[].input.message.metadata.content.content.config.deepResearch` |boolean |Whether to open DeepResearch. |
|`tasks[].input.message.metadata.content.content.config.enableKnowledgeQA` |boolean |Whether to open the knowledge quiz. |
|`tasks[].input.message.metadata.content.content.config.enableWebSearch` |boolean |Whether to enable web search. |
|`tasks[].input.message.metadata.content.content.config.enableAeolusAssetSearch` |boolean |Whether to enable Aeolus asset search. |
|`tasks[].input.message.metadata.content.content.config.enableSkills` |array |List of enabled skills. |
|`tasks[].input.message.metadata.content.content.config.extraInfo` |object |Enter extended information. |
|`tasks[].input.message.metadata.content.content.config.generalAgentInfo` |object |Enter the generic Agent context to carry. |
|`tasks[].input.message.metadata.content.content.config.content` |string |User input. |


<span id="d0a02c32"></span>
### Tasks[].events field


|Field path |Type |Explain |
|---|---|---|
|`tasks[].events[].artifactUpdate` |object |Product update events are often used for steps, processes, and stages. |
|`tasks[].events[].message` |object |Message events are often used for final replies. |
|`tasks[].events[].statusUpdate` |object |Task status update events, often used in the final state. |


<span id="2383bfad"></span>
### artifactUpdate field


|Field path |Type |Explain |
|---|---|---|
|`artifactUpdate.taskId` |string |Associated task ID. |
|`artifactUpdate.contextId` |integer |Session ID. |
|`artifactUpdate.artifact` |object |Product object. |
|`artifactUpdate.append` |boolean |Whether to add to an existing product. |
|`artifactUpdate.lastChunk` |boolean |Whether it is the last sharding of the product. |
|`artifactUpdate.artifact.artifactId` |string |Product ID. |
|`artifactUpdate.artifact.name` |string |Product name. |
|`artifactUpdate.artifact.description` |string |Product description. |
|`artifactUpdate.artifact.parts` |array |Product content snippet. |
|`artifactUpdate.artifact.parts[].text` |string |Product text. |
|`artifactUpdate.artifact.parts[].mediaType` |string |Product media type, such as `text/plain`. |
|`artifactUpdate.artifact.metadata` |object |Product extension meta\-information. |
|`artifactUpdate.artifact.metadata.kind` |string |Meta information type, such as `step`. |
|`artifactUpdate.artifact.metadata.stepAction` |string |Step actions, such as `add_step`. |
|`artifactUpdate.artifact.metadata.stepType` |string |Step types, such as `executor_think`. |
|`artifactUpdate.artifact.metadata.stepId` |integer |Step ID. |
|`artifactUpdate.artifact.metadata.parentStepId` |integer |Parent step ID. |
|`artifactUpdate.artifact.metadata.stepStatus` |integer |Step status. |
|`artifactUpdate.artifact.metadata.displayProcess` |boolean |Whether to show the process. |
|`artifactUpdate.artifact.metadata.assets` |array |Step associate asset. |


<span id="43559c9b"></span>
### Message event field


|Field path |Type |Explain |
|---|---|---|
|`message.taskId` |string |Associated task ID. |
|`message.contextId` |integer |Session ID. |
|`message.role` |string |Message role; Agent replies to `ROLE_AGENT`. |
|`message.parts` |array |Message content snippet. |
|`message.parts[].text` |string |Reply to text. |
|`message.parts[].mediaType` |string |Media type, such as `text/plain`. |
|`message.messageId` |string |Message ID. |
|`message.metadata` |object |Message extension meta information. |
|`message.metadata.sequence` |integer |Event serial number. |
|`message.metadata.planStatus` |string |A planned state, such as `success`. |
|`message.metadata.conversationType` |string |Type of conversation, such as `research`. |
|`message.metadata.kind` |string |Message type, such as `report`. |
|`message.metadata.reportKind` |string |Report types, such as `markdown`. |
|`message.metadata.contentType` |string |Content types, such as `markdown`. |


<span id="938acc72"></span>
### statusUpdate field


|Field path |Type |Explain |
|---|---|---|
|`statusUpdate.taskId` |string |Associated task ID. |
|`statusUpdate.contextId` |integer |Session ID. |
|`statusUpdate.status` |object |Task state object. |
|`statusUpdate.status.state` |string |A2A task state, such as `TASK_STATE_COMPLETED`. |
|`statusUpdate.metadata` |object |State extension meta\-information. |
|`statusUpdate.metadata.sequence` |integer |Event serial number. |
|`statusUpdate.metadata.phase` |string |Task phase, such as `completed`. |
|`statusUpdate.metadata.planStatus` |string |A planned state, such as `success`. |
|`statusUpdate.metadata.plan_status` |string |Compatible snake_case plan status field. |
|`statusUpdate.metadata.timing` |object |Task time\-consuming information. |
|`statusUpdate.metadata.messageId` |integer |Agent reply message ID. |
|`statusUpdate.metadata.relativeMessageId` |integer |The user enters the message ID. |
|`statusUpdate.final` |boolean |Whether it is a task end\-state event. |


<span id="89c8d7fb"></span>
### Summary field


|Field path |Type |Explain |
|---|---|---|
|`tasks[].summary.hasFinalArtifact` |boolean |Is there a final product? |
|`tasks[].summary.hasFinalMessage` |boolean |Is there a final message? |


<span id="06065345"></span>
#### History snapshot return example

```Plain
{
  "session": {
    "contextId": 14541,
    "name": "OpenAPI Data Q&A",
    "data_set_id": null,
    "create_time": "2026-08-12 09:56:09",
    "last_active_time": "2026-08-12 10:55:14",
    "is_expired": false,
    "restrict_mode": 0,
    "session_type": "deep_research",
    "latest_task_status": "completed",
    "is_mixed": true,
    "mcp_servers": [],
    "version": "v5",
    "customTag": [],
    "is_knowledge_qa": false,
    "scene": "data_set",
    "report_id": null,
    "query_history_id": null,
    "storage_id": null,
    "origin_report_storage_id": null,
    "origin_data_preview_mode": null,
    "related_query_id": null,
    "related_query_question": null,
    "related_query_data_set_id": null,
    "x_page_url": null,
    "related_query_data_set_id_list": null,
    "is_backend_created": false,
    "submitted_via_internal_a2a": false,
    "server_time": "2026-08-12 10:55:44",
    "file_list": [],
    "generalAgentInfo": {},
    "linkEmbed": [],
    "extraInfo": {}
  },
  "tasks": [
    {
      "task": {
        "id": "15582",
        "contextId": 14541,
        "status": {
          "state": "TASK_STATE_COMPLETED"
        },
        "metadata": {
          "version": "v5",
          "sequence": 1,
          "phase": "completed",
          "planStatus": "success",
          "agentId": 430,
          "deepResearchTaskId": 15582,
          "messageId": 38105,
          "relativeMessageId": 38104,
          "createTime": 1786503308000,
          "timing": {
            "createTime": 1786503308000,
            "startTime": 1786503308092,
            "endTime": 1786503313725,
            "durationMs": 5725
          }
        }
      },
      "input": {
        "message": {
          "role": "ROLE_USER",
          "parts": [
            {
              "text": "Hello"
            }
          ],
          "messageId": "38104",
          "metadata": {
            "content": {
              "content": {
                "config": {
                  "source": "normal_chat",
                  "deepResearch": true,
                  "enableLarkQA": false,
                  "enableWebSearch": true,
                  "enableAeolusAssetSearch": false,
                  "enableKnowledgeQA": true,
                  "enableSkills": [],
                  "linkEmbed": [],
                  "extraInfo": {
                    "template": "Hello",
                    "skills": []
                  },
                  "llmModel": false,
                  "enable_report_search": true,
                  "version": 4,
                  "generalAgentInfo": {
                    "fileList": [],
                    "datasetList": [],
                    "larkFileList": [],
                    "reportList": []
                  },
                  "relatedQueryDataSetIdList": [],
                  "enableSlideGeneration": false,
                  "content": "Hello"
                }
              }
            }
          }
        }
      },
      "events": [
        {
          "artifactUpdate": {
            "taskId": "15582",
            "artifact": {
              "artifactId": "step-1558201",
              "metadata": {
                "version": "v5",
                "sequence": 1,
                "phase": "running",
                "planStatus": "running",
                "kind": "step",
                "stepAction": "add_step",
                "stepType": "executor_think",
                "stepId": 1558201,
                "parentStepId": 0,
                "stepStatus": 1,
                "displayProcess": true,
                "llmMessageIndex": 0,
                "type": "deep_research_running_step",
                "status": 1,
                "assets": [],
                "messageId": 38105,
                "relativeMessageId": 38104
              },
              "parts": [
                {
                  "text": "",
                  "mediaType": "text/plain"
                }
              ],
              "name": "Thinking and reasoning",
              "description": "Thinking and reasoning"
            },
            "append": false,
            "contextId": 14541,
            "lastChunk": true
          }
        },
        {
          "artifactUpdate": {
            "taskId": "15582",
            "artifact": {
              "artifactId": "step-1558202",
              "metadata": {
                "version": "v5",
                "sequence": 2,
                "phase": "running",
                "planStatus": "running",
                "kind": "step",
                "stepAction": "add_step",
                "stepType": "executor_think",
                "stepId": 1558202,
                "parentStepId": 1558201,
                "stepStatus": 1,
                "displayProcess": true,
                "llmMessageIndex": 0,
                "contentType": "text",
                "type": "deep_research_running_step",
                "status": 1,
                "assets": [],
                "messageId": 38105,
                "relativeMessageId": 38104
              },
              "parts": [
                {
                  "text": "Hello! Product update events are often used for steps, processes, and stages.😊",
                  "mediaType": "text/plain"
                }
              ],
              "name": "Thinking and reasoning",
              "description": "Thinking and reasoning completed"
            },
            "append": false,
            "contextId": 14541,
            "lastChunk": true
          }
        },
        {
          "message": {
            "taskId": "15582",
            "role": "ROLE_AGENT",
            "parts": [
              {
                "text": "Hello! Product update events are often used for steps, processes, and stages.😊",
                "mediaType": "text/plain"
              }
            ],
            "metadata": {
              "version": "v5",
              "sequence": 3,
              "planStatus": "success",
              "conversationType": "research",
              "messageId": 38105,
              "relativeMessageId": 38104,
              "kind": "report",
              "reportKind": "markdown",
              "contentType": "markdown"
            },
            "messageId": "38105",
            "contextId": 14541
          }
        },
        {
          "statusUpdate": {
            "taskId": "15582",
            "status": {
              "state": "TASK_STATE_COMPLETED"
            },
            "metadata": {
              "version": "v5",
              "sequence": 4,
              "phase": "completed",
              "planStatus": "success",
              "plan_status": "success",
              "timing": {
                "createTime": 1786503308000,
                "startTime": 1786503308092,
                "endTime": 1786503313725,
                "durationMs": 5725
              },
              "messageId": 38105,
              "relativeMessageId": 38104
            },
            "contextId": 14541,
            "final": true
          }
        }
      ],
      "summary": {
        "hasFinalArtifact": false,
        "hasFinalMessage": true
      }
    }
  ]
}
```


<span id="b41ddf4f"></span>
#### Hide History Task Return Example

```Plain
{
  "success": true,
  "sessionId": "2481",
  "taskId": "661",
  "taskCanceled": false
}
```
