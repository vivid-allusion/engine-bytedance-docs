---
title: "Function Calling"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1554654"
---

Function Calling enables AI to recognize specific user intents in spoken language and invoke external functions you have implemented to accomplish particular tasks. For example: retrieving real\-time information (such as weather), operating business systems (such as checking order status), or controlling app features (playing music, turning off lights, adjusting volume), and more.

<span id=".5qih5Z6L6ZmQ5Yi2"></span>
# Limitations

It is only compatible with BytePlus ModelArk models or third\-party LLMs that support Function Calling. For a comprehensive list of supported ModelArk models, refer to the [Model List-Tool use](https://docs.byteplus.com/en/docs/ModelArk/1330310#f44ceef7).

<span id=".5a6e546w5rWB56iL"></span>
# Workflow

The workflow of Function Calling involves the following core roles:


* **LLM**: Responsible for understanding user intent and deciding which function to invoke.

* **System service**: As the technical foundation, responsible for receiving your requests, invoking the LLM, and passing the LLM's decisions (such as function calling instructions) to your application via callbacks.

* **Your application**: Responsible for implementing and executing specific local functions (such as retrieving weather information).


The core of the entire process is "**LLM decision, your code execution**". The specific implementation process is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a026144817d64727a279dc07b38f3635) </span>


1. Prepare and declare functions:

   Define specific local functions in the client application. When calling the `StartVoiceChat` interface, declare to the model the functions you have defined.

2. Decision and execution:

   1. The user submits a request to the AI that requires external capabilities to complete (for example: "Help me check the weather in Shanghai").

   2. The large model identifies the user's intent, decides which function needs to be called, and generates the corresponding calling instruction.

   3. The system issues instructions via callbacks:

      1. First, it sends a "function calling notification": informing you in advance that a function is about to be called. After receiving the "calling notification", you can immediately request to play a soothing message (such as "Querying, please wait") to optimize the user's waiting experience.

      2. Second, it sends the "function call instruction": specifying the function to be executed and the input parameters (such as `location: "Shanghai"`).

   4. Your application executes the local function according to the "call instruction", obtains the execution result, and returns it to the system.

3. AI response:

   After the system receives the reported function execution result, how it is delivered to the user depends on the return method you select:

   * Method 1 (direct playback):

      The function execution result is directly converted to speech and played via TTS. This is suitable for scenarios where the result does not require refinement, or the reply content is relatively long.

   * Method 2 (playback after LLM processing):

      The function execution result is returned to the LLM, summarized and refined by the model, and then played via TTS. This is suitable for scenarios where the reply needs to be processed further.


<span id="942e1d9a"></span>
# Before You Begin


1. **Prepare the function**.

   You need to implement the logic of the specific function to be called by AI in your business application. The purpose of Function Calling is to enable the model to "decide" which function to call and what parameters to pass, while the execution of the function is entirely handled by your program.

   For example, to implement weather queries, you need to implement a function that can query and return weather information.

2. **Determine the implementation method.** 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During integration, you need to handle the call instructions sent by the system and return your external function's execution results.   </div>
   

   
   |Comparison items |Server\-side implementation |Client\-side implementation |
   |---|---|---|
   |**Use cases** |* Functions are deployed on an independent server.<br><br>* Use cases requiring unified management and verification of function calls. |* Functions are local to the client, such as controlling app features or accessing device hardware.<br><br>* To avoid setting up additional backend services. |
   |**Development requirements** |Provide a publicly accessible URL address for receiving callback data. |Listen for callbacks from the RTC SDK in client code, and parse and construct specific binary data packets according to the documentation. |
   |**Communication method** |The system issues instructions to the URL you provide via a public HTTP POST request. |The system sends instructions to your client app via the RTC data channel. |
   


<span id=".5pyN5Yqh56uv5a6e546w"></span>
# Server\-Side Implementation

<span id=".XzEt5byA5ZCvLWZ1bmN0aW9uLWNhbGxpbmct5Yqf6IO9"></span>
## Step 1: Declare Functions and Configure Callbacks

When calling the `StartVoiceChat` interface, you need to provide the following configuration:


* `LLMConfig.Tools`: Declare all functions that you need the model to call. Please ensure that for each function declared here, you have implemented the corresponding logic in your business code. Among them, `parameters` must strictly comply with the JSON Schema specification.

* `FunctionCallingConfig`:

   * `ServerMessageUrl`: Your backend service address, used to receive function call instructions. It must be a publicly accessible URL and be able to correctly handle HTTP POST requests without `Content-Type`.

   * `ServerMessageSignature`: Custom authentication key. This string will be returned as\-is in the callback request, allowing you to verify the legitimacy of the source on your server.

> The following example demonstrates how to declare a weather query function named `get_current_weather` and configure the callback receiving address.


```JSON
// Declare all functions you need to call (ensure all functions are implemented in your business code)
{
    "LLMConfig": {
        "Tools": [
            {
              "type": "function",
              "function": {
                "name": "get_current_weather",
                "description": "Retrieve weather information for a specified location",
                "parameters": {
                  "type": "object",
                  "properties": {
                    "location": {
                      "type": "string",
                      "description": "Geographical location, e.g., London"
                    }
                  },
                  "required": ["location"]
                }
              }
            }
        ]
    },
    "FunctionCallingConfig": {
        "ServerMessageUrl": "https://your-backend.com/api/fc_callback",  
        "ServerMessageSignature": "your_custom_signature"
     }
}
```


<span id="c49f62e6"></span>
## Step 2: Process Callback Messages

When the AI detects an intent to invoke a tool, the server URL you configured will receive two messages related to FC in succession. You need to distinguish and obtain these two messages by checking the `Type` field in the message body.


1. Obtain and parse the function call notification.

   When the AI detects an intent to invoke a tool, you will first receive a function call notification message (`Type` is `information`). An example notification message is as follows:

   ```JSON
   {
       "Message": "{\"event_type\":\"function_calling\",\"function\":\"get_current_weather\",\"tool_call_id\":\"call_yx8****\",\"response_id\":\"021765**********e711d\"}",
       "Signature": "test_fc_***",              // Which is the ServerMessageSignature you configured in Step 1
       "Type": "information",                   // Fixed value, indicates this is a function call notification
       "RoomID": "ChatRoom01",                  // Conversation room ID
       "TaskID": "73bc1a7e-73ef-470f-91****",
       "TaskType": "voiceChat",      // Fixed value, indicates AI conversation task
       "AppId": "661e****543cf"      // AppId of the application
   }
   ```
   

   The `Message` field is an escaped JSON string and must be parsed before use. The specific content is as follows:

&nbsp;

   
   |Field name |Type |Description |
   |---|---|---|
   |event_type |String |Fixed as `function_calling`, indicating that a Function Calling function call has been triggered. |
   |function |String |Name of the triggered function. |
   |tool_call_id |String |Function Calling task ID for this instance. |
   |response_id |String |Response ID returned for this Function Calling task. If an error occurs in this task, it can be used for troubleshooting. |
   

2. Play comfort phrases.

   Call the `UpdateVoiceChat` interface to play comfort phrases and enhance the user experience.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the comfort phrases have not finished playing when the function result is returned, the system will wait for the comfort phrases to finish before announcing the result.   </div>
   

   ```JSON
   {
       "AppId": "661e****543cf",
       "RoomId": "ChatRoom01",
       "TaskId": "task1",
       "Command": "ExternalTextToSpeech",   // Fixed as ExternalTextToSpeech
       "Message": "Querying, please wait patiently.", // The content must end with punctuation
       "InterruptMode": 3  // Fixed as 3. The playback priority of soothing phrases is low and will be interrupted by subsequent function results.
   }
   ```
   

