---
title: "Event notification overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Event-notification-overview"
---

You can configure event notification rules to monitor changes to resources in TOS in real time. This topic provides background information and prerequisites for event notifications, as well as the event types supported by TOS.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

TOS can deliver notifications for certain event changes to BytePlus Function Service (veFaaS) and Message Queue for Kafka. For more information, see [What is veFaaS](https://docs.byteplus.com/en/docs/faas/What_is_Function_Service) and [What is Message Queue for Kafka](https://docs.byteplus.com/en/docs/kafka/what-is-message-queue-for-kafka).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Event notifications are currently only available in China (Beijing), China (Guangzhou), China (Shanghai), and Asia Pacific (Johor).

* After you create or modify an event notification rule, it will begin working within a few minutes. During this time, you may receive notifications for previous operations. To view only events that occurred after the rule took effect, we recommend filtering the data by the `eventTime` field.


<span id=".5pSv5oyB55qE5LqL5Lu257G75Z6L"></span>
## Supported event types


|**Event type** |**Event name** |**TOS API** |**Description** |
|---|---|---|---|
|tos:ObjectCreated:\* |tos:ObjectCreated:Put |PutObject |Triggered after an object is uploaded via simple upload. |
||tos:ObjectCreated:Post |PostObject |Triggered after an object is uploaded via form upload. |
||tos:ObjectCreated:Origin |GetObject |Triggered after TOS writes the requested object to the bucket via a back\-to\-origin rule. |
||tos:ObjectCreated:Fetch |FetchObject |Triggered after an object is fetched. |
||tos:ObjectCreated:Copy |CopyObject |Triggered after an object is successfully copied. |
||tos:ObjectCreated:CompleteUpload |CompleteUpload |Triggered after a multipart upload task is complete. |
||tos:ObjectCreated:Append |AppendObject |Triggered after a successful append operation. |
||tos:ObjectCreated:Modify |ModifyObject |Triggered after an object is modified.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only HNS buckets support <code>tos:ObjectCreated:Modify</code> events.</div><br> |
|tos:ObjectRemoved:\* |tos:ObjectRemoved:Delete |DeleteObject |Triggered after an object is deleted. This includes batch deletion. |
||tos:ObjectRemoved:DeleteMarkerCreated |DeleteObject |Triggered when a deletion mark is created. |
||tos:ObjectRemoved:TrashMoved |DeleteObject |Triggered after an object is deleted and moved to Recycle Bin.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only HNS buckets support <code>tos:ObjectRemoved:TrashMoved</code> events.</div><br> |
|tos:LifecycleExpiration:\* |tos:LifecycleExpiration:Delete |DeleteObject |Triggered after an object is permanently deleted via a lifecycle rule. |
||tos:LifecycleExpiration:DeleteMarkerCreated |DeleteObject |Triggered when a deletion mark is created via a lifecycle rule. |
||tos:LifecycleExpiration:TrashMoved |DeleteObject |Triggered after an object is deleted and moved to Recycle Bin via a lifecycle rule.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only HNS buckets support <code>tos:LifecycleExpiration:TrashMoved</code> events.</div><br> |
|tos:ObjectReplication:\* |tos:ObjectReplication:ObjectCreated |\- |Triggered after an object is created via a cross\-region or same\-region replication rule. |
||tos:ObjectReplication:ObjectModified |\- |Triggered after an object is overwritten via a cross\-region or same\-region replication rule. |
|tos:ObjectRestore:\* |tos:ObjectRestore:Post |RestoreObject |Triggered after a task is created to restore objects from Archive, Cold Archive, or Deep Cold Archive. |
||tos:ObjectRestore:Completed |RestoreObject |Triggered after a task to restore objects from Archive, Cold Archive, or Deep Cold Archive is complete. |
|tos:LifecycleTransition |tos:LifecycleTransition |\- |Triggered after the storage type of an object is changed via a lifecycle rule. |
|tos:ObjectRename |tos:ObjectRename |RenameObject |Triggered after an object is renamed using RenameObject. |


<span id=".5LqL5Lu26YCa55-l5qC85byP"></span>
## Event notification structure

The following is an example of a message that TOS sends to publish an tos:ObjectCreated:Put event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <code>events</code> parameter is an array type, and a single notification may contain multiple events.</div>


```json
{"events": [
      {
       "eventName":"tos:ObjectCreated:Put",
        "eventSource":"tos",
        "eventTime":"2022-08-29T08:50:54Z",
        "eventVersion":"1.0",
        "tos":{
            "bucket":{
                "trn":"trn:tos:::test",
                "name":"test",
                "ownerIdentity":"2100000000"
             },
             "object":{
                 "eTag":"\"cbd8273ce352dfac24d5d65fa3f8****\"",
                 "key":"aa.png",
                 "size":29098,
                 "versionId":"57CE0809CDADB97E****"
             },
             "tosSchemaVersion":"1.0",
             "ruleId":"testput",
             "region":"cn-beijing",
             "requestParameters":{
                 "sourceIPAddress":"192.160.**.***:*****",
                 "customParameters": "image"
             },
             "responseElements":{
                 "requestId":"99cb480c7dee50d6630c7dee-ac14****"
             },
             "userIdentity":{
                 "principalId":"trn:iam::2100000000:user/test"
            }
        }        
     }
  ]
}
```


The parameters are described below:


|**Parameter** ||||**Category** |**Example value** |**Description** |
|---|---|---|---|---|---|---|
|eventName ||||String |tos:ObjectCreated:Put |The type of the event. For a list of types supported by TOS, see [Supported event types](https://docs.byteplus.com/docs/tos/Event-notification-overview#.5pSv5oyB55qE5LqL5Lu257G75Z6L). |
|eventSource ||||String |tos |Fill in **tos** as the source of the event notification message. |
|eventTime ||||String |2022\-08\-29T08:50:54Z |The time when the event occurred. Expressed in ISO\-8601 format. |
|eventVersion ||||String |1.0 |The event notification version number is currently **1.0**. |
|tos |bucket |trn ||String |trn:tos:::test |The unique identifier of the bucket, in the format `trn:tos:::<bucketname>`. |
|||name ||String |test |The name of the bucket. |
|||ownerIdentity ||String |2100100000 |The ID of the BytePlus account that created the bucket. |
||object |eTag ||String |"cbd8273ce352dfac24d5d65fa3f8\*\*\*\*" |The ETag of the object. This parameter is empty for deleteMarkerCreate events. |
|||key ||String |aa.png |The name of the object. |
|||size ||Integer |29098 |The size of the object. This parameter is 0 for deleteMarkerCreate events. |
|||versionId ||String |57CE0809CDADB97E\*\*\*\* |Object version ID. For deleteMarkerCreate events, this parameter is the ID of the deletion mark. |
|||originKey ||String |abc.txt |The name of the source object in scenarios where the object is renamed using RenameObject, or deleted and moved to Recycle Bin. |
||tosSchemaVersion |||String |1.0 |The version number of this field domain is currently **1.0**. |
||ruleId |||String |testput |The name of the configured event notification rule. |
||region |||String |cn\-beijing |The region where the bucket is located. |
||requestParameters |sourceIPAddress ||String |`192.160.**.***:*****` |The source IP address of the request. |
||responseElements |requestId ||String |99cb480c7dee50d6630c7dee\-ac14\*\*\*\* |Request ID. |
||userIdentity |principalId ||String |trn:iam::2100000000:user/test |The BytePlus account used by the requester:<br><br><br>* If the requester is using a master account, enter the ID of that account.<br><br>* If the requester is using a sub account, use this format to fill in the field: `trn:iam::<AccountID>:user/<username>`. |
||archiveEventData |restoreEventData |restorationExpiryTime |String |2024\-02\-02T00:00:00Z |The expiration time of the temporary copy generated after restoration, in ISO\-8601 format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter <code>restorationExpiryTime</code> is only present for <code>tos:ObjectRestore:Completed</code> events after archived, cold archived, or deep cold archived objects are successfully restored.</div><br> |
||||restoreStorageClass |String |ARCHIVE |The storage type from which the object will be retrieved. The values are explained as follows:<br><br><br>* ARCHIVE: Archive<br><br>* COLD_ARCHIVE: Cold Archive<br><br>* DEEP_COLD_ARCHIVE: Deep Cold Archive<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter <code>restoreStorageClass</code> is only present for <code>tos:ObjectRestore:Completed</code> events after archived, cold archived, or deep cold archived objects are successfully restored.</div><br> |
||lifecycleEventData |transitionEventData |destinationStorageClass |String |INTELLIGENT_TIERING |The storage type to which the object will transition via a lifecycle rule. The values are explained as follows:<br><br><br>* IA: Infrequent Access Storage<br><br>* INTELLIGENT_TIERING: Intelligent Tiering<br><br>* ARCHIVE_FR: Flashback Archive<br><br>* ARCHIVE: Archive<br><br>* COLD_ARCHIVE: Cold Archive<br><br>* DEEP_COLD_ARCHIVE: Deep Cold Archive<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter <code>destinationStorageClass</code> is only present for <code>tos:LifecycleTransition</code> events after objects have been successfully transitioned using lifecycle rules.</div><br> |


<span id=".5pON5L2c5q2l6aqk"></span>
## Rule hosting

When creating an event notification rule for a particular cloud service, you can designate it as a "hosted rule" by specifying certain parameters. TOS users only have read access to these rules.

<span id="8RS3w9tl"></span>
### **Prerequisites**


* You have activated TOS and [created a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* You have enabled other services that require event notification rules to be hosted, such as PFS and EFS.


<span id="7JrNpLDc"></span>
### **Notes**


|**Category** |**Description** |
|---|---|
|**Ability provider** |The hosting action itself takes place at the corresponding hosting service. |
|**Permissions required** |* Once a rule is hosted, it becomes read\-only. It cannot be modified or deleted through the TOS console or API<br><br>* The cloud service hosting the rule has full lifecycle management permissions, including the ability to read, modify, and delete the rule. |
|**Hosting service identifier** |The TOS console displays **the name of the hosting service** if a rule is hosted by another service, such as PFS. |
|**Canceling hosting** |The hosting service initiates hosting actions. You cannot cancel hosting directly on the TOS side. Contact the hosting service provider to find out if canceling hosting is possible. |


&nbsp;
