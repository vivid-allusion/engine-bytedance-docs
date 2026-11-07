---
title: "GetBucketNotificationV2"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketNotificationV2"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This API retrieves the event notification rules set for a specified bucket.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Notes


* You must be the bucket owner or have the GetBucketNotification permission authorized for the current bucket to call this API.

* HNS buckets do not currently support the GetBucketNotificationV2 API.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?notification_v2 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5LiO5raI5oGv5aS0"></span>
## Request parameters and headers


|**Name** |**Location** |**Parameter type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|notification_v2 |Query |String |Yes |\- |Special identifier representing the GetBucketNotificationV2 request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request **elements ** 

This request has no message elements.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## **Response headers**

This request returns common response headers. See [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## **Response body elements**


|**Name** |**Type** |**Sample value** |Note |
|---|---|---|---|
|Rules |Array |\- |Event notification rule information. |
|Events |Array |["tos:ObjectCreated: *", "tos:ObjectRemoved:* "] |Event type. For a list of types supported by TOS, see [Supported event types](https://docs.byteplus.com/en/docs/tos/Event-notification-overview?_vtm_=a78999.b69280.0_0.0_0.0.70_7654530873681135157#supported-event-types).<br><br>Parent node: Rules |
|Filter |Container |\- |Filter rules.<br><br>Parent node: Rules |
|TOSKey |Container |\- |Filter information for the object.<br><br>Parent node: Filter |
|FilterRules |Array |[<br><br>{"Name": "prefix",<br><br>"Value": "test_"<br><br>},<br><br>{<br><br>"Name": "suffix",<br><br>"Value": ".jpg" }<br><br>] |Filter rules that objects must match. Supports setting `prefix` and `suffix`, which filter event objects based on prefix and suffix rules respectively.<br><br><br>* If both prefix and suffix rules are set, the event must meet both to trigger a notification.<br><br>* If neither a prefix nor a suffix is set, all objects in the bucket will be matched.<br><br><br>Parent node: TOSKey |
|Name |String |prefix |Matching condition. The fields are described as follows:<br><br><br>* `prefix`: prefix.<br><br>* `suffix`: suffix.<br><br><br>Parent node: FilterRules |
|Value |String |test_ |Matching prefix and suffix information.<br><br>Parent node: FilterRules |
|RuleId |String |TestNotification |Event notification rule name must follow this convention:<br><br><br>* Event names must be unique within the bucket.<br><br>* Length must not exceed 255 characters.<br><br><br>If not set, TOS will automatically generate a rule name.<br><br>Parent node: Rules |
|Destination |Container |\- |Event notification push targets must include at least one target and support up to five different targets.<br><br>Parent node: Rules |
|ServiceManaged    |Boolean |true |The default value is `true`, indicating that the rule is a managed rule.<br><br>Parent node: Rules |
|ServiceManagedBy  |String |ServiceCode |The hosting provider's Service Code identifies the management service to which this rule belongs.<br><br>Parent node: Rules |
|VeFaaS |Array |[<br><br>{"FunctionId": "l2u0\*\*\*\*"}<br><br>] |The event delivery target is the function service.<br><br>Parent node: Destination |
|FunctionId |String |l2u0\*\*\*\* |The function ID for event delivery. You can log in to the [Function Service Console](https://console.byteplus.com/vefaas) and check the **Function ID** on the **Configuration** page of the function.<br><br>Parent node: VeFaaS |
|Kafka |Array |"Kafka":[<br><br>{<br><br>"Role":"trn:iam::214748\*\*\*\*:role/aaa",<br><br>"InstanceId":"kafka\-cnoeb1pq83rs\*\*\*\*",<br><br>"Topic":"test\-aaa",<br><br>"User":"bbbbb"<br><br>}<br><br>] |The event delivery target is the Kafka version of the message queue.<br><br>Parent node: Destination |
|Role |String |trn:iam::214748\*\*\*\*:role/aaa |Role TRN for authorizing TOS to access Kafka services.<br><br>Parent node: Kafka |
|InstanceId |String |kafka\-cnoeb1pq83rs\*\*\*\* |Kafka instance ID.<br><br>Parent node: Kafka |
|Topic |String |test\-aaa |Name of the Kafka topic.<br><br>Parent node: Kafka |
|User |String |bbb |Kafka user name.<br><br>Parent node: Kafka |
|Version |String |1698031811529301000 |Version number of the event notification rule.<br><br>Same level as Rules. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?notification_v2= HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response


* The event notification target is the function service

   ```JSON
   HTTP/1.1 200 OK
   Content-Length: 259
   Content-Type: application/json
   Date: Wed, 17 May 2023 12:18:08 GMT
   Server: TosServer
   X-Tos-Id-2: b2cb0164c600cacd6464c600-ac1023d1-1pzG6a-GBN-cgb-tos
   X-Tos-Request-Id: b2cb0164c600cacd6464c600-ac1023d1-1pzG6a-GBN-cgb-tos
   X-Tos-Server-Time: 7
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
               },
               "ServiceManaged": true,
               "ServiceManagedBy": "ServiceCode"
           }
       ],
       "Version": "1698031811529301000"
   }
   ```
   

* The event notification target is the Kafka version of the message queue

   ```Bash
   HTTP/1.1 200 OK
   Content-Length: 414
   Content-Type: application/json
   Date: Wed, 17 May 2023 12:18:08 GMT
   Server: TosServer
   X-Tos-Id-2: b2cb0164c600cacd6464c600-ac1023d1-1pzG6a-GBN-cgb-tos
   X-Tos-Request-Id: b2cb0164c600cacd6464c600-ac1023d1-1pzG6a-GBN-cgb-tos
   X-Tos-Server-Time: 7
   {
       "Rules": [
           {
               "Events": [
                   "tos:ObjectCreated:*",
                   "tos:ObjectRemoved:*"
               ],
               "Filter": {
                   "TOSKey": {
                       "FilterRules": [
                           {
                               "Name": "prefix",
                               "Value": "test_"
                           },
                           {
                               "Name": "suffix",
                               "Value": ".jpg"
                           }
                       ]
                   }
               },
               "RuleId": "event",
               "Destination": {
                   "Kafka": [
                       {
                           "Role": "trn:iam::214748****:role/aaa",
                           "InstanceId": "kafka-cnoeb1pq83rs****",
                           "Topic": "test-aaa",
                           "User": "bbbbb"
                       }
                   ]
               },
               "ServiceManaged": true,
               "ServiceManagedBy": "ServiceCode"
           }
       ],
       "Version": "1755056218115649299"
   }
   ```