3. Obtain and parse the function call instruction.

   Immediately after, you will receive a function call instruction message (`Type` is `tool_calls`). You need to first parse the outer `Message` field, then parse the inner `arguments` field to obtain the final function name and execution parameters.

   An example message is as follows:

   ```JSON
   {
       "Message": "[{\"id\":\"call_yx8****\",\"type\":\"function\",\"function\":{\"name\":\"get_current_weather\",\"arguments\":\"{\\\"location\\\":\\\"London\\\",\\\"unit\\\":\\\"
   Celsius\\\"}\"}}]",
       "Signature": "cn_test_***",          // That is, the ServerMessageSignature you configured in Step 1.
       "Type": "tool_calls",               // Fixed value, indicates that this message is a function command message.
       "RoomID": "ChatRoom01",            // Call room ID
       "TaskID": "73bc1a7e-73ef-470f-91****",  // Internal task ID of the system, for internal troubleshooting
       "TaskType": "voiceChat",      // Fixed value, indicates an AI conversation task
       "AppId": "661e****543cf"      // Application AppId
   }
   ```
   

   The `Message` field is an escaped JSON string containing the following content:

&nbsp;

   
   |Field name |Type |Description |
   |---|---|---|
   |id |String |The Function Calling task ID for this session, which matches the value of `message.tool_call_id` in the returned function call notification. |
   |type |String |The tool type called by Function Calling, fixed as `function`, indicating a function call. |
   |function |Object |Function call details. Format example:<br><br>> `arguments` is a JSON string. You need to parse it again to obtain the parameter object.<br><br><br>```JSON```<br>```{```<br>```    "name": "get_current_weather",  // Function name```<br>```    "arguments": {"location":"Shanghai","unit":"Celsius"} // Function input parameters```<br>```}```<br> |
   


<span id=".XzUt5omn6KGM5bel5YW35bm25pKt5pS-57uT5p6c"></span>
## Step 3: Execute External Functions

After obtaining the call instruction information, you need to implement the following in your own application:


1. **Route to function**: Based on the value of `function.name` (for example, `"get_current_weather"`), call the corresponding function you have implemented in your code.

2. **Pass parameters**: Pass the parameters parsed from `function.arguments` in the previous step as input arguments to your function.

3. **Obtain the return value**: Execute your function and obtain its return result. This result will be returned in the next step.


<span id="d4049f67"></span>
## Step 4: Return the Function Result

Call the `UpdateVoiceChat` interface to return the function execution result to the system, which will then be played by the AI.


<Tabs>
<Tab zoneid="QRYvTa2ds9" title="Method 1: Send to LLM for processing before playback">
<TabTitle>Method 1: Send to LLM for processing before playback</TabTitle>

Send the raw data returned by the function back to the LLM for processing before playback. Applicable to scenarios requiring summarization, polishing, and other secondary processing.

