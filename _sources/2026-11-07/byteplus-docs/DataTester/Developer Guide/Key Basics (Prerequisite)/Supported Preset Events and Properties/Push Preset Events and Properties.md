---
title: "Push Preset Events and Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Push-Preset-Events-and-Properties"
---


|Event name |Display name |Property |Property type |Property display name |
|---|---|---|---|---|
|rangers_push_send |Push operation \- server level sent successfully |$inactive |string |Is it a passive event? |
|||channel_id |float |Channel ID |
|||channel_type |string |channel type |
|||code |float |code |
|||content_language |string |content_language |
|||err |string |err |
|||push_batch_id |float |Batch ID |
|||push_config_id |float |Task ID |
|||push_uuid |string |push id |
|||task_unit_id |float |task_unit_id |
|||test_group |string |test_group |
|||message_id |string |message_id |
|||workflow_vids |list |workflow_vids |
|rangers_push_click |Push operation \- message click |channel_type |string |channel type |
|||message_id |string |message_id |
|||push_batch_id |float |Batch ID |
|||push_config_id |float |Task ID |
|||push_uuid |string |push id |
|||test_group |string |test_group |
|||$task_unit_id |float |task_unit_id |
|||workflow_vids |list |workflow_vids |
|rangers_push_show |Push operation \- message display |channel_type |string |channel type |
|||message_id |string |message_id |
|||push_batch_id |float |Batch ID |
|||push_config_id |float |Task ID |
|||push_uuid |string |push id |
|||test_group |string |test_group |
|||$task_unit_id |float |task_unit_id |
|||workflow_vids |list |workflow_vids |
|rangers_push_workflow |rangers_push_workflow |$inactive |string |Is it a passive event? |
|||push_batch_id |float |Batch ID |
|||push_config_id |float |Task ID |
|||push_unit_id |float |push_unit_id |
|||task_unit_id |float |task_unit_id |
|||workflow_type |string |workflow_type |
|||workflow_vids |list |workflow_vids |
|rangers_push |rangers_push |channel_type |string |channel type |
|||event_type |string |event_type |
|||message_id |string |message_id |
|||$extra |string |extra |
