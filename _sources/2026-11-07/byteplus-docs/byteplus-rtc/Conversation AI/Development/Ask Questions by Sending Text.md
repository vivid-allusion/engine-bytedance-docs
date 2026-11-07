---
title: "Ask Questions by Sending Text"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-2129096"
---

In addition to voice input, you can simulate user input by sending text commands, directly ask questions to the AI, and immediately receive a voice response.

<span id="use-cases"></span>
## Use Cases

&nbsp;


|Scenario |Description |
|---|---|
|E\-commerce live streaming |Send questions raised by viewers in live chat or private messages in real time to the AI host during the live stream for answers. |
|Special content input |When questions contain rare characters, technical terms, complex encoding, or many homophones, users can ensure the accuracy of their questions by entering text. |


<span id="server-side-implementation"></span>
## Server\-Side Implementation

Call the `UpdateVoiceChat` API to pass in the large model context. Refer to the following example:

```JSON
{
  "AppId": "YOUR_AppId",             // Same as StartVoiceChat
  "RoomId": "YOUR_RoomId",           // Same as StartVoiceChat
  "TaskId": "YOUR_TaskId",           // Same as StartVoiceChat
  "Command": "ExternalTextToLLM",    // Must be this value
  "Message": "Give some item build suggestions. User's current status: lagging in gold, mage, squishy.",  // Enter custom text. The text must end with punctuation.
  "InterruptMode": 2 // Enter the processing priority for the large model context content. 2 indicates medium priority. The AI will send the text to the large model for processing after the current interaction ends.
}
```


<span id="client-side-implementation"></span>
## Client\-Side Implementation

Call the client API [sendUserBinaryMessage (using Android as an example)](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#senduserbinarymessage) to construct a control message with `Command` set to `ExternalTextToLLM`.


* `userId`: Enter the AI identifier (that is, `StartVoiceChat` configuration's `AgentConfig.UserId`).

* `buffer`: Must follow the TLV binary format:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5f49c0ca26d16c6e300267b8fd76ef6.jpg) </span>

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|magic_number |binary |Message format identifier. In the current scenario, the message format is fixed as `ctrl` and is used to identify this message as a control message. |
|length |binary |Length of the large model context message to be passed in, in bytes, stored in big\-endian format. This indicates the byte length of the `control_message` field. |
|control_message |binary |Large model context configuration information to be passed in, in JSON format. For the specific content format, see `control_message`. |


control_message

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|Command |String |Control command. Enter `ExternalTextToLLM` here. |
|Message |String |Large model context content to be passed in. The text must end with punctuation and not exceed 200 characters. |
|InterruptMode |Int |Processing priority for the large model context content to be passed in.<br><br><br>* `1`: High priority. AI will terminate the current interaction, send the text to the large model for processing, and output the result.<br><br>* `2`: Medium priority. After the current interaction ends, AI will send the text to the large model for processing and output the result.<br><br>* `3`: Low priority. If AI is currently interacting, it will immediately discard the incoming text content. If AI is not interacting, it will send the text to the large model for processing and output the result. |


You can refer to the following example to implement custom input of large model context from the client.

```C++
// Pass in large model context information
void sendLLMMessage(const std::string &uid, const std::string& content) {
    nlohmann::json json_data;
    json_data["Command"] = "ExternalTextToLLM";
    json_data["Message"] = content;
    json_data["InterruptMode"] = 1; 
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

// userId is the ID of the AI in the room (corresponds to AgentConfig.UserId in StartVoiceChat)
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


```Java
// Pass in large model context information
public void sendLLMMessage(String userId, String content) {
    JSONObject json = new JSONObject();
    try {
        json.put("Command", "ExternalTextToLLM");
        json.put("Message", content);
        json.put("InterruptMode", 1); // InterruptMode optional values: 1, 2, 3
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
// userId is the ID of the AI in the room (corresponds to AgentConfig.UserId in StartVoiceChat)
public void sendUserBinaryMessage(String userId, byte[] buffer) {
    if (rtcRoom_ != null) {
        rtcRoom_.sendUserBinaryMessage(userId, buffer, MessageConfig.RELIABLE_ORDERED);
    }
}
```


```TypeScript
import VERTC from '@volcengine/rtc';
const BotName = 'RobotMan_';  // The ID of the AI in the room (corresponds to AgentConfig.UserId in StartVoiceChat)
const CommandKey = 'ctrl';
const engine = VERTC.createEngine('<YOUR_APP_ID>'); // Replace <YOUR_APP_ID> with your actual AppID

/**
 *@briefInstruction type
 */
enum COMMAND {
  /**
   *@briefPass in large model context information
   */
  EXTERNAL_TEXT_TO_LLM = 'ExternalTextToLLM',
};

/**
 *@briefType of interruption
 */
enum INTERRUPT_PRIORITY {
  /**
   *@briefPlaceholder
   */
  NONE,
  /**
   *@briefHigh priority. The system will terminate the current interaction, send the text to the large model for processing, and output the result.
   */
  HIGH,
  /**
   *@briefMedium priority. After the current interaction ends, the system will send the text to the large model for processing and output the result.
   */
  MEDIUM,
  /**
   *@briefLow priority. If AI is currently interacting, the system will immediately discard the incoming text content. If AI is not interacting, it will send the text to the large model for processing and output the result.
   */
  LOW,
};

/**
 *@briefWrap the string in TLV format.
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
 *@briefPass in large model context information
 */
engine.sendUserBinaryMessage(
  BotName,
  stringToTLV(
    JSON.stringify({
      Command: COMMAND.EXTERNAL_TEXT_TO_LLM,
      Message: "Give some item build suggestions. User's current status: lagging in gold, mage, squishy.",
      InterruptMode: INTERRUPT_PRIORITY.HIGH,
    }),
    CommandKey,
  )
);
```