> The value of `ToolCallID` must be exactly the same as the value of the [Step 3: Execute External Functions](https://docs.byteplus.com/docs/byteplus-rtc/docs-1554654#.XzUt5omn6KGM5bel5YW35bm25pKt5pS-57uT5p6c) in the `tool_calls` command you received.


```JSON
{
  "AppId": "YOUR_AppId", // Same as StartVoiceChat
  "RoomId": "YOUR_RoomId", // Same as StartVoiceChat
  "TaskId": "YOUR_TaskId", // Same as StartVoiceChat
  "Command": "function", // Must be function
  "Message": "{\\\\"ToolCallID\\\\":\\\\"call_yx8****\\\\",\\\\"Content\\\\":\\\\"The weather in Shanghai is sunny, 25 degrees Celsius.\\\\"}" // Pass the function result as a JSON escaped string
}
```


The LLM may generate a reply: "The weather in Shanghai is nice today, it is sunny, and the temperature is 25 degrees Celsius."


</Tab>
<Tab zoneid="cJVvTYQmsU" title="Method 2: Direct playback (without LLM processing)">
<TabTitle>Method 2: Direct playback (without LLM processing)</TabTitle>

Play the function's raw result directly via TTS. Applicable to scenarios where the returned result does not require processing or the reply sentence is long and latency needs to be reduced.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">To reduce latency, split long replies into several short sentences and call the <code>UpdateVoiceChat</code> interface multiple times.</div>



* <div data-tips="true" data-tips-type="warning">Split the first sentence by comma (，) or semicolon (；); split subsequent sentences by period (。), question mark (？), or other complete sentence punctuation. Avoid splitting decimal points in numbers.</div>


* <div data-tips="true" data-tips-type="warning">Sentence splitting example: <code>The weather is sunny today,</code> <code>The temperature is 10-29 degrees Celsius, with a northerly wind of force three.</code> . <code>In the next seven days, the weather will remain sunny.</code></div>



```JSON
{
  "AppId": "YOUR_AppId", // Same as StartVoiceChat
  "RoomId": "YOUR_RoomId", // Same as StartVoiceChat
  "TaskId": "YOUR_TaskId", // Same as StartVoiceChat
  "Command": "ExternalTextToSpeech", // Must be ExternalTextToSpeech
  "Message": "The weather in Shanghai is sunny.", // Pass the result of the tool call as a regular string
  "InterruptMode": 2 // Fixed value is 2
}
```



</Tab>
</Tabs>


<span id=".5a6i5oi356uv5a6e546w"></span>
# Implement via Client

Process Function Calling notifications and instructions on the client (such as App or web page), execute the function locally, and then send the result back to the system.

<span id="ec09075b"></span>
## Step 1: Declare the function

Call the `StartVoiceChat` interface and configure the `LLMConfig.Tools` field to declare the function you want to call (ensure all functions are implemented in the business code). The `parameters` must strictly comply with the JSON Schema specification.

> The following example demonstrates how to declare a weather query function named `get_current_weather`.


```JSON
{
  "LLMConfig": {
    "Tools": [{
      "type": "function",
      "function": {
        "name": "get_current_weather",
        "description": "Retrieve weather information for a specified location",
        "parameters": {
          "type": "object",
          "properties": {
            "location": {
              "type": "string",
              "description": "Geographical location, e.g., London"
            }
           },
          "required": ["location"]
        }
      }
    }]
  }
}
```


<span id="0811fe0c"></span>
## Step 2: Listen for callbacks and process


1. Listen on the client for [onRoomBinaryMessageReceived](https://docs.byteplus.com/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived-2) callbacks.

   When the AI detects an intent to call a tool, this callback will be triggered twice in succession, and you will receive two binary messages related to Function Calling. You need to parse the `magic number` in the message header to identify and process these two messages.

2. Obtain the function calling notification.

   When the AI detects an intent to call a tool, you will first receive a function calling notification message `message` (with a magic number of info). This message is in binary format, and you need to parse this field after receiving the message. The format and parsing example of `message` are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6d518e9d23d046168f5c58e3aac02586) </span>

&nbsp;

   
   |Field name |Type |Description |
   |---|---|---|
   |magic number |String |Message format, fixed as `info`, indicating that this message is a notification that the function has been triggered. |
   |length |String |Notification message length, in bytes. Stored in big\-endian format. |
   |info_message |String |Detailed information about the function call notification. Content as follows:<br><br>```JSON```<br>```{```<br>```    "event_type": "function_calling",   // Event type, fixed as this value```<br>```    "function": "get_current_weather",  // Name of the triggered function, consistent with the name you defined in StartVoiceChat```<br>```    "tool_call_id": "call_yx8****",       // Unique ID for this function call, required for subsequent result callbacks```<br>```    "response_id": "resp_abcde"         // Unique ID for this response, can be used for troubleshooting```<br>```}```<br> |
   

   `message` parsing example:

   
   <Tabs>
   <Tab zoneid="GoOgN4RLKy" title="C++">
   <TabTitle>C++</TabTitle>
   
   ```C++
   // Structure corresponding to the message body JSON
   struct FCInfoMessage {
       std::string event_type;
       std::string function;
       std::string tool_call_id;
       std::string response_id;
   };
   
   
   // Unpacking function, dedicated to "info" messages: only performs protocol validation and extracts the JSON string
   bool UnpackInfoMessage(const uint8_t *message, int size, std::string& json_payload) {
       const int kHeaderSize = 8;
       if (size < kHeaderSize) {
           return false;
       }
   
   
       // Validate magic number "info" (0x696E666F)
       uint32_t magic = ntohl(*reinterpret_cast<const uint32_t*>(message));
       if (magic != 0x696E666F) {
           return false;
       }
   
   
       // Read length (big-endian)
       uint32_t length = ntohl(*reinterpret_cast<const uint32_t*>(message + 4));
       if (size - kHeaderSize != static_cast<int>(length)) {
           return false;
       }
   
   
       if (length > 0) {
           json_payload.assign(reinterpret_cast<const char*>(message) + kHeaderSize, length);
       } else {
           json_payload.clear();
       }
       return true;
   }
   
   
   // External parsing interface: parses the FCInfoMessage structure
   bool ParseInfoMessage(const uint8_t* message, int size, FCInfoMessage& out_info) {
       std::string json_str;
       if (!UnpackInfoMessage(message, size, json_str)) {
           return false;
       }
   
   
       // Parse JSON with some fault tolerance; if parsing fails, directly return false
       nlohmann::json json_data = nlohmann::json::parse(json_str, /*callback=*/nullptr, /*allow_exceptions=*/false);
       if (json_data.is_discarded()) {
           return false;
       }
   
   
       out_info.event_type   = json_data.value("event_type", "");
       out_info.function     = json_data.value("function", "");
       out_info.tool_call_id = json_data.value("tool_call_id", "");
       out_info.response_id  = json_data.value("response_id", "");
   
   
       return true;
   }
   
   
   // In the onRoomBinaryMessageReceived callback
   void onRoomBinaryMessageReceived(const char* uid, int size, const uint8_t* message) {
       FCInfoMessage info_msg;
       if (!ParseInfoMessage(message, size, info_msg)) {
           // Not a valid info message, ignore directly; you can continue to check whether it is a tool or other message
           return;
       }
   
       // Parsing succeeded! It is now safe to use the fields in info_msg.
       std::cout << "Function Call Notification for: " << info_msg.function << std::endl;
       std::cout << "ToolCallID: " << info_msg.tool_call_id << std::endl;
   
       // You can add your own business logic here
       // For example, after receiving a function call notification, call the `sendUserBinaryMessage` function to let the AI play a soothing message.
       // For specific implementation, refer to the documentation below.
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="eOnZ7s7J1f" title="Java">
   <TabTitle>Java</TabTitle>
   
   ```Java
   // Class corresponding to the message body JSON
   class FCInfoMessage {
       public String event_type;
       public String function;
       public String tool_call_id;
       public String response_id;
   }
   
   // In the onRoomBinaryMessageReceived callback
   @Override
   public void onRoomBinaryMessageReceived(String uid, ByteBuffer message) {
       // Parse using big-endian order
       message.order(ByteOrder.BIG_ENDIAN);
   
       // Must have at least 4 bytes for magic + 4 bytes for length
       if (message.remaining() < 8) {
           message.rewind();
           return;
       }
   
       byte[] magicBytes = new byte[4];
       message.get(magicBytes);
       String magic = new String(magicBytes, StandardCharsets.UTF_8);
   
       // Dispatch processing based on the magic number
       if ("info".equals(magic)) {
           int length = message.getInt();
           // Simple validity check: length cannot be negative, and there must be enough remaining bytes
           if (length < 0 || message.remaining() < length) {
               message.rewind();
               return;
           }
   
           byte[] payload = new byte[length];
           message.get(payload);
           String infoStr = new String(payload, StandardCharsets.UTF_8);
   
           // Parse JSON using libraries such as Gson or Jackson
           Gson gson = new Gson();
           FCInfoMessage infoMsg = gson.fromJson(infoStr, FCInfoMessage.class);
   
           // You can now prepare to play the soothing message according to infoMsg.function
           System.out.println("Function Call Notification for: " + infoMsg.function);
           // Immediately call sendUserBinaryMessage to play the soothing message...
       } else if ("tool".equals(magic)) {
           // ... Handle the "tool" message here (optional)
       }
   
       // Reset buffer position so that other logic can process it
       message.rewind();
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="dkOwR0HbG7" title="TypeScript">
   <TabTitle>TypeScript</TabTitle>
   
   ```TypeScript
   // Define type interface
   interface FCInfoMessage {
       event_type: string;
       function: string;
       tool_call_id: string;
       response_id: string;
   }
   
   // In the onRoomBinaryMessageReceived callback
   engine.on('onRoomBinaryMessageReceived', (event: { userId: string, message: ArrayBuffer }) => {
       const { userId, message } = event;
       if (message.byteLength < 8) return;
       
       const dataView = new DataView(message);
       const magic = new TextDecoder().decode(message.slice(0, 4));
   
       if (magic === 'info') {
           const length = dataView.getUint32(4, false); // false for big-endian
           const payload = new TextDecoder().decode(message.slice(8, 8 + length));
           
           const infoMsg: FCInfoMessage = JSON.parse(payload);
           
           // You can now prepare to play the soothing message according to infoMsg.function
           console.log(`Function Call Notification for: \\\\${infoMsg.function}`);
           // Immediately call engine.sendUserBinaryMessage to play the soothing message...
           
       } else if (magic === 'tool') {
           // ... Handle tool message here
       }
   });
   ```
   
   
   
   </Tab>
   </Tabs>
   

3. (Optional) Play a soothing message.

   Function execution requires a certain amount of time. After receiving the function calling notification, you can immediately call [sendUserBinaryMessage](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage) to send a control message, allowing the AI to play a soothing message.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the soothing message has not finished playing when the function result is returned, the system will wait for the soothing message to finish before announcing the result.   </div>
   

   * `userId`: The AI identifier (corresponding to `AgentConfig.UserId`).

   * `buffer`: Input the content of the soothing message. The following format must be followed:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6938c15a149ab250b2dd784df71d6190.jpg) </span>

&nbsp;

      
      |Parameter name |Type |Description |
      |---|---|---|
      |magic number |String |Message format identifier. In the current scenario, the message format is fixed as `ctrl`, used to identify the message as a control message. |
      |length |String |Soothing phrase length, in bytes. Stored in big\-endian format. |
      |control_message |String |Soothing phrase configuration information, in JSON string format. Content as follows:<br><br>```JSON```<br>```{```<br>```  "Command": "ExternalTextToSpeech", // Command type, fixed value, indicates text-to-speech```<br>```  "Message": "Querying, please wait patiently.",   // Soothing message text to be played```<br>```  "InterruptMode": 3            // Must be 3, indicating that if the AI is currently interacting, the system will directly discard the incoming soothing message text. If not interacting, the AI will send the soothing message to TTS for playback```<br>```}```<br> |
      

      Example of inputting a soothing message:

      
      <Tabs>
      <Tab zoneid="nb3gvE1nIK" title="C++">
      <TabTitle>C++</TabTitle>
      
      ```C++
      // Send a text-to-speech (TTS) command to let the AI broadcast the specified soothing message content.
      void sendTTSMessage(const std::string &uid, const std::string& content) {
          nlohmann::json json_data;
          json_data["Command"] = "ExternalTextToSpeech";
          json_data["Message"] = content;
          json_data["InterruptMode"] = 3; 
          sendUserBinaryMessage(uid, json_data.dump());
      }
      
      void buildBinaryMessage(const std::string& magic_number, const std::string& message, size_t& binary_message_length, std::shared_ptr<uint8_t[]>& binary_message) {
          auto magic_number_length = magic_number.size();
          auto message_length = message.size();
      
          binary_message_length = magic_number_length + 4 + message_length;
          binary_message = std::shared_ptr<uint8_t[]>(new uint8_t[binary_message_length]);
          std::memcpy(binary_message.get(), magic_number.data(), magic_number_length);
          binary_message[magic_number_length] = static_cast<uint8_t>((message_length >> 24) & 0xFF);
          binary_message[magic_number_length+1] = static_cast<uint8_t>((message_length >> 16) & 0xFF);
          binary_message[magic_number_length+2] = static_cast<uint8_t>((message_length >> 8) & 0xFF);
          binary_message[magic_number_length+3] = static_cast<uint8_t>(message_length & 0xFF);
          std::memcpy(binary_message.get()+magic_number_length+4, message.data(), message_length);
      }
      
      int sendUserBinaryMessage(const std::string &uid, const std::string& message) {
          if (rtcRoom_ != nullptr)
          {
              size_t length = 0;
              std::shared_ptr<uint8_t[]> binary_message = nullptr;
              buildBinaryMessage("ctrl", message, length, binary_message);
              return rtcRoom_->sendUserBinaryMessage(uid.c_str(), static_cast<int>(length), binary_message.get());
          }
          return -1;
      }
      ```
      
      
      
      </Tab>
      <Tab zoneid="Sj8YquUZz4" title="Java">
      <TabTitle>Java</TabTitle>
      
      ```Java
      // Send a text-to-speech (TTS) command to let the agent broadcast the specified soothing message content.
      public void sendTTSMessage(String userId, String content) {
          JSONObject json = new JSONObject();
          try {
              json.put("Command", "ExternalTextToSpeech");
              json.put("Message", content);
              json.put("InterruptMode", 3); 
          } catch (JSONException e) {
              throw new RuntimeException(e);
          }
          String jsonString = json.toString();
          byte[] buildBinary = buildBinaryMessage("ctrl", jsonString);
          sendUserBinaryMessage(userId, buildBinary);
      }
      
      
      private byte[] buildBinaryMessage(String magic_number, String content) {
          byte[] prefixBytes = magic_number.getBytes(StandardCharsets.UTF_8);
          byte[] contentBytes = content.getBytes(StandardCharsets.UTF_8);
          int contentLength = contentBytes.length;
      
          ByteBuffer buffer = ByteBuffer.allocate(prefixBytes.length + 4 + contentLength);
          buffer.order(ByteOrder.BIG_ENDIAN);
          buffer.put(prefixBytes);
          buffer.putInt(contentLength);
          buffer.put(contentBytes);
          return buffer.array();
      }
      
      public void sendUserBinaryMessage(String userId, byte[] buffer) {
          if (rtcRoom_ != null) {
              rtcRoom_.sendUserBinaryMessage(userId, buffer, MessageConfig.RELIABLE_ORDERED);
          }
      }
      ```
      
      
      
      </Tab>
      <Tab zoneid="xqTJcM4hqf" title="TypeScript">
      <TabTitle>TypeScript</TabTitle>
      
      ```TypeScript
      import VERTC from '@volcengine/rtc';
      
      
      const BotName = 'RobotMan_'; // Custom agent name
      const CommandKey = 'ctrl'; 
      const engine = VERTC.createEngine('Your AppID'); // Your RTC application APPId
      
      /**
       *@briefCommand type
       */
      enum COMMAND {
        /**
         *@briefSend a text-to-speech (TTS) command to let the agent broadcast the specified soothing message content.
         */
        EXTERNAL_TEXT_TO_SPEECH = 'ExternalTextToSpeech',
      };
      
      /**
       *@briefMode settings
       */
      enum INTERRUPT_PRIORITY {
        /**
         *@briefComfort phrase mode.
         */
        LOW = 3,
        MEDIUM = 2,
        HIGH = 1
      };
      
      /**
       *@briefWrap the string as TLV
       */
      function stringToTLV(inputString: string, type = '') {
        const typeBuffer = new Uint8Array(4);
      
        for (let i = 0; i < type.length; i++) {
          typeBuffer[i] = type.charCodeAt(i);
        }
      
        const lengthBuffer = new Uint32Array(1);
        const valueBuffer = new TextEncoder().encode(inputString);
      
        lengthBuffer[0] = valueBuffer.length;
      
        const tlvBuffer = new Uint8Array(typeBuffer.length + 4 + valueBuffer.length);
      
        tlvBuffer.set(typeBuffer, 0);
      
        tlvBuffer[4] = (lengthBuffer[0] >> 24) & 0xff;
        tlvBuffer[5] = (lengthBuffer[0] >> 16) & 0xff;
        tlvBuffer[6] = (lengthBuffer[0] >> 8) & 0xff;
        tlvBuffer[7] = lengthBuffer[0] & 0xff;
      
        tlvBuffer.set(valueBuffer, 8);
      
        return tlvBuffer.buffer;
      };
      
      
      /**
       *@briefSend a text-to-speech (TTS) command to have the agent broadcast the specified comfort phrase content.
       */
      engine.sendUserBinaryMessage(
        BotName,
        stringToTLV(
          JSON.stringify({
            Command: COMMAND.EXTERNAL_TEXT_TO_SPEECH,
            Message: '请稍等，正在查询。',
            InterruptMode: INTERRUPT_PRIORITY.LOW,
          }),
          CommandKey,
        )
      );
      ```
      
      
      
      </Tab>
      </Tabs>
      

4. **Obtain function call instruction**.

   After receiving the call notification, you will receive a function call instruction message (the `magic number` is `tool`). You need to parse the `message` to obtain the specific parameters required to execute the function. The format and parsing example of `message` are as follows:

   `message` format:

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a8ec9934817d4348bf3b1eba21194d91) </span>

