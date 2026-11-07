---
title: "Trigger event message structure"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Trigger_event_message_structure"
---

The trigger passes Json formatted message data as an event parameter to your function, triggering function execution. The message data structure passed by different triggers varies; this document summarizes the message structures of all triggers that connect to FaaS.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The event parameters for different runtime languages may vary slightly; please refer to the actual parameters.</div>


<span id="timer-trigger"></span>
## Timer trigger

The message structure of the Timer trigger event is as follows:

```json
// Example event 
{
  "id": "9cab1030-dccf-4b61-ae07-542bffef****",
  "source": "/faas/event/timer/{timer_id}",
  "specversion": "1.0",
  "time": "2022-11-22T04:28:07.945838513Z",
  "type": "faas.timer.event"
  "datacontenttype": "application/octet-stream",
  "data": "Hello byteplus",

}
```



|Parameter |Type |Description |
|---|---|---|
|id |string |CloudEvent proprietary field: Request ID, each request has a unique ID. |
|source |string |CloudEvent proprietary field: The value for the Timer trigger is `/faas/event/timer/{timer_id}`. |
|specversion |string |Cloudevent proprietary field: cloudevent version. |
|time |string |Message trigger time, the time format is an ISO 8601 formatted timestamp. |
|type |string |cloudevent proprietary fields: event type, the value for Timer trigger is `faas.timer.event`. |
|datacontenttype |string |cloudevent proprietary field: message type, all as `application/octet-stream`. |
|data |string |Message content. |


<span id="api-gateway-trigger"></span>
## API Gateway trigger

The message structure of the API Gateway trigger event is as follows:

```json
        // Example event
        {
          "httpMethod": "GET",
    "path": "/",
    "pathParameters": {
        "path": "value"
    },
    "queryStringParameters": {
        "foo": "bar"
    },
    "headers": {
        "Host": "10.243.***.***:9001",
        "User-Agent": "curl/7.79.1",
        "Accept": "*/*",
        "Accept-Encoding": "gzip",
        "X-Faas-Request-Id": "b7e5ac05-cf6a-466a-86d4-093b24c3****"
    },
    "body": "{\"hello\": \"veFaaS\"}"
        }
```



|**Parameter** |**Description** |
|---|---|
|httpMethod |HTTP request methods, including POST, GET, PUT, DELETE, HEAD, OPTIONS. |
|path |HTTP request path. |
|pathParameters |Parameter of the HTTP request path. |
|queryStringParameters |Query parameter of the HTTP request path. |
|headers |HTTP request headers. For sub\-parameter description, refer to the headers parameter description below. |
|body |HTTP request payload. |


The headers parameter description is as follows:


|**Parameter** |**Description** |
|---|---|
|Host |Address of the `function instance`, format: Instance IP:port. |
|User\-Agent |Browser identity string. |
|Accept |Browser\-accepted file types. |
|Accept\-Encoding |Encoding formats that the browser can accept. |
|X\-Faas\-Request\-Id |Unique identifier for the function request. |


<span id="kafka-trigger"></span>
## Kafka trigger

The message structure of the Kafka trigger event is as follows:

```json
// Example event 
{
  "id": "cb57fdb4-1c12-490d-b556-b8c70054****", 
  "source": "/faas/event/kafka/{trigger_id}", 
  "type": "faas.kafka.event", 
  "specversion": "1.0", 

  "datacontenttype": "application/octet-stream", 
  "time": "2022-04-26T08:55:36.723908863Z", 
  "data": "user data", 
  
  "extensions": {
    "topic": "test_topic", 
    "partition": "9", 
    "consumergroup": "test_topic_xw1t1yqz", 
    "offset": "34", 
    
    "key": "" 
  }
}
```



