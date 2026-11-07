---
title: "Add TOS files through the API"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Add_TOS_files_through_the_API"
---

This topic describes how to import files from Volcengine Object Storage (TOS) into the knowledge space of a multimodal search scenario via API. After submitting the import task, the system automatically parses and imports the files. You can check the progress and results through the task query interface.

## Prerequisites

* A multimodal search scenario is created, initialized, and configured. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario), [initialize a multimodal search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario), and [Configure a multimodal search scenario](https://docs.byteplus.com/en/docs/contextsearch/Configure_a_multimodal_search_scenario).

* Private network access or public network access is enabled, and the corresponding access address is obtained. For more information, see [View configuration information](https://docs.byteplus.com/en/docs/contextsearch/View_multimodal_configuration_information).

* Credentials have been obtained for interface authentication. For more information, see [View configuration information](https://docs.byteplus.com/en/docs/contextsearch/View_multimodal_configuration_information).

* The files to be imported have been uploaded to BytePlus TOS, and the TOS address of the files has been obtained. For specific operations, see [View file details](https://docs.byteplus.com/en/docs/tos/docs-viewing-file-details).

## Procedure

### Submit an import task

Call the `POST /v1/spaces/{space_id}/ingest` API to submit the import task and pass the TOS file address to the system.

#### Request header parameters description

|**Parameter** |**Required** |**Description** |
|---|---|---|
|X\-Admin\-Token |Yes |Management interface authentication token. |
|X\-Caller\-Id |Yes |Business user identifier, accepts any string value. Example: `my-app-user-001`. |
|Content\-Type |Yes |Fixed value `application/json`. |

#### Request body parameters description

|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|urls |Array |Yes |List of TOS files to import. Each element contains the `url` field and an optional `custom_data` field. |
|urls[].url |String |Yes |TOS file address, formatted as `tos://bucket/path/filename`. |
|urls[].custom_data |Object |No |Custom key\-value pairs to attach business metadata to the documentation. |
|connector_type |String |Yes |Fixed value `tos`, indicating import from object storage. |
|authz_provider |String |No |Permission control method, default is `local`. |
|authz_visibility |String |No |Document visibility with the following valid values:<br><br><br>* public (public)<br><br>* restricted (restricted)<br><br>* no_search (not searchable)<br><br><br>Default value is `restricted`. |
|authz_subject_keys |Array |No |Accessible subject list, effective when authz_visibility is restricted. Format example: ["user:123", "dept:engineering"]. |

#### Request example

```Bash
curl -X POST 'https://{访问地址}/v1/spaces/default/ingest' \
  -H 'X-Admin-Token: <admin_token>' \
  -H 'X-Caller-Id: caller-user-123' \
  -H 'Content-Type: application/json' \
  -d '{
    "urls": [
      {
        "url": "tos://bucket/path/doc-1.pdf",
        "custom_data": {
          "department": "engineering",
          "category": "design-doc"
        }
      },
      {
        "url": "tos://bucket/path/doc-2.docx"
      }
    ]
  }'
```

#### Response example

```JSON
{
  "task_id": "task_123",
  "space_id": "default",
  "connector_type": "tos",
  "status": "pending"
}
```

> **tip**

> Successful interface submission only indicates task creation, not file import completion. Use the returned `task_id` to query the task status.

### Query task status

Call `GET /v1/spaces/{space_id}/tasks/{task_id}` to check task status and confirm if file parsing and storage are complete. Storage tasks run asynchronously. After submitting a task, use this interface to check task details and processing results for each document.

#### Request header parameter description

|**Parameter** |**Required** |**Description** |
|---|---|---|
|X\-Admin\-Token |Yes |Management interface authentication token. |

#### Request body parameter description

|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|items_offset |Integer |No |Pagination offset, default `0`. |
|items_limit |Integer |No |Number of items returned per page, default is `100`. |

#### Request example

```Bash
curl -X GET 'https://{访问地址}/v1/spaces/default/tasks/task_123?items_offset=0&items_limit=100' \
  -H 'X-Admin-Token: <admin_token>'
```

#### Response example

```JSON
{
  "task_id": "task_123",
  "space_id": "default",
  "connector_type": "tos",
  "status": "succeeded",
  "item_total": 2,
  "item_succeeded": 2,
  "item_failed": 0,
  "tokens": 0,
  "affected_doc_ids": ["doc_1", "doc_2"],
  "error_code": "",
  "error_message": "",
  "items": [
    {
      "source_url": "tos://bucket/path/doc-1.pdf",
      "doc_id": "doc_1",
      "status": "succeeded",
      "tokens": 0,
      "error_code": "",
      "error_message": ""
    },
    {
      "source_url": "tos://bucket/path/doc-2.docx",
      "doc_id": "doc_2",
      "status": "succeeded",
      "tokens": 0,
      "error_code": "",
      "error_message": ""
    }
  ],
  "items_offset": 0,
  "items_limit": 100,
  "created_at": 1781020000000,
  "updated_at": 1781020300000
}
```

#### Response parameter description

|**Parameter** |**Description** |
|---|---|
|task_id |Unique task identifier. |
|status |Overall task status, valid values are as follows:<br><br><br>* pending (waiting)<br><br>* running (in progress)<br><br>* succeeded (all successful)<br><br>* failed (some failed)<br><br><br>Because the import task runs asynchronously, polling every 2–5 seconds is recommended until `status` is `succeeded` or `failed`. |
|item_total |Total number of submitted documents. |
|item_succeeded |Number of successfully processed documents. |
|item_failed |Number of failed documents. |
|affected_doc_ids |List of document IDs generated after successful storage |
|items |Processing details for each document, including `source_url`, `doc_id`, `status`, `error_code`, and `error_message`. |

When the task status is `succeeded`, it means the file has been parsed and stored successfully and can be searched in multimodal search scenarios.

## FAQs

### Returns 401 ADMIN_TOKEN_REQUIRED

Check whether the X\-Admin\-Token is correctly included in the request header.

### Returns 503 ADMIN_TOKEN_NOT_CONFIGURED

The server has not configured the Admin Token. Contact the administrator to complete the configuration.

### Task status remains `pending` for an extended time

Confirm the scene is published and the service is running

### File parsing failed (`item status` is `failed`)

Check whether the TOS file path is correct, the file format is supported, and the TOS permissions have been granted for ContextSearch to read.