&nbsp;

   
   |Field name |Type |Description |
   |---|---|---|
   |magic number |String |Message format, fixed as `tool`, indicating that this message is a function call command. |
   |length |String |Function call command message length, in bytes. Stored in big\-endian format. |
   |tool_message |String |Function call command message content. Format as follows:<br><br>```JSON```<br>```{```<br>```  "tool_calls": [```<br>```    {```<br>```      "id": "call_***45",       // Call ID, subsequent responses need to be associated with this ID for receipt```<br>```      "type": "function",       // Fixed value, indicates this is a function call```<br>```      "function": {```<br>```        "name": "get_current_weather",     // Name of the function to be called```<br>```        "arguments": "{\"location\":\"London\"}"  // Parameters required to execute the function, JSON string (note escaping)```<br>```      }```<br>```    }```<br>```  ]```<br>```}```<br> |
   

   `message` parsing example:

   
   <Tabs>
   <Tab zoneid="GXjtajiNb5" title="C++">
   <TabTitle>C++</TabTitle>
   
   ```C++
   // Define C++ struct corresponding to the JSON structure
   struct FunctionCall {
       std::string name;
       std::string arguments; // Note: This is a stringified JSON
   };
   
   struct ToolCall {
       std::string id;
       std::string type;
       FunctionCall function;
   };
   
   
   bool ParseToolMessage(const uint8_t* message, int size, std::vector<ToolCall>& out_calls) {
       // 1. Binary unpacking
       const int kHeaderSize = 8;
       if (size < kHeaderSize) return false;
   
       uint32_t magic = ntohl(*reinterpret_cast<const uint32_t*>(message));
       if (magic != 0x746F6F6C) return false; // "tool"
   
       uint32_t length = ntohl(*reinterpret_cast<const uint32_t*>(message + 4));
       if (size - kHeaderSize != static_cast<int>(length)) return false;
   
       std::string json_str;
       if (length > 0) {
           json_str.assign(reinterpret_cast<const char*>(message) + kHeaderSize, length);
       }
   
       // 2. Parse JSON
       nlohmann::json json_data = nlohmann::json::parse(json_str, nullptr, false);
       if (json_data.is_discarded() || !json_data.contains("tool_calls") || !json_data["tool_calls"].is_array()) return false;
   
       out_calls.clear();
   
       // 3. Iterate and populate the struct
       for (const auto& item : json_data["tool_calls"]) {
           ToolCall tool_call;
           tool_call.id   = item.value("id", "");
           tool_call.type = item.value("type", "");
   
           if (item.contains("function") && item["function"].is_object()) {
               const auto& func_json = item["function"];
               tool_call.function.name      = func_json.value("name", "");
               tool_call.function.arguments = func_json.value("arguments", "{}");
           }
           out_calls.push_back(tool_call);
       }
       return true;
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="ZjMViI7TXd" title="Java">
   <TabTitle>Java</TabTitle>
   
   ```Java
   class FunctionDetails {
       @SerializedName("name")
       public String name;
   
       @SerializedName("arguments")
       public String arguments; // This is a JSON string, may require secondary parsing
   }
   
   // Corresponds to each element in the tool_calls array
   class ToolCall {
       @SerializedName("id")
       public String id; // This is the tool_call_id we need
   
       @SerializedName("type")
       public String type;
   
       @SerializedName("function")
       public FunctionDetails function;
   }
   
   // Corresponds to the top-level JSON object of payload
   class ToolMessagePayload {
       @SerializedName("subscriber_user_id")
       public String subscriberUserId;
   
       @SerializedName("tool_calls")
       public ToolCall[] tool_calls;
   }
   
   
   // File 2: Implement callbacks in your RTC client
   
   class YourRtcClient {
       // ... Other code ...
   
       // In the onRoomBinaryMessageReceived callback
       // @Override
       public void onRoomBinaryMessageReceived(String uid, ByteBuffer message) {
           // Ensure to restore the ByteBuffer position after processing to avoid affecting other handlers
           message.mark();
   
           try {
               message.order(ByteOrder.BIG_ENDIAN);
               if (message.remaining() < 8) return;
   
               byte[] magicBytes = new byte[4];
               message.get(magicBytes);
               String magic = new String(magicBytes, StandardCharsets.UTF_8);
   
               if ("tool".equals(magic)) {
                   int length = message.getInt();
                   if (message.remaining() >= length) {
                       byte[] payloadBytes = new byte[length];
                       message.get(payloadBytes);
                       String payloadStr = new String(payloadBytes, StandardCharsets.UTF_8);
   
                       // Parse using Gson
                       Gson gson = new Gson();
                       ToolMessagePayload toolPayload = gson.fromJson(payloadStr, ToolMessagePayload.class);
   
                       // Safely obtain information about the first function call
                       if (toolPayload != null && toolPayload.tool_calls != null && toolPayload.tool_calls.length > 0) {
                           ToolCall firstCall = toolPayload.tool_calls[0];
                           
                           String toolCallId = firstCall.id; // Successfully obtained tool_call_id!
                           String funcName = firstCall.function.name;
                           String argumentsStr = firstCall.function.arguments;
   
                           System.out.println("FC tool received:");
                           System.out.println("  - Tool Call ID: " + toolCallId);
                           System.out.println("  - Function Name: " + funcName);
                           System.out.println("  - Arguments: " + argumentsStr);
   
                           // argumentsStr is a JSON string and can be further parsed
                           // Map<String, Object> argsMap = gson.fromJson(argumentsStr, Map.class);
                       }
                   }
               }
           } finally {
               // Restore ByteBuffer position
               message.reset();
           }
       }
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="NjvZntu5mq" title="TypeScript">
   <TabTitle>TypeScript</TabTitle>
   
   ```TypeScript
   interface FunctionDetails {
       name: string;
       arguments: string; // This is a JSON string, may require secondary parsing
   }
   
   // Corresponds to each element in the tool_calls array
   interface ToolCall {
       id: string; // This is the tool_call_id we need
       type: string;
       function: FunctionDetails;
   }
   
   // Corresponds to the top-level JSON object of payload
   interface ToolMessagePayload {
       subscriber_user_id: string;
       tool_calls: ToolCall[];
   }
   
   
   // 2. Implement callbacks in your RTC client
   engine.on('onRoomBinaryMessageReceived', (event: { userId: string, message: ArrayBuffer }) => {
       const { userId, message } = event;
       if (message.byteLength < 8) return;
   
       const dataView = new DataView(message);
       const magic = new TextDecoder().decode(message.slice(0, 4));
   
       if (magic === 'tool') {
           const length = dataView.getUint32(4, false); // false for big-endian
           if (message.byteLength < 8 + length) return;
   
           const payloadStr = new TextDecoder().decode(message.slice(8, 8 + length));
           
           // Use the correct top-level interface for parsing
           const toolPayload: ToolMessagePayload = JSON.parse(payloadStr);
           
           // Safely obtain information about the first function call
           if (toolPayload && toolPayload.tool_calls && toolPayload.tool_calls.length > 0) {
               const firstCall = toolPayload.tool_calls[0];
               
               const toolCallId = firstCall.id; // Successfully obtained tool_call_id!
               const funcName = firstCall.function.name;
               const argumentsStr = firstCall.function.arguments;
   
               console.log('FC tool received:', {
                   fromUserId: userId,
                   tool_call_id: toolCallId,
                   function_name: funcName,
                   function_args_str: argumentsStr
               });
               
               // argumentsStr is a stringified JSON and can be further parsed
               try {
                   const args = JSON.parse(argumentsStr);
                   console.log('Parsed arguments:', args);
               } catch (e) {
                   console.error('Failed to parse function arguments string:', e);
               }
           }
       }
   });
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="49bd83b1"></span>
## Step 3: **Execute external function**

After successfully parsing the `tool` message, you need to implement the following in your own business logic:


1. **Route to function**: According to the value of `function.name` (for example, `"get_current_weather"`), call the corresponding function that you have implemented in your own code.

2. **Pass parameters**: Pass the parameters parsed from `function.arguments` in the previous step as input parameters to your function.

3. **Obtain return value**: Execute your function and obtain its return result. This result will be returned in the next step.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning"><code>function.arguments</code> field itself is a string, and its content is a JSON object. Before calling your local function, you must perform another round of JSON parsing on this string to obtain the actual parameters.</div>


<span id=".XzUt5pKt5pS-5bel5YW36LCD55So55qE57uT5p6c5L-h5oGv"></span>
## Step 4: Return **function result**

Call [sendUserBinaryMessage](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage) to return the function execution result to the system, which will then be played by the AI.

<span id="04d3dd85"></span>
### Method 1: Playback after LLM processing

Return the original data from the function to the LLM for processing before playback. This is suitable for scenarios that require summarization, refinement, or other secondary processing.

Call [sendUserBinaryMessage](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage) to input the function execution result, and play it directly.


* `userId`: The identifier ID of the AI (corresponding to `AgentConfig.UserId`).

* `buffer`: Input the function execution result. The following format must be followed:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da013d2aabd3d8c6bdcf225963c927bf.jpg) </span>

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|magic number |String |Message format, fixed as `func`. |
|length |String |The length of the function call result information, in bytes. Stored in big\-endian format. |
|Function_Response |String |Function call result information. |


You can refer to the following sample code to return the function call result information and play it:


<Tabs>
<Tab zoneid="vp6XuCDn9m" title="C++">
<TabTitle>C++</TabTitle>

```C++
// Use the nlohmann/json library for JSON operations
// https://github.com/nlohmann/json
#include "json.hpp"

// For convenience
using json = nlohmann::json;

// --- Configuration ---
// Please replace "RobotMan_" here with the actual UserId you set for the AI
const std::string kAgentUserId = "RobotMan_";


// Function for sending binary messages
// You need to adapt according to the actual SDK interface
void sendUserBinaryMessage(const std::string& userId, const std::vector<uint8_t>& message);


/*** @brief Package the JSON string into a TLV byte stream of type 'func' */
std::vector<uint8_t> stringToTLV(const std::string& content) {
    const std::string type = "func";
    size_t type_len = type.length();
    size_t content_len = content.length();
    size_t total_len = type_len + 4 + content_len;

    std::vector<uint8_t> buffer(total_len);

    // 1. Write Type ("func")
    std::memcpy(buffer.data(), type.data(), type_len);

    // 2. Write Length (big-endian)
    buffer[type_len + 0] = (content_len >> 24) & 0xFF;
    buffer[type_len + 1] = (content_len >> 16) & 0xFF;
    buffer[type_len + 2] = (content_len >> 8) & 0xFF;
    buffer[type_len + 3] = content_len & 0xFF;

    // 3. Write Value (JSON string)
    if (!content.empty()) {
        std::memcpy(buffer.data() + type_len + 4, content.data(), content_len);
    }

    return buffer;
}


/*** @brief Send the response to the function call */
void SendFunctionResponse(const std::string& toolCallID, const std::string& content) {
    json payload;
    payload["ToolCallID"] = toolCallID;
    payload["Content"] = content;

    std::string jsonString = payload.dump();
    
    std::vector<uint8_t> binaryMessage = stringToTLV(jsonString);

    // Send the binary message to the specified AI
    sendUserBinaryMessage(kAgentUserId, binaryMessage);
}
```



</Tab>
<Tab zoneid="ibXvMX3CrE" title="Java">
<TabTitle>Java</TabTitle>

```Java
public void SendFunctionResponse(String ToolCallID, String Content) {
    JSONObject json = new JSONObject();
    try {
        json.put("ToolCallID", ToolCallID);
        json.put("Content", Content);
    } catch (JSONException e) {
        throw new RuntimeException(e);
    }
    String jsonString = json.toString();
    System.out.println(jsonString);

    // Please replace "AgentUserId" with the actual UserId you set for the AI agent
    app.rtcSdkWrap.sendUserBinaryMessage("AgentUserId", stringToTLV(jsonString));
}

public byte[] stringToTLV(String content) {
    String func_type = "func";
    byte[] prefixBytes = func_type.getBytes(StandardCharsets.UTF_8);
    byte[] contentBytes = content.getBytes(StandardCharsets.UTF_8);
    int contentLength = contentBytes.length;

    ByteBuffer buffer = ByteBuffer.allocate(prefixBytes.length + 4 + contentLength);
    buffer.order(ByteOrder.BIG_ENDIAN);
    buffer.put(prefixBytes);
    buffer.putInt(contentLength);
    buffer.put(contentBytes);
    return buffer.array();
}
```



</Tab>
<Tab zoneid="IcoWgXNrbt" title="TypeScript">
<TabTitle>TypeScript</TabTitle>

```TypeScript
import VERTC from '@volcengine/rtc';

/** *@briefWrap the string as TLV */
function stringToTLV(inputString: string) {
  const type = 'func';
  const typeBuffer = new Uint8Array(4);

  for (let i = 0; i < type.length; i++) {
    typeBuffer[i] = type.charCodeAt(i);
  }

  const lengthBuffer = new Uint32Array(1);
  const valueBuffer = new TextEncoder().encode(inputString);

  lengthBuffer[0] = valueBuffer.length;

  const tlvBuffer = new Uint8Array(typeBuffer.length + 4 + valueBuffer.length);

  tlvBuffer.set(typeBuffer, 0);

  tlvBuffer[4] = (lengthBuffer[0] >> 24) & 0xff;
  tlvBuffer[5] = (lengthBuffer[0] >> 16) & 0xff;
  tlvBuffer[6] = (lengthBuffer[0] >> 8) & 0xff;
  tlvBuffer[7] = lengthBuffer[0] & 0xff;

  tlvBuffer.set(valueBuffer, 8);

  return tlvBuffer.buffer;
};

/** *@briefConvert TLV data format to string *@noteTLV data format * | magic number | length(big-endian) | value | *@param {ArrayBufferLike}tlvBuffer
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

/** *@briefReceive toolcall via onRoomBinaryMessageReceived*        Send response via sendUserBinaryMessage */
function handleRoomBinaryMessageReceived(
  event: {
    userId: string;
    message: ArrayBuffer;
  },
) {
  const { message } = event;
  const { type, value } = tlv2String(message);
  const data = JSON.parse(value);
  const tool_calls = data?.tool_calls;
  
  if (tool_calls?.length) {
    // To simplify the example, we only handle the first function call
    const toolCall = tool_calls[0];
    const functionName = toolCall.function.name;
    // Key point: 'arguments' is a JSON string and must be parsed into an object before it can be used
    const functionArgs = JSON.parse(toolCall.function.arguments);

    // Please replace this section with your own function call logic
    // The code below is a generic example, demonstrating how to dynamically generate results based on the function name and parameters.
    // In real scenarios, you need to call your own actual function according to functionName.
    const functionResult = `函数 \\\\${functionName} 已执行，收到的参数为: \\\\${JSON.stringify(functionArgs)}`;
        
    this.engine.sendUserBinaryMessage(
      'Your AI Bot Name',     // Please replace 'Your AI Bot Name' with the actual UserId you set for the AI agent
      stringToTLV(
        JSON.stringify({
          ToolCallID: toolCall.id,
          Content: functionResult, // Return the function execution result
        })
      )
    );
  }
};

/** *@briefListen for binary messages in the room */
this.engine.on(VERTC.events.onRoomBinaryMessageReceived, handleRoomBinaryMessageReceived.bind(this));
```



</Tab>
</Tabs>


<span id=".5pa55byPLTHvvJrnm7TmjqXmkq3mlL7vvIjkuI3nu48tbGxtLeWkhOeQhu-8iQ=="></span>
### Method 2: Direct playback (without LLM processing)

Play the original function result directly via TTS. This is suitable for scenarios where the return result does not require processing or where the reply sentence is long and latency needs to be reduced.

Call the [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage) interface, set the following parameters, input the function call result, and play it:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">To reduce latency, split long reply sentences into several short sentences, and call <a href="https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage">sendUserBinaryMessage</a> multiple times.</div>



* <div data-tips="true" data-tips-type="warning">Sentence splitting recommendation: Split the first clause by comma (，) or semicolon (；); split subsequent clauses by period (。), question mark (？), or other complete sentence punctuation. Avoid splitting decimal points in numbers.</div>


* <div data-tips="true" data-tips-type="warning">Sentence splitting example: <code>The weather is sunny today,</code> <code>The temperature is 10-29 degrees Celsius, with a northerly wind of force three.</code> . <code>In the next seven days, the weather will remain sunny.</code></div>


* `userId`: The identifier ID of the AI (corresponding to `AgentConfig.UserId`).

* `buffer`: Input the function call result information and related configuration. The following format must be followed:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6938c15a149ab250b2dd784df71d6190.jpg) </span>

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|magic number |String |Message format identifier. In the current scenario, the message format is fixed as `ctrl`, which is used to indicate that this message is a control message. |
|length |String |The length of the function call result information, in bytes. Stored in big\-endian format. |
|control_message |String |Function call result configuration information. The specific content format is as follows:<br><br>```JSON```<br>```{```<br>```  "Command": "ExternalTextToSpeech",  // Fixed value```<br>```  "Message": "Here is the result of the function call.",    // Pass in the result of the function call```<br>```  "InterruptMode": 2  // Must be 2; directly play the function result to ensure it is not interrupted.```<br>```}```<br> |


Input example:


<Tabs>
<Tab zoneid="zrdF7tasyR" title="C++">
<TabTitle>C++</TabTitle>

```C++
// Send a text-to-speech (TTS) command to let the AI announce the function call result information
void sendTTSMessage(const std::string &uid, const std::string& content) {
    nlohmann::json json_data;
    json_data["Command"] = "ExternalTextToSpeech";
    json_data["Message"] = content;
    json_data["InterruptMode"] = 2; 
    sendUserBinaryMessage(uid, json_data.dump());
}

void buildBinaryMessage(const std::string& magic_number, const std::string& message, size_t& binary_message_length, std::shared_ptr<uint8_t[]>& binary_message) {
    auto magic_number_length = magic_number.size();
    auto message_length = message.size();

    binary_message_length = magic_number_length + 4 + message_length;
    binary_message = std::shared_ptr<uint8_t[]>(new uint8_t[binary_message_length]);
    std::memcpy(binary_message.get(), magic_number.data(), magic_number_length);
    binary_message[magic_number_length] = static_cast<uint8_t>((message_length >> 24) & 0xFF);
    binary_message[magic_number_length+1] = static_cast<uint8_t>((message_length >> 16) & 0xFF);
    binary_message[magic_number_length+2] = static_cast<uint8_t>((message_length >> 8) & 0xFF);
    binary_message[magic_number_length+3] = static_cast<uint8_t>(message_length & 0xFF);
    std::memcpy(binary_message.get()+magic_number_length+4, message.data(), message_length);
}

int sendUserBinaryMessage(const std::string &uid, const std::string& message) {
    if (rtcRoom_ != nullptr)
    {
        size_t length = 0;
        std::shared_ptr<uint8_t[]> binary_message = nullptr;
        buildBinaryMessage("ctrl", message, length, binary_message);
        return rtcRoom_->sendUserBinaryMessage(uid.c_str(), static_cast<int>(length), binary_message.get());
    }
    return -1;
}
```



</Tab>
<Tab zoneid="fGGDh9CvI9" title="Java">
<TabTitle>Java</TabTitle>

```Java
// Send a text-to-speech (TTS) command to let the agent announce the tool call result information
public void sendTTSMessage(String userId, String content) {
    JSONObject json = new JSONObject();
    try {
        json.put("Command", "ExternalTextToSpeech");
        json.put("Message", content);
        json.put("InterruptMode", 2); 
    } catch (JSONException e) {
        throw new RuntimeException(e);
    }
    String jsonString = json.toString();
    byte[] buildBinary = buildBinaryMessage("ctrl", jsonString);
    sendUserBinaryMessage(userId, buildBinary);
}


private byte[] buildBinaryMessage(String magic_number, String content) {
    byte[] prefixBytes = magic_number.getBytes(StandardCharsets.UTF_8);
    byte[] contentBytes = content.getBytes(StandardCharsets.UTF_8);
    int contentLength = contentBytes.length;

    ByteBuffer buffer = ByteBuffer.allocate(prefixBytes.length + 4 + contentLength);
    buffer.order(ByteOrder.BIG_ENDIAN);
    buffer.put(prefixBytes);
    buffer.putInt(contentLength);
    buffer.put(contentBytes);
    return buffer.array();
}

public void sendUserBinaryMessage(String userId, byte[] buffer) {
    if (rtcRoom_ != null) {
        rtcRoom_.sendUserBinaryMessage(userId, buffer, MessageConfig.RELIABLE_ORDERED);
    }
}
```



</Tab>
<Tab zoneid="xOY4vDBoHp" title="TypeScript">
<TabTitle>TypeScript</TabTitle>

```TypeScript
import VERTC from '@volcengine/rtc';


const BotName = 'RobotMan_'; // Custom agent name
const CommandKey = 'ctrl'; 
const engine = VERTC.createEngine('Your AppID'); // Your RTC application AppId

/**
 *@briefCommand type
 */
enum COMMAND {
  /**
   *@briefSend a text-to-speech (TTS) command to let the agent announce the tool call result information
   */
  EXTERNAL_TEXT_TO_SPEECH = 'ExternalTextToSpeech',
};

/**
 *@briefMode setting
 */
enum INTERRUPT_PRIORITY {
  /**
   *@briefAgent announcement call command message content mode.
   */
  LOW = 3,
  MEDIUM = 2,
  HIGH = 1
};

/**
 *@briefWrap the string as TLV
 */
function stringToTLV(inputString: string, type = '') {
  const typeBuffer = new Uint8Array(4);

  for (let i = 0; i < type.length; i++) {
    typeBuffer[i] = type.charCodeAt(i);
  }

  const lengthBuffer = new Uint32Array(1);
  const valueBuffer = new TextEncoder().encode(inputString);

  lengthBuffer[0] = valueBuffer.length;

  const tlvBuffer = new Uint8Array(typeBuffer.length + 4 + valueBuffer.length);

  tlvBuffer.set(typeBuffer, 0);

  tlvBuffer[4] = (lengthBuffer[0] >> 24) & 0xff;
  tlvBuffer[5] = (lengthBuffer[0] >> 16) & 0xff;
  tlvBuffer[6] = (lengthBuffer[0] >> 8) & 0xff;
  tlvBuffer[7] = lengthBuffer[0] & 0xff;

  tlvBuffer.set(valueBuffer, 8);

  return tlvBuffer.buffer;
};


/**
 *@briefSend a text-to-speech (TTS) command to let the agent announce the specified soothing phrase content.
 */
engine.sendUserBinaryMessage(
  BotName,
  stringToTLV(
    JSON.stringify({
      Command: COMMAND.EXTERNAL_TEXT_TO_SPEECH,
      Message: '上海天气是晴天，25摄氏度',
      InterruptMode: INTERRUPT_PRIORITY.MEDIUM,
    }),
    CommandKey,
  )
);
```



</Tab>
</Tabs>


<span id="65fd645c"></span>
# Advanced Usage and Practice

<span id="fc4bde78"></span>
## Multi\-turn Function Calls

When a user's utterance contains multiple tasks with dependencies (such as "Check the meeting room first, then navigate"), the large model will interact with your service in multiple rounds, sequentially, to gradually complete the tasks.

<span id="407fe687"></span>
#### Typical example


* **User query**: "Help me check the meeting room for my next meeting, then navigate to it."

* **First round (obtain prerequisite)** 

   1. **Model**: Generates the first instruction and calls `get_next_meeting_info()`.

   2. **Your service**: After execution, you must immediately return the result `{"room": "Building A, Room 301 meeting room"}` to the model.

* **Second round (execute dependent action)** 

   1. **Model**: After receiving the result "Building A, Room 301 meeting room" from the first round, based on this information, issues the second instruction and calls `start_navigation(destination="Building A, Room 301 meeting room")`.

   2. **Your service**: After execution, immediately return the result `{"status": "Navigation has been started"}` to the model again.

* **End (summary reply)** 

   * **Model**: Confirms all steps are completed and generates the final reply: "Navigation to Building A, Room 301 meeting room has been started for you."


<span id="134f18bb"></span>
#### Implementation method


1. **Start session**: Call `StartVoiceChat` and provide all possible functions in the `Tools` parameter.

2. **Receive and execute instructions**: Your backend service will receive a `tool_calls` instruction.

3. **Execute function**: Execute the corresponding function in your code.

4. **Fill in result**: Return the function execution result to the large model service via the `UpdateVoiceChat` interface.

5. **Loop and wait**: The large model will decide, based on the result you returned, whether to generate the next function call instruction or to generate the final text reply. You only need to repeat steps 2–4 in a loop until you no longer receive `tool_calls` instructions.


<span id="JMB9sbq3Mf"></span>
## Improve FC Triggering Accuracy

To prevent the large model from incorrectly triggering external functions (Function Calling) in irrelevant or ambiguous scenarios, you can use the following methods to improve the triggering accuracy of Function Calling.

<span id="mNx7OCzday"></span>
### Declare high\-quality tools

When declaring tools via `LLMConfig.Tools` in the `StartVoiceChat` interface, provide clear and accurate tool declarations:


* `name`: Use a clear and semantic English name, for example, `get_current_weather`, instead of `tool_1` or `my_func`.

* `description`: Clearly describe the core purpose of the function in a single sentence.

   * (Not recommended) `"description": "A weather tool."`

   * (Recommended) `"description": "Retrieves real-time weather information for a specified city."`

* `parameters`: Clearly explain the purpose and format requirements of the parameters, and provide examples.

   * (Not recommended) `"description": "Location"`

   * (Recommended) `"description": "The city name for the weather query, for example, 'Shanghai'. Do not include province information."`


<span id="call-history"></span>
### Preserve tool call history

If your use case requires the model to continue referencing previous tool execution results in later turns, such as "plan the itinerary based on the weather you just checked" or "process a refund based on the order details returned in the previous turn," set `LLMConfig.EnableToolCallHistory` to `true` in the `StartVoiceChat` request.

When enabled, the system writes tool call instructions and tool return results into subsequent context as part of the corresponding conversation turn. This helps reduce cases where the model overlooks results that have already been returned. If no Function Calling is triggered in a given turn, that turn still contains only the user's question and the final response, and no additional tool call history is added.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This parameter takes effect only when <code>LLMConfig.Tools</code> is configured and Function Calling is actually triggered.</div>


* <div data-tips="true" data-tips-type="warning"><code>HistoryLength</code> is still counted by conversation turn. One completed user query and its final response count as one turn. If a tool call is triggered in between, the tool call instructions and tool return results are included in that same turn. They do not increase the <code>HistoryLength</code> count and are retained or evicted together with that turn.</div>



<span id="MOPZrkXT3d"></span>
### Design system prompts

Use system prompts (`LLMConfig.SystemMessages`) to specify function calling conditions for the model, which allows you to precisely control the model's tool\-calling behavior.

<span id="akRZpR1X7a"></span>
#### Guiding principles


* **Intent matching**: Only call the function when the user's intent clearly matches the tool's functionality.

* **Proactive clarification**: When the user's intent is ambiguous or necessary parameters are missing, you should clarify by asking questions rather than guessing.

* **Preventing hallucination**: Do not call undeclared tools or fabricate values for parameters.


<span id="efd18865"></span>
#### Example prompt

You can refer to the following template and adjust it according to your business scenario:


<Tabs>
<Tab zoneid="q9Eq40lphE" title="Prompt example">
<TabTitle>Prompt example</TabTitle>

```Plain
## Tool calling rules
You have the following tools. Only call a tool when you accurately identify that the user's intent matches the function of one of the tools below:
adjust_volume (Adjust volume): Only call this when the user expresses any desire to change the device volume. For example, "I cannot hear you clearly," "It is too loud," "Mute it," "Turn up the volume," and more.
get_current_weather (Query weather): Only call this when the user expresses a desire to know weather information. For example, "Will it rain in Hangzhou tomorrow?", "Help me check the weather in Shanghai," "Is it cold outside?", and more.
If the user's intent does not match the trigger conditions for any of the tools above, do not call any tool; engage in direct conversation instead. If the user's intent is ambiguous, clarify it by asking questions.
```



</Tab>
<Tab zoneid="JS8pGQIdOZ" title="Corresponding SystemMessages example">
<TabTitle>Corresponding SystemMessages example</TabTitle>

```JSON
"LLMConfig": {
    // ... Other LLM parameters, such as Mode, Tools ...
    "SystemMessages": [
        // ... This section can include other role settings or behavioral guidelines ...
        "## Tool Calling Rules\\nYou have the following tools. Only call a tool when you accurately identify that the user's intent matches the function of one of the tools below:\\n1. `adjust_volume` (Adjust Volume): Call only when the user expresses any desire to change the device volume. For example, \"I can't hear clearly\", \"The sound is too loud\", \"Mute it for me\", \"Turn up the volume\", etc.\\n2. `get_current_weather` (Check Weather): Call only when the user expresses a desire to know meteorological information. For example, \"Will it rain in Hangzhou tomorrow?\", \"Help me check the weather in Shanghai\", \"Is it cold outside?\", etc.\\nIf the user's intent does not match the trigger conditions of any of the tools above, it is strictly prohibited to call any tool; please converse directly. If the user's intent is ambiguous, please ask questions to clarify their intent."
    ]
}
```



</Tab>
</Tabs>


<span id="78df3196"></span>
# FAQ


* Q1: After configuring Function Calling, is it possible not to read out the function call result information returned to the AI via `updateVoiceChat/sendUserBinaryMessage`?

   No, it is not possible.

* Q2: After configuring Function Calling, how are the related configurations updated?

   You need to first call the `StopVoiceChat` API to stop the AI conversation task, and then call the `StartVoiceChat` API to reconfigure the Function Calling feature.