|Parameter |Type |Description |
|---|---|---|
|id |string |CloudEvent's proprietary field: request ID, each request has a unique ID. |
|source |string |cloudevent proprietary field: The value for the Kafka trigger is `/faas/event/kafka/{trigger_id}`. |
|type |string |Type\-specific field for cloudevent: event type, Kafka trigger value is `faas.kafka.event`. |
|specversion |string |Cloudevent proprietary field: cloudevent version. |
|datacontenttype |string |Cloudevent proprietary field: Message type, all are `application/octet-stream`. |
|time |string |Message trigger time, the time format is an ISO 8601 timestamp. |
|data |string |Message content. |
|extensions |\- |Extended information of the event. For sub\-parameter description, refer to the description of the extensions parameter below. |


The extensions parameter description is as follows:


|Parameter |Type |Description |
|---|---|---|
|topic |string |Message source Topic. |
|partition |string |Partition of the message source. |
|consumergroup |string |Consumer group of the message source. |
|offset |string |Consumption point. |
|key |string |Message Key. |


<span id="rocketmq-trigger"></span>
## RocketMQ trigger

RocketMQ trigger event message structure is as follows:

```json
// Example event 
{
   "id":"2372345f-950e-432f-b6bf-6293dd36****",
   "source":"/faas/event/rocketmq/{trigger_id}",
   "type":"faas.rocketmq.event",
   "specversion":"1.0",
      
   "datacontenttype":"application/octet-stream",
   "time":"2022-10-10T03:13:47.085293242Z",
   "data":"DATA SENT BY THE PRODUCER", 
   
   "extensions":{
       "topic":"MQ_INST_85bcoh8hirzg_mw2fx%topic-zero", // [instance-id]%[topic-name]
       "queueid":"6",
       "consumergroup":"MQ_INST_85bcoh8hirzg_mw2fx%GID_group_3", // [instance-id]%[group-name]
       "offset":"18183",

       "msgid":"0A41C2EB12F50000000030c216100006", 
       "tags": "abc" 
    }
}
```



|Parameter |Type |Description |
|---|---|---|
|id |string |Cloudevent proprietary field: request id, each request has a unique id. |
|source |string |Cloudevent proprietary field: The value for RocketMQ trigger is `/faas/event/rocketmq/{trigger_id}`. |
|type |string |CloudEvent specific fields: event type, the value for RocketMQ trigger is `faas.rocketmq.event`. |
|specversion |string |Cloudevent proprietary field: Cloudevent version. |
|datacontenttype |string |CloudEvent proprietary field: message type, all are `application/octet-stream`. |
|time |string |Message trigger time, the time format is an ISO 8601 timestamp. |
|data |string |Message content. |
|extensions |\- |Extension information for the event. For a description of sub\-parameters, refer to the extensions parameter description below. |


The extensions parameter description is as follows:


|Parameter |Type |Description |
|---|---|---|
|topic |string |Message source topic. |
|queueid |string |Queue id of the message source. |
|consumergroup |string |Message consumption group of the source. |
|offset |string |Consumption offset. |
|msgid |string |Message id. |
|tags |string |message tag information. |


<span id="tos-trigger"></span>
## TOS trigger

TOS trigger event message structure is as follows:

```json
//Example event
{
   "specversion":"1.0",
   "id":"1124807578fd9936307578f-ac17****",
   "source":"/faas/event/tos/{bucket_name}",
   "type":"faas.tos.event",
   "datacontenttype":"application/octet-stream",
   "time":"2022-08-25T11:06:29.043768218Z",
   "data":{
      "events":[
         {
            "eventName":"tos:ObjectCreated:Put",
            "eventSource":"tos",
            "eventTime":"2022-08-25T11:05:51Z",
            "eventVersion":"1.0",
            "tos":{
               "bucket":{
                  "trn":"trn:tos:::test",
                  "name":"test",
                  "ownerIdentify":"200000****"
               },
               "object":{
                  "eTag":"cd163b393cf54d961f9959842ff1****",
                  "key":"build.sh",
                  "size":188,
                  "versionId":"57CE0809CDADB97E****"
               },
               "tosSchemaVersion":"1.0",
               "ruleId":"303436663662383932300ee348075767****",
               "region":"cn-beijing",
               "requestParameters":{
                  "sourceIPAddress":"192.160.**.***:*****"
               },
               "responseElements":{
                  "requestId":"1124807578fd9936307578f-ac17****"
               },
               "userIdentity":{
                  "principalId":"trn:iam::200000****:root"
               }
            }
         }
      ]
   }
}
```



