---
title: "Obtain AI Status"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1415216"
---

Real\-time AI status can be obtained via callbacks, such as listening, thinking, speaking, being interrupted, or when an error occurs. You can display this status information in real time on the client, or persistently store and analyze it on the server.

<span id=".5o6l5pS25pa55byP"></span>
## Reception Methods

AI status information can be received through either the client or server, with different use cases for each:


* **Client\-side reception (recommended)**  : Lower latency and higher reliability, suitable for scenarios where AI status needs to be displayed in real time on the client (App, Web).

* **Server\-side reception**: Suitable for scenarios requiring persistent storage of status, further analysis, or where the client is not convenient for handling real\-time binary messages.


<span id=".6YCa6L-H5a6i5oi356uv5o6l5pS2"></span>
## Receiving via the Client

<span id=".5a6e546w5pa55byP"></span>
### Implementation Method


1. When calling the `StartVoiceChat` API, set `AgentConfig.EnableConversationStateCallback` to `true`.

2. Listen for the RTC SDK callback [onRoomBinaryMessageReceived](https://docs.byteplus.com/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived-2) on the client side.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Callback names may differ across platforms; see <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-client-api">Client API</a> for details.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the C language interface, the callback name is <code>on_message_received</code>.   </div>
   


When the AI status changes, you will receive a binary `message` via the above callback. You need to parse it to obtain specific status information.

<span id=".6Kej5p6Q5raI5oGv"></span>
### Message Parsing Example

For the `message` format, see [Binary Message Format](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216#binary) for details. You can refer to the following example to parse `message`:


<Tabs>
<Tab zoneid="b7kBUuIE5n" title="TypeScript">
<TabTitle>TypeScript</TabTitle>

```TypeScript
import VERTC from '@volcengine/rtc';

/**
 *@briefConvert TLV data format to string
 *@noteTLV data format
 * | magic number | length(big-endian) | value |
 *@param {ArrayBufferLike}tlvBuffer
 *@returns 
 */
function tlv2String(tlvBuffer: ArrayBufferLike) {
  const typeBuffer = new Uint8Array(tlvBuffer, 0, 4);
  const lengthBuffer = new Uint8Array(tlvBuffer, 4, 4);
  const valueBuffer = new Uint8Array(tlvBuffer, 8);

  let type = '';
  for (let i = 0; i < typeBuffer.length; i++) {
    type += String.fromCharCode(typeBuffer[i]);
  }

  const length =
    (lengthBuffer[0] << 24) | (lengthBuffer[1] << 16) | (lengthBuffer[2] << 8) | lengthBuffer[3];

  const value = new TextDecoder().decode(valueBuffer.subarray(0, length));

  return { type, value };
};

/**
 *@brief Room Message Handler
 */
function handleRoomBinaryMessageReceived(
  event: {
    userId: string;
    message: ArrayBuffer;
  },
) {
  const { message } = event;
  const { type, value } = tlv2String(message);
  const data = JSON.parse(value);
  const { EventTime, RoundID, Stage, TaskId, UserID, ErrorInfo } = data || {};
  const { Code, Description } = Stage || {};
  // Process type and data for business logic
  console.log(type, EventTime, RoundID, TaskId, UserID, Code, Description);
  if (ErrorInfo) {
    const { ErrorCode, Reason } = ErrorInfo;
    console.log('Error Occurred:', ErrorCode, Reason);
  }
  // ...
}

/**
 *@briefListen for binary messages in the room
 */
this.engine.on(VERTC.events.onRoomBinaryMessageReceived, handleRoomBinaryMessageReceived);
```



</Tab>
<Tab zoneid="adgh4tVCES" title="Java">
<TabTitle>Java</TabTitle>

```Java
//Agent status structure
import com.google.gson.annotations.SerializedName;

class ErrorDetail {
    @SerializedName("ErrorCode")
    int errorCode;

    @SerializedName("Reason")
    String reason;
}

class Stage {
    @SerializedName("Code")
    /**
     * 0: errorOccurred
     * 1: listening
     * 2: thinking
     * 3: answering
     * 4: interrupted
     * 5: answerFinish
     */
    int code;

    @SerializedName("Description")
    String description;
}

public class conversationStatusMessage {
    @SerializedName("TaskId")
    String taskId;

    @SerializedName("UserID")
    String userID;

    @SerializedName("RoundID")
    long roundID;

    @SerializedName("EventTime")
    long eventTime;

    @SerializedName("Stage")
    Stage stage;

    @SerializedName("ErrorInfo")
    ErrorDetail errorInfo;

    public String toString() {
        String string = "taskId:" + taskId + ", " +
                "userID:" + userID + ", " +
                "roundID:" + roundID + ", " +
                "eventTime:" + eventTime + ", " +
                "stage:" + stage.code + " - " + stage.description;
        if (errorInfo != null) {
            string += ", errorCode:" + errorInfo.errorCode + ", reason:" + errorInfo.reason;
        }
        System.out.println(string);
        return string;
    }
}

class RoomEventHandler {
    //Parse message
    public void onRoomBinaryMessageReceived(String uid, ByteBuffer buffer) {
    byte[] prefixBytes = new byte[4];
    buffer.get(prefixBytes);

    String prefix = new String(prefixBytes, StandardCharsets.UTF_8);
    if (prefix.equals("conv")) {
        int length = buffer.getInt();
        byte[] jsonBytes = new byte[length];
        buffer.get(jsonBytes);
        String jsonContent = new String(jsonBytes, StandardCharsets.UTF_8);
        conversationStatusMessage statusMessage = new Gson().fromJson(jsonContent, conversationStatusMessage.class);
        System.out.println("Unpack_conv length:" + length + " " + statusMessage.toString());
    } else {
        System.out.println("Invalid message prefix:" + prefix);
    }
}
```



</Tab>
<Tab zoneid="Dl7iUjLPzR" title="C++">
<TabTitle>C++</TabTitle>

```C++
struct ErrorDetail {
int errorCode;
    std::string reason;
};

struct conversationStatusMessage
{
    struct Stage
    {
        int code;
        std::string description;
    };

    std::string taskId;
    std::string userID;
    int64_t roundID;
    int64_t eventTime;
    Stage stage;
    std::optional<ErrorDetail> errorInfo;
};

void onRoomBinaryMessageReceived(const char *uid, int size, const uint8_t *message)
{
    static const int headerSize = 8;
    if (size < headerSize)
    {
        return;
    }

    uint32_t header = messageHeader(message);
    if (header == 0x636F6E76U) // magic number "conv"
    {
        std::string strMessage = unpack(message, size);
        if (!strMessage.empty())
        {
            unpackConversationStage(strMessage);
        }
    }
    else
    {
        LOG_E << "unknown message header: " << header;
        return;
    }
}

void unpackConversationStage(const std::string &message)
{
    // Parse JSON string
    nlohmann::json json_data = nlohmann::json::parse(message);
    // Store parsed data
    conversationStatusMessage statusMessage;
    statusMessage.taskId = json_data["TaskId"];
    statusMessage.userID = json_data["UserID"];
    statusMessage.roundID = json_data["RoundID"];
    statusMessage.eventTime = json_data["EventTime"];

    conversationStatusMessage::Stage stage;
    stage.code = json_data["Stage"]["Code"];
    stage.description = json_data["Stage"]["Description"];
    statusMessage.stage = stage;

    if (json_data.contains("ErrorInfo") && !json_data["ErrorInfo"].is_null()) {
        ErrorDetail errorDetail;
        errorDetail.code = json_data["ErrorInfo"]["ErrorCode"];
        errorDetail.reason = json_data["ErrorInfo"]["Reason"];
        statusMessage.errorInfo = errorDetail;
    }
}
```



</Tab>
<Tab zoneid="McrQVP14vJ" title="Objective-C">
<TabTitle>Objective-C</TabTitle>

```Objective-C
#import <Foundation/Foundation.h>

@interface ErrorDetail : NSObject
@property (nonatomic, assign) int errorCode;
@property (nonatomic, copy) NSString *reason;
@end

@implementation ErrorDetail
@end

@interface Stage : NSObject
@property (nonatomic, assign) int code;
@property (nonatomic, copy) NSString *description;
@end

@implementation Stage
@end

@interface conversationStatusMessage : NSObject

@property (nonatomic, copy) NSString *taskId;
@property (nonatomic, copy) NSString *userID;
@property (nonatomic, assign) int64_t roundID;
@property (nonatomic, assign) int64_t eventTime;
@property (nonatomic, strong) Stage *stage;
@property (nonatomic, strong) ErrorDetail *errorInfo;
@property (nonatomic, assign) BOOL hasErrorInfo;

@end

@implementation conversationStatusMessage
@end

@interface RoomEventHandler : NSObject
@end

@implementation RoomEventHandler
//callbacks
- (void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSString *_Nonnull)uid message:(NSData *_Nonnull)message {
    NSString *strMessage = unpack(message);
    if (strMessage) {
        parseData(strMessage);
    }
}
@end

NSString *unpack(NSData *data) {
    const int headerSize = 8;
    NSUInteger size = data.length;
    if (size < headerSize) {
        return nil;
    }
    const uint8_t *message = data.bytes;
    // Check magic number "conv"
    uint32_t magic = (message[0] << 24) | (message[1] << 16) | (message[2] << 8) | message[3];
    if (magic != 0x636F6E76) {
        return nil;
    }
    
    // Get length
    uint32_t length = (message[4] << 24) | (message[5] << 16) | (message[6] << 8) | message[7];
    if (size - headerSize != length) {
        return nil;
    }
    
    // Get conversationStatusMessage
    NSString *conversationStatusMessage = nil;
    if (length > 0) {
        conversationStatusMessage = [[NSString alloc] initWithBytes:message + headerSize length:length encoding:NSUTF8StringEncoding];
    } else {
        conversationStatusMessage = @"";
    }
    
    return conversationStatusMessage;
}

void parseData(NSString *message) {
    NSError *error = nil;
    NSDictionary *json_data = [NSJSONSerialization JSONObjectWithData:[message dataUsingEncoding:NSUTF8StringEncoding] options:0 error:&error];
    if (error || json_data == nil) {
        NSLog(@"JSON parse error: %@", error);
        return;
    }

    conversationStatusMessage *statusMsg = [[conversationStatusMessage alloc] init];
    statusMsg.taskId = json_data[@"TaskId"];
    statusMsg.userID = json_data[@"UserID"];
    statusMsg.roundID = [json_data[@"RoundID"] longLongValue];
    statusMsg.eventTime = [json_data[@"EventTime"] longLongValue];

    Stage stage;
    stage.code = [json_data[@"Stage"][@"Code"] intValue];
    stage.description = json_data[@"Stage"][@"Description"];
    statusMsg.stage = stage;

    if (json_data[@"ErrorInfo"] && json_data[@"ErrorInfo"] != [NSNull null]) {
        ErrorDetail errorDetail;
        errorDetail.code = [json_data[@"ErrorInfo"][@"ErrorCode"] intValue];
        errorDetail.reason = json_data[@"ErrorInfo"][@"Reason"];
        statusMsg.errorInfo = errorDetail;
        statusMsg.hasErrorInfo = YES;
    } else {
        statusMsg.hasErrorInfo = NO;
    }
}
```



</Tab>
<Tab zoneid="tksAURoOef" title="C">
<TabTitle>C</TabTitle>

```C
#define CONVERSATION_MAGIC_HEADER_SIZE 8
#define CONVERSATION_MAGIC_STATUS_STR "conv"

static bool _is_target_message(const uint8_t* message, const char* target) {
    if (message == NULL || target == NULL) {
        return false;
    }
    // Check if the first 4 bytes match the magic number for "conv"
    if (*(const uint32_t*)message != *(const uint32_t*)target) {
        return false;
    }
    return true;
}

static void on_conversation_status_message_received(byte_rtc_engine_t engine, const cJSON* root) {
    cJSON* stage_obj = cJSON_GetObjectItem(root, "Stage");
    if (stage_obj != NULL) {
        cJSON* code_obj = cJSON_GetObjectItem(stage_obj, "Code");
        if (code_obj != NULL) {
            printf("conversation status message, code: %d\\n", (int)cJSON_GetNumberValue(code_obj));
        }
        cJSON* description_obj = cJSON_GetObjectItem(stage_obj, "Description");
        if (description_obj != NULL) {
            printf("conversation status message, description: %s\\n", cJSON_GetStringValue(description_obj));
        }
    }
    cJSON* task_id_obj = cJSON_GetObjectItem(root, "TaskId");
    if (task_id_obj != NULL) {
        printf("conversation status message, task_id: %s\\n", cJSON_GetStringValue(task_id_obj));
    }
    cJSON* user_id_obj = cJSON_GetObjectItem(root, "UserID");
    if (user_id_obj != NULL) {
        printf("conversation status message, user_id: %s\\n", cJSON_GetStringValue(user_id_obj));
    }
    cJSON* round_id_obj = cJSON_GetObjectItem(root, "RoundID");
    if (round_id_obj != NULL) {
        printf("conversation status message, round_id: %d\\n", (int)cJSON_GetNumberValue(round_id_obj));
    }
    cJSON* event_time_obj = cJSON_GetObjectItem(root, "EventTime");
    if (event_time_obj != NULL) {
        printf("conversation status message, event_time: %lld\\n", (long long)cJSON_GetNumberValue(event_time_obj));
    }
    cJSON* error_info_obj = cJSON_GetObjectItem(root, "ErrorInfo");
    if (error_info_obj != NULL && cJSON_IsObject(error_info_obj)) {
        cJSON* error_code_obj = cJSON_GetObjectItem(error_info_obj, "ErrorCode");
        if (error_code_obj != NULL) {
            printf("error info, code: %d\\n", (int)cJSON_GetNumberValue(error_code_obj));
        }
        cJSON* reason_obj = cJSON_GetObjectItem(error_info_obj, "Reason");
        if (reason_obj != NULL) {
            printf("error info, reason: %s\\n", cJSON_GetStringValue(reason_obj));
        }
    }
}

// Callback function
static void on_message_received(byte_rtc_engine_t engine, const char* room, const char* src, const uint8_t* message, int size, bool binary) {
    cJSON* root = NULL;
    if (size < CONVERSATION_MAGIC_HEADER_SIZE) {
        return;
    }
    if (!_is_target_message(message, CONVERSATION_MAGIC_STATUS_STR)) {
        // Non-agent status message
        return;
    }
    
    root = cJSON_Parse((const char*)(message + CONVERSATION_MAGIC_HEADER_SIZE));
    if (NULL == root) {
        return;
    }

    on_conversation_status_message_received(engine, root);

    cJSON_Delete(root);
}
```



</Tab>
</Tabs>


<span id=".6YCa6L-H5pyN5Yqh56uv5o6l5pS2"></span>
## Receiving via the server

<span id="3850cd71"></span>
### Implementation Method


1. When calling the `StartVoiceChat` API, configure the callback server using the following parameters:

   ```json
   "AgentConfig": {
       "EnableConversationStateCallback": true,  // Must be set to true
       
       // 1. Your callback service address. The system will POST status messages here. The following requirements must be met:
       // - Must be a domain name address accessible from the public internet. If using HTTPS, ensure that the SSL certificate is valid and complete.
       // - If AI status callbacks (ServerMessageURLForRTS) are also configured, both must use the same URL address.
       // - Ensure that the server pointed to by this URL can properly handle POST requests without a Content-Type.
       "ServerMessageURLForRTS": "https://your-server.com/example_domain/vertc/cstage",
       
       // 2. Authentication key. Customizable by you; the platform simply returns it as-is in the callback for validation on your server.
       "ServerMessageSignatureForRTS": "your_custom_secure_signature" 
   }
   ```
   

2. Receive, verify, and parse callback messages.

   When the AI status changes, the URL you configured will receive an HTTP POST request with the following request body format:

   ```JSON
   {
     "message": "Y29udgAAAKV7Cg...=",
     "binary": true,
     "signature": "your_custom_secure_signature"
   }
   ```
   

   * `message`: Binary message content encoded in Base64. For the specific format, see [Binary Message Format](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216#binary).

   * `signature`: The signature string returned by the platform, which is configured in `StartVoiceChat` using `AgentConfig.ServerMessageSignatureForRTS`.

      After receiving the callback message, you also need to complete the following operations:

   * **Receive message**: Obtain the `message` and `signature` fields and their values.

   * \*\*Verify \*\* `signature`: Compare the value of `signature` with `AgentConfig.ServerMessageSignatureForRTS`.

   * \*\*Parse \*\* `message`: Only proceed to decode and parse the content of `message` after the signature verification passes.


The following is a complete Go service example that implements the above process.

> You can quickly verify this example locally. For detailed instructions, see [Local Verification](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216#4291405f).


```Golang
package main

import (
   "encoding/base64"
   "encoding/binary"
   "encoding/json"
   "fmt"
   "github.com/gin-gonic/gin"
)
// --- 1. Configuration you need to modify ---
const (
   conversationStageHeader = "conv"
   exampleSignature        = "your_custom_secure_signature"   // Replace with the actual key you configured in StartVoiceChat
)

type RtsMessage struct {
   Message   string `json:"message"`
   Signature string `json:"signature"`
}

type Conv struct {
   TaskID    string    `json:"TaskId"`
   UserID    string    `json:"UserID"`
   RoundID   int64     `json:"RoundID"`   
   EventTime int64     `json:"EventTime"`
   Stage     StageInfo `json:"Stage"`
}

type StageInfo struct {
   Code        stageCode `json:"Code"`
   Description string    `json:"Description"`
}
type stageCode int

const (
   _ stageCode = iota
   listening
   thinking
   answering
   interrupted
   answerFinish
)

var (
   stageListening    = StageInfo{Code: listening, Description: "listening"}
   stageThinking     = StageInfo{Code: thinking, Description: "thinking"}
   stageAnswering    = StageInfo{Code: answering, Description: "answering"}
   stageInterrupted  = StageInfo{Code: interrupted, Description: "interrupted"}
   stageAnswerFinish = StageInfo{Code: answerFinish, Description: "answerFinish"}
)

func HandleConversationStageMsg(c *gin.Context) {
   msg := &RtsMessage{}
   if err := c.BindJSON(&msg); err != nil {
      fmt.Printf("BindJson failed,err:%v\n", err)
      return
   }
   if msg.Signature != exampleSignature {
      fmt.Printf("Signature not match\n")
      return
   }

   conv, err := Unpack(msg.Message)
   if err != nil {
      fmt.Printf("Unpack failed,err:%v\n", err)
      return
   }

   fmt.Println(conv)

   // Business logic

   c.String(200, "ok")
}

func Unpack(msg string) (*Conv, error) {
   data, err := base64.StdEncoding.DecodeString(msg)
   if err != nil {
      return nil, fmt.Errorf("DecodeString failed,err:%v", err)
   }
   if len(data) < 8 {
      return nil, fmt.Errorf("Data invalid")
   }
   dataHeader := string(data[:4])
   if dataHeader != conversationStageHeader {
      return nil, fmt.Errorf("Header not match")
   }
   dataSize := binary.BigEndian.Uint32(data[4:8])
   if dataSize+8 != uint32(len(data)) {
      return nil, fmt.Errorf("Size not match")
   }

   subData := data[8:]
   conv := &Conv{}
   err = json.Unmarshal(subData, conv)
   if err != nil {
      return nil, fmt.Errorf("Unmarshal failed,err:%v\n", err)
   }
   return conv, nil
}

func main() {

   r := gin.Default()
   // --- 2. Configuration you need to modify ---
   // Callback path: The path here ("/example_domain/vertc/cstage") must exactly match the path part of ServerMessageURLForRTS configured in StartVoiceChat.
   // For example, if your callback URL is "https://my-service.com/api/rtc/status",
   // then the path here must be "/api/rtc/status".
   r.POST("/example_domain/vertc/cstage", HandleConversationStageMsg)
   r.Run()
}
```


Expected parsing result example:

```Bash
&{ChatTask01 Huoshan01 16 1765787330849 {1 listening}}
```


<span id="4291405f"></span>
### **Local Verification**

Ensure that you have the Go runtime environment installed locally before proceeding.


1. Create a `main.go` file, copy the above sample code, and modify the value of `exampleSignature` and the path in `r.POST` according to the comments.

2. Install the Gin framework:

   ```Shell
   go get github.com/gin-gonic/gin
   ```
   

3. Start the service:

   ```Shell
   go run main.go
   ```
   

   You will see a prompt indicating that the service has started on port `8080`.

4. Open a new terminal and use `curl` to simulate a real callback request.

   Caution: The value of `signature` must be exactly the same as the value of `exampleSignature` in the `main.go` code.

   ```Bash
   curl -X POST 'http://127.0.0.1:8080/example_domain/vertc/cstage' \
     -H 'Content-Type: application/json' \
     -d '{
       "message":"Y29udgAAAKV7CgkiRXZlbnRUaW1lIiA6IDE3NjU3Njk1MDI4NDcsCgkiUm91bmRJRCIgOiAzLAoJIlN0YWdlIiA6IAoJewoJCSJDb2RlIiA6IDUsCgkJIkRlc2NyaXB0aW9uIiA6ICJhbnN3ZXJGaW5pc2giCgl9LAoJIlRhc2tJZCIgOiAiQ2hhdFRhc2swMSIsCgkiVXNlcklEIiA6ICJIdW9zaGFuMDEiCn0=",
       "signature":"your_custom_secure_signature"
     }'
   ```
   

   Expected result:

   * The curl command outputs "ok".

   * In the terminal running the Go service, you will see logs indicating successful parsing:

   ```Bash
   &{ChatTask01 Huoshan01 3 1765769502847 {5 answerFinish}}
   ```
   


<span id=".6ZmE5b2V"></span>
## Appendix

<span id="binary"></span>
### Binary Message Format

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f899ca238acab3626fc34d41aa1d896a.jpg) </span>

&nbsp;


|Parameter |Type |Description |
|---|---|---|
|magic number |binary |Message format, fixed as `conv`. |
|length |binary |Message length, in bytes. Stored in big\-endian format. |
|conversation_status_message |binary |Message details. See [conversation_status_message](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216#66e7a2f8) for details. |


<span id="66e7a2f8"></span>
##### conversation_status_message

&nbsp;


|Parameter |Type |Description |
|---|---|---|
|TaskId |String |AI conversation task ID. |
|UserID |String |Speaker UserId. |
|RoundID |Int64 |Conversation round. Counting starts from `0`. |
|EventTime |Int64 |The Unix timestamp (ms) when the event occurred on the RTC server. |
|Stage |[Stage](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216#26d9ed1f) |Detailed description of task status. |
|ErrorInfo |[ErrorInfo](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216#d15a53f4) |Detailed information about task errors. This field is returned only when `Stage.Code` is `0`. |


<span id="26d9ed1f"></span>
##### Stage

&nbsp;


|Parameter |Type |Description |
|---|---|---|
|Code |Int |Status code.<br><br><br>* 0: Task encountered an error.<br><br>* 1: AI is listening.<br><br>* 2: AI is thinking.<br><br>* 3: AI is speaking.<br><br>* 4: AI was interrupted.<br><br>* 5: AI finished speaking. |
|Description |String |Task status description. |


<span id="d15a53f4"></span>
##### ErrorInfo

&nbsp;


|Parameter |Type |Description |
|---|---|---|
|Code |Int |Error status code. See details in [Error Codes](https://docs.byteplus.com/docs/byteplus-rtc/docs-1928198#80233b4b). |
|Reason |String |Detailed error reason. |
