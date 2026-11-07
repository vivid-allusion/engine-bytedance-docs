---
title: "Turn-end Detection and Dialogue Triggering"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1544164"
---

The ability to accurately determine whether the user's utterance has ended and trigger an AI response directly affects the naturalness and fluency of the conversation. If turn\-end detection or triggering timing is inappropriate, it may cause the AI to 'interrupt' (responding too early) or 'respond sluggishly' (responding too late). You can control the triggering of AI responses either automatically or manually.


* **Automatic mode**: Based on the user's silence duration or semantic turn\-end detection, the system automatically determines whether the user's utterance has ended and triggers an AI response. Suitable for most natural conversation scenarios.

* **Manual mode**: Manually trigger an AI response via API commands (such as button presses) or subtitle results. Suitable for scenarios that require precise control of the interaction flow.


<span id=".5bqU55So5Zy65pmv"></span>
## Use Cases

&nbsp;


|Scenario |Description |
|---|---|
|Consultation and practice |* Automatic trigger: After the user freely narrates or asks a question, a new round of conversation is automatically triggered.<br><br>* Manual trigger: The user inputs by pressing the "Hold to talk" button, and releasing the button immediately triggers the AI response. |
|Online education |* Automatic trigger: Students can ask the AI assistant questions at any time, and the system automatically detects the end of the question and provides an answer.<br><br>* Manual trigger: Students click the "Ask" button to start speaking, click again to end, and the answer is triggered after the question is fully submitted. |


<span id=".6Ieq5Yqo6Kem5Y-R5paw5LiA6L2u5a-56K-d"></span>
## Automatic Triggering

<span id=".6buY6K6k562W55Wl"></span>
### Default Strategy

By default, the system monitors voice activity in real time. When the user's pause exceeds the preset silence duration `ASRConfig.VADConfig.SilenceTime` (default is 600 ms), the system considers the utterance to be complete and triggers an AI response.


* **Default configuration**

   * `ASRConfig.TurnDetectionMode`: 0, which enables automatic triggering of a new round of dialogue.

   * `ASRConfig.VADConfig.SilenceTime`: Default is 600 ms. If the user's pause duration exceeds this configured value, the system considers the sentence to be complete.

* **Limitations**

   * **Sluggish response**: For fast\-paced conversations, a 600 ms wait may be too long, causing the AI to wait an extra moment after the user finishes speaking before responding, which feels like a delayed AI response.

   * **Premature interruption (AI interrupting)**  : For slow speech or complex conversations that require thinking pauses, 600 ms may be too short. Normal pauses between sentences may be misjudged as the end, causing a sentence to be split into multiple rounds of invalid dialogue.


<span id=".5omL5Yqo6Kem5Y-R5paw5LiA6L2u5a-56K-d"></span>
## Manual Triggering

Trigger a new round of dialogue based on received end signals or subtitle results to achieve precise and reliable interaction control.

<span id=".5q2l6aqkLTHvvJrnvJblhpnop6blj5Hml7bmnLrpgLvovpE="></span>
### Step 1: Define **Trigger Timing**

Clearly specify the points for triggering AI responses in your business logic. Common methods include:


* **Based on business signaling**: Triggered by specific in\-app events and requires customization. For example: when the user releases the "Hold to talk" button, clicks the "Send" button on the UI, or completes payment verification.

* **Based on subtitle results**: Triggered after obtaining a complete speech recognition result. For example, when the `paragraph` field in the subtitle callback message is `true`, it indicates that the user's entire utterance has ended, which triggers a new round of conversation. For information on how to receive and parse subtitle callbacks, see [Real-time Subtitles (Dialog Records)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284).


<span id=".5q2l6aqkLTLvvJrorr7nva7miYvliqjop6blj5HmlrDkuIDova7lr7nor53mqKHlvI8="></span>
### Step 2: **Enable Manual Trigger Mode**

When calling the `StartVoiceChat` API, set `ASRConfig.TurnDetectionMode` to `1`.

<span id=".5q2l6aqkLTPvvJrmiYvliqjop6blj5HmlrDkuIDova7lr7nor50="></span>
### Step 3: **Perform Manual Trigger**