|Parameter |Type |Description |
|---|---|---|
|specversion |string |cloudevent proprietary field: cloudevent version. |
|id |string |cloudevent proprietary field: request id, each request has a unique id. |
|source |string |Type\-specific field for cloudevent: TOS trigger is `/faas/event/tos/{bucket_name}`. |
|type |string |Type\-specific field for cloudevent: event type, TOS trigger value is `faas.tos.event`. |
|datacontenttype |string |Cloudevent proprietary field: the message type, all are `application/octet-stream`. |
|time |string |Message trigger time, timestamp in ISO 8601 format. |
|data |string |TOS event notification specifics. |


<span id="tls-trigger"></span>
## TLS trigger

TLS trigger event message structure is as follows:

```json
// Example event
{
    'id': 'f42307b3-5cd6-4d92-9dc7-b4559175****', 
    'source': '/faas/event/tls/4o3f****', 
    'type': 'faas.tls.event', 
    'specversion': '1.0', 
    
    'datacontenttype': 'application/octet-stream', 
    'time': '2024-07-09T15:41:01.977924767Z', 
    'data': {
        '__path__': '/var/log/emlmsobj/0.log', 
        '__source__': '192.**.**.**', 
        '__tag____client_ip__': '192.**.**.**', 
        '__tag____receive_time__': '1720539661666', 
        'content': '[FaaS System] Stopping function...', 
        'function_id': 'emlm****', 
        'function_name': 'TLSProducer2', 
        'log_type': 'stdout', 
        'pod_name': 'emlmsobj-v2nv5z3yv9-69b9bb7487-*****', 
        'revision_number': '1', 
        'timestamp': '2024-07-09T15:41:00.086897178Z'
     }, 
     
     'extensions': {
         'consumergroup': 'tls-trigger-consume-2_4o3fw1qf', 
         'key': '', 
         'maxretrynum': '3', 
         'offset': '43', 
         'partition': '0', 
         'retriesforbadstatusrequests': '0', 
         'topic': 'out-ba109ccd-7edc-4a6d-9095-8cdcb1f0****'
     },
}
```



|Parameter |Type |Description |
|---|---|---|
|id |string |Cloudevent proprietary field: Request id, each request has a unique id. |
|source |string |CloudEvent proprietary field: The value for the TLS trigger is `/faas/event/tls/{trigger_id}`. |
|type |string |Cloudevent proprietary field: event type, the value for TLS trigger is `faas.tls.event`. |
|specversion |string |Cloudevent proprietary field: Cloudevent version. |
|datacontenttype |string |CloudEvent proprietary field: message type, all are `application/octet-stream`. |
|time |string |Message trigger time, formatted as an ISO 8601 timestamp. |
|data |json |TLS log message content. The proprietary fields of TLS are **path**, **source**, **tag____client_ip**, and **tag____receive_time**. The others are fields specified by the user output log. |
|extensions |json |Extension information of the event. Sub\-parameter description, please refer to the descriptions of the extensions parameter below. |


The extensions parameter description is as follows:


|Parameter |Type |Description |
|---|---|---|
|topic |string |Message source Topic. |
|partition |string |The partition of the message source. |
|consumergroup |string |Consumer group of the message source. |
|offset |string |Consumption point. |
|key |string |Message Key. |
|retriesforbadstatusrequests |string |Message retry count. n represents the nth retry. |
|maxretrynum |string |Maximum message retry count. |
