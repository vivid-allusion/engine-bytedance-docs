---
title: "PutBucketNotificationV2"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketNotificationV2"
---

## Feature description

This API sets event notification rules for a storage bucket (Bucket). Through event notifications, you can receive alerts when resources within the bucket change.

## Notes

* This API can only be used after the event notification feature is optimized and launched.

* To call this API, you must be the bucket owner or have the PutBucketNotification permission authorized for the current bucket.

* HNS buckets do not support the PutBucketNotificationV2 interface.

## Request syntax

```JSON
PUT /?notification_v2 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
{
    "Rules":[
        {
            "Events":[
                "tos:ObjectCreated:*",
                "tos:ObjectRemoved:*"
            ],
            "Filter":{
                "TOSKey":{
                    "FilterRules":[
                        {
                            "Name":"prefix",
                            "Value":"test_"
                        },
                        {
                            "Name":"suffix",
                            "Value":".jpg"
                        }
                    ]
                }
            },
            "RuleId":"string",
            "Destination":{
                "VeFaaS":[
                    {
                        "FunctionId":"function_id"
                    }
                ]
            }
        }
    ]
}
```

## Request parameters and headers

The public response headers returned by this request. See [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

|**Name** |**Location** |**Parameter Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|notification_v2 |Query |String |Yes |\- |Represents a special identifier for the PutBucketNotificationV2 request. |

## Request elements

|**Name** |**Type** |**Required** |**Sample value** |Note |
|---|---|---|---|---|
|Rules |Array |No |\- |Event notification rule information. |
|Events |Array |Yes |["tos:ObjectCreated: *", "tos:ObjectRemoved:* "] |Set the event types to notify. For a list of types supported by TOS, see [Supported event types](https://docs.byteplus.com/docs/tos/Event-notification-overview#.5pSv5oyB55qE5LqL5Lu257G75Z6L).<br><br>Parent node: Rules |
|Filter |Container |No |\- |Set filter rules.<br><br>Parent node: Rules |
|TOSKey |Container |No |\- |Currently supports setting FilterRule, which is the object's filter information.<br><br>Parent node: Filter |
|FilterRules |Array |No |[<br><br>{"Name": "prefix",<br><br>"Value": "test_"<br><br>},<br><br>{<br><br>"Name": "suffix",<br><br>"Value": ".jpg" }<br><br>] |Set the filtering rules that the target object must match. Supports setting `prefix` and `suffix` for filtering event objects by prefix and suffix rules respectively.<br><br><br>* If both prefix and suffix rules are set, events must meet both to trigger a notification.<br><br>* If neither a prefix nor a suffix is set, all objects in the bucket will be matched.<br><br><br>Parent node: TOSKey |
|Name |String |No |prefix |Set the conditions to match. The options are as follows:<br><br><br>* `prefix`: prefix.<br><br>* `suffix`: suffix.<br><br><br>Parent node: FilterRules |
|Value |String |Not supported |test_ |Set the prefix and suffix information to match.<br><br>Parent node: FilterRules |
|RuleId |String |No |TestNotification |Specify the event notification rule name, naming rules are as follows:<br><br><br>* Event names must be unique within the bucket.<br><br>* Length must not exceed 255 characters.<br><br><br>If not set, TOS will automatically generate the rule name.<br><br>Parent node: Rules |
|Destination |Container |Yes |\- |Set event notification push targets, including at least one target and support up to 5 different targets.<br><br>Parent node: Rules |
|VeFaaS |Array |No |[<br><br>{"FunctionId": "l2u0\*\*\*\*"}<br><br>] |Set the event delivery target to a function service, allowing multiple different function services to be set.<br><br>Parent node: Destination |
|FunctionId |String |Yes<br><br>> **tip**<br><br><br>> When the event delivery target is a function service, `FunctionId` is a required parameter.<br> |l2u0\*\*\*\* |Function ID for event delivery. You can log in to the [Function Service Console](https://console.byteplus.com/vefaas) and view the **Function ID** on the function **Configuration** page.<br><br>Parent node: VeFaaS |
|Kafka |Array |Yes<br><br>> **tip**<br><br><br>> The parameter `Kafka` is required only when the event delivery target is a Kafka message queue.<br> |"Kafka":[<br><br>{<br><br>"Role":"trn:iam::214748\*\*\*\*:role/aaa",<br><br>"InstanceId":"kafka\-cnoeb1pq83rs\*\*\*\*",<br><br>"Topic":"test\-aaa",<br><br>"User":"bbbbb"<br><br>}<br><br>] |Set the event delivery target to Kafka message queue. Multiple different Kafka instances can be configured.<br><br>Parent node: Destination |
|Role |String |Yes |trn:iam::214748\*\*\*\*:role/aaa |Role TRN. This role must be bound to the system preset policy KafkaAccessForTOS to authorize TOS to access the Kafka service.<br><br>Parent node: Kafka<br><br>> **tip**<br><br><br>> You need to create a role first, bind the system preset policy KafkaAccessForTOS to the role, and then obtain the role TRN.<br> |
|InstanceId |String |Yes |kafka\-cnoeb1pq83rs\*\*\*\* |Kafka instance ID.<br><br>Parent node: Kafka |
|Topic |String |Yes |test\-aaa |Name of the Kafka topic.<br><br>Parent node: Kafka |
|User |String |Yes |bbb |Kafka user name.<br><br>Parent node: Kafka |
|Version |String |No |1698031811529301000 |The version number of the event notification rule. Use the GetBucketNotificationV2 API to obtain this value.<br><br>Configuring the `Version` parameter ensures the atomicity of event notification rule settings. It is recommended to configure the `Version` parameter when modifying event notification rules through the PutBucketNotificationV2 API.<br><br>At the same level as Rules |

## **Response headers**

The public response headers returned by this request. See [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

## **Response body elements**

There are no message elements in the response for a successful request.

## Sample request

* Set event notifications to deliver to the function service

   ```JSON
   PUT /?notification_v2= HTTP/1.1
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Fri, 30 Jul 2021 13:53:55 +0000
   Authorization: authorization string
   {
       "Rules":[
           {
               "Events":[
                   "tos:ObjectCreated:*",
                   "tos:ObjectRemoved:*"
               ],
               "Filter":{
                   "TOSKey":{
                       "FilterRules":[
                           {
                               "Name":"prefix",
                               "Value":"test_"
                           },
                           {
                               "Name":"suffix",
                               "Value":".jpg"
                           }
                       ]
                   }
               },
               "RuleId":"TestNotification",
               "Destination":{
                   "VeFaaS":[
                       {
                           "FunctionId":"l2u0****"
                       }
                   ]
               }
           }
       ]
   }
   ```

* Set event notifications to deliver to the Kafka version of the message queue

   ```Bash
   PUT /?notification_v2= HTTP/1.1
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Wed, 13 Aug 2025 03:36:58 +0000 
   Authorization: authorization string
   {
       "Rules":[
           {
               "Events":[
                   "tos:ObjectCreated:*",
                   "tos:ObjectRemoved:*"
               ],
               "Filter":{
                   "TOSKey":{
                       "FilterRules":[
                           {
                               "Name":"prefix",
                               "Value":"test_"
                           },
                           {
                               "Name":"suffix",
                               "Value":".jpg"
                           }
                       ]
                   }
               },
               "RuleId":"event",
               "Destination":{
                   "Kafka":[
                       {
                           "Role":"trn:iam::214748****:role/aaa",
                           "InstanceId":"kafka-cnoeb1pq83rs****",
                           "Topic":"test-aaa",
                           "User":"bbbbb"
                       }
                   ]
               }
           }
       ]
   }
   ```

## Sample response

```JSON
HTTP/1.1 200 OK
Content-Length: 0
Date: Wed, 17 May 2023 12:18:08 GMT
Server: TosServer
X-Tos-Id-2: c25e0164c600b8df6464c600-ac1bb4fd-1pzG6a-PBN-cgb-tos-front-2
X-Tos-Request-Id: c25e0164c600b8df6464c600-ac1bb4fd-1pzG6a-PBN-cgb-tos-front-2
X-Tos-Server-Time: 165
```