After receiving input business signaling or subtitle results, depending on your business architecture, you can send instructions from either the server or client to trigger a new round of conversation.

<span id=".6YCa6L-H5pyN5Yqh56uv6Kem5Y-R5paw5LiA6L2u5a-56K-d"></span>
#### Trigger via server

Call the `UpdateVoiceChat` API and set `Command` to `FinishSpeechRecognition`. Configuration example:

```JSON
{
  "AppId": "YOUR_AppId",     //  Consistent with StartVoiceChat
  "RoomId": "YOUR_RoomId",      //  Consistent with StartVoiceChat
  "TaskId": "YOUR_TaskId",      //  Consistent with StartVoiceChat
  "Command": "FinishSpeechRecognition" //Must be this value
}
```


<span id=".6YCa6L-H5a6i5oi356uv6Kem5Y-R5paw5LiA6L2u5a-56K-d"></span>
#### Trigger via client

Call the RTC SDK's `sendUserBinaryMessage` API to send a binary message in a specific format to trigger a new round of conversation.


* `userId`: The AI's ID, which must be consistent with the definition in `StartVoiceChat`.

* `buffer`: A binary data block that must be encapsulated in TLV (Type\-Length\-Value) format. As shown below:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5f49c0ca26d16c6e300267b8fd76ef6.jpg) </span>

&nbsp;

   
   |Parameter name |Type |Description |
   |---|---|---|
   |magic_number |binary |Message format identifier, fixed as `ctrl`. |
   |length |binary |Byte length of the message body `control_message`, stored in big\-endian format. |
   |control_message |binary |Message content, which itself is a JSON\-formatted string. Content is as follows (`Command` is a fixed value):<br><br>`{"Command": "FinishSpeechRecognition"}`. |
   


<span id="1804044c"></span>
##### Configuration example


<Tabs>
<Tab zoneid="cWzjG5AOWs" title="C++">
<TabTitle>C++</TabTitle>

```C++
// Send command to trigger a new round of dialogue
void sendFinishRecognitionMessage(const std::string &uid) {
    nlohmann::json json_data;
    json_data["Command"] = "FinishSpeechRecognition";
    sendUserBinaryMessage(uid, json_data.dump());
}
void buildBinaryMessage(const std::string& magic_number, const std::string& message, size_t& binary_message_length, std::shared_ptr<uint8_t[]>& binary_message) { //Wrap the string in TLV format
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
    return -1;}
```



</Tab>
<Tab zoneid="W76Uku0bng" title="Java">
<TabTitle>Java</TabTitle>

```Java
// Send command to trigger a new round of dialogue
public void sendFinishRecognitionMessage(String userId) {
    JSONObject json = new JSONObject();
    try {
        json.put("Command", "FinishSpeechRecognition");
    } catch (JSONException e) {
        throw new RuntimeException(e);
    }
    String jsonString = json.toString();
    byte[] buildBinary = buildBinaryMessage("ctrl", jsonString);
    sendUserBinaryMessage(userId, buildBinary);
}
private byte[] buildBinaryMessage(String magic_number, String content) { //Wrap the string in TLV format
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
<Tab zoneid="pWX63z5mY4" title="TypeScript">
<TabTitle>TypeScript</TabTitle>

```TypeScript
import VERTC from '@volcengine/rtc';

/**
 *@briefAgent configuration
 */
const BotName = 'RobotMan_'; // Agent name
const CommandKey = 'ctrl'; // Control command
const engine = VERTC.createEngine('Your AppID'); // RTC application AppId

/**
 *@briefCommand type
 */
enum COMMAND {
  /**
   *@briefTrigger command for a new round of dialogue
   */
  FinishSpeechRecognition = 'FinishSpeechRecognition',
};


/**
 *@briefWrap the string in TLV format
 */
function stringToTLV(inputString: string, type = '') {
  const typeBuffer = new Uint8Array(type.length);

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
 *@briefSend command to trigger a new round of dialogue
 */
engine.sendUserBinaryMessage(
  BotName,
  stringToTLV(
    JSON.stringify({
      Command: COMMAND.FinishSpeechRecognition,
    }),
    CommandKey,
  )
);

```



</Tab>
</Tabs>
