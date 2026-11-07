---
title: "GetSnapshotTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-7oypi02iom"
---

After you start a snapshot task, you can call `GetSnapshotTask` to specify the `AppId`, `RoomId` and `TaskId` to get the relevant information of the specified snapshot task.

> The interface can query the task started within 72 hours.


<span id="HTTP"></span>
## HTTP request


* Method：GET

* Endpoint：https://open.byteplusapi.com?Action=GetSnapshotTask&Version=2022\-06\-01


<span id="Request"></span>
## Request parameters

<span id="Common"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="Query"></span>
### Query

&nbsp;


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetSnapshotTask` |Interface name. The value of this interface: `GetSnapshotTask` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |Room Id. It's the identifier of a room. |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |


<span id="Response"></span>
## Response parameters

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|SnapshotTask |Object of [SnapshotTask](https://docs.byteplus.com/en/docs/12/14259#snapshottask) |`-` |Information about the snapshot task |


<span id="snapshottask"></span>
### SnapshotTask

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|StartTime |Long |`1677227309000` |Unix timestamp when the task starts, in ms. |
|EndTime |Long |`1677227511000` |Unix timestamp when the task stops, in ms.`0` means that the task is running. |
|Status |Long |`3` |Status of the task.<br><br><br>* `0`: Unknown exception<br><br>* `1`: Not started<br><br>* `2`: Running<br><br>* `3`: Ended<br><br>* `4`: Task failed |
|StopReason |String |`IdleTimeOut` |Reason why task stops:<br><br><br>* Empty: the task is not finished<br><br>* `UnknownStopReason`: There is a unknown reason for stopping<br><br>* `StopByAPI`: The user stops the task by calling the API<br><br>* `StartTaskFailed`: The task failed to start<br><br>* `IdleTimeOut`: the idle time has exceeded the set value. |
|TargetStreams |Object of [Streams](https://docs.byteplus.com/en/docs/12/14259#streams) |`-` |The audio & video stream that needs to be snapshoted in the room. |
|MaxIdleTime |Integer |`200` |The max idle time for the task. |
|ImageConfig |Object of [ImageConfig](https://docs.byteplus.com/en/docs/12/14259#imageconfig) | |Configuration of image: format, size and the interval of snapshot. |
|StorageConfig |Object of [StorageConfig](https://docs.byteplus.com/en/docs/12/14259#storageconfig) |`-` |Configuration about storage. AK and SK won't be returned. |


<span id="streams"></span>
### Streams

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14259#stream) |`-` |A list of `Streams`. It can be empty. When empty, it means subscribing to all streams in the room. In a `StreamList`, `Stream. Index`cannot be duplicated. |


<span id="stream"></span>
### Stream

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Index |Integer |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |`Your_UserId` |UserId which represents the user a stream belongs to. |
|StreamType |Integer |`0` |The type of stream. The value can be `0` or `1`, and the default value is `0`. `0`means normal audio & video stream, `1` means screen stream. You don't need to specify `StreamType` for WTN. |


<span id="imageconfig"></span>
### ImageConfig

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Format |Integer |`0` |The format of the image.<br><br><br>* `0` ( default): `JPEG`<br><br>* `1`: `PNG`.<br><br><br>When the value is invalid, it is automatically adjusted to the default value. |
|Width |Integer |`0` |The actual width of the video frame used in px, and the value range is `[0,1920]`. The default value is `0`, and in this case, it is the same as the actual width of the video stream. If the value is invalid, it will be automatically adjusted to the default value. |
|Height |Integer |`0` |The actual height of the video frame in px, and the value range is `[0,1080]` . The default value is `0`. And in this case, it is the same as the actual height of the video stream. If the value is illegal, it will be automatically adjusted to the default value. |
|Interval |Float |`2.0` |The interval between consecutive screenshots, in seconds. Floating\-point values are supported with millisecond precision (0.001s).<br><br><br>* **Valid range**: `[0.1, 600]`<br><br>* **Default**: `2.0`<br><br>* Values with more than 3 decimal places will be truncated. |


<span id="storageconfig"></span>
### StorageConfig

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |Integer |`0` |Storage platform<br><br>`0`: BytePlus TOS<br><br>`2`: Third\-party storage platform supporting S3 protocol |
|TosConfig |Object of [TosConfig](https://docs.byteplus.com/en/docs/12/14259#tosconfig) |`-` |When Type = `0`, the value of TosConfig needs to be set correctly, otherwise the request will report an error. |
|VodConfig |Object of [VodConfig](https://docs.byteplus.com/en/docs/12/14259#vodconfig) |`-` |When Type = `1`, the value of VodConfig needs to be set correctly, otherwise the request will report an error |
|CustomConfig |Object of [CustomConfig](https://docs.byteplus.com/en/docs/12/14259#customconfig) |`-` |When Type = `2`, you need to set the value of CustomConfig correctly, otherwise the request will report an error |


<span id="tosconfig"></span>
### TosConfig

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |String |`300000000` |BytePlus AccountId.You can find it by clicking the account icon in the top\-right corner.<br><br>Even if you use the AK and SK of a sub\-user during the OpenAPI authentication process, the AccountId must be of the main account ID. |
|Bucket |String |`Your_Bucket` |Name of bucket you created on TOS platform. |
|Region |Integer |`0` |Supported regions:<br><br><br>* `0` (default): ap\-southeast\-1<br><br>* `1`: cn\-hongkong<br><br>* `2`: ap\-southeast\-3 |


<span id="vodconfig"></span>
### VodConfig

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |String |`Your_AccountId` |Console account ID, such as `200000000`.<br><br><br>* To find the AccountID: Console \-\> My Account \-\> Account ID<br><br>   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/OpenAPI/image.png) </span><br><br>* This `AccountID` must be the main account's `AccountID`.<br><br>* Even if AK and SK used to authenticate is from sub\-account, the `AccountID`must be the main account's `AccountID`. |
|Region |Integer |`-` |Only support `0` (ap\-southeast\-1). |
|Space |String |`Your_Space` |Vod space name. |


<span id="customconfig"></span>
### CustomConfig

&nbsp;


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Vendor |Integer |`0` |Third\-party cloud storage platform.<br><br><br>* 0: Amazon S3. By default.<br><br>* 1: Aliyun object Storage Service OSS<br><br>* 2: HUAWEI CLOUD OBS<br><br>* 3: Tencent Cloud COS<br><br>* 4: Qiniu Cloud Kodo.<br><br>* 5: Google Cloud Storage |
|Region |Integer |`0` |Different storage platforms support different regions, see [Region list](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115995#region-list)<br><br>The default value is `0`. |
|Bucket |String |`Your_Bucket` |The name of the bucket. |
|AccessKey |String |`Your_AccessKey` |The AccessKey of the third\-party storage platform account. Make sure this account has writing permission to the bucket.<br><br>It's not recommended to enable reading permission. |
|SecretKey |String |`Your_SecretKey` |The SecretKey of the third\-party storage platform account |


<span id="sample-request"></span>
### Sample request

```json
https://open.byteplusapi.com?Action=GetSnapshotTask&Version=2022-06-01&AppId=You****pId&RoomId=Your_RoomId&TaskId=Your_TaskId
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "SnapshotTask": {
            "StartTime": 1677227309000,
            "EndTime": 1677227511000,
            "Status": 3,
            "StopReason": "IdleTimeOut",
            "TargetStreams": {
                "StreamList": [
                    {
                        "Index": 0,
                        "UserId": "user0",
                        "StreamType": 1
                    },
                    {
                        "Index": 1,
                        "UserId": "user1",
                        "StreamType": 1
                    }
                ]
            },
            "MaxIdleTime": 200,
            "ImageConfig": {
                "Format": 0,
                "Width": 800,
                "Height": 800,
                "Interval": 2
            },
            "StorageConfig": {
                "Type": 1,
                "VodConfig": {
                    "AccountId": 20****000,
                    "Region": 0,
                    "Space": "Your_Space"
                }
            }
        }
    },
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "GetSnapshotTask",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "cn-north-1"
    }
}
```
