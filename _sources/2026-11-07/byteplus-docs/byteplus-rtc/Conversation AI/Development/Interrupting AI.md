---
title: "Interrupting AI"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1511927"
---

You can interrupt AI speech either automatically via voice or manually, starting a new round of conversation to enhance the fluency and naturalness of interactions.


* **Automatic interruption**: The system automatically determines and interrupts AI based on the user's voice input.

* **Manual interruption**: The user actively initiates an interruption request (such as clicking a button or sending a command). This operation can be implemented on the client side or server side.


<span id="b7a756a1"></span>
## Use Cases

&nbsp;


|Use cases |Description |
|---|---|
|**Intelligent customer service** |Use a shorter automatic interruption duration, combined with manual interruption, to achieve rapid response and precise control. |
|**Online education** |Use a longer automatic interruption duration to avoid mistakenly interrupting student speech. Teachers can use manual interruption for necessary intervention. |
|**Multi\-person meetings** |Combine automatic and manual interruption to flexibly manage speaking rights. |


<span id=".6K-t6Z-z6Ieq5Yqo5omT5pat"></span>
## Automatic Interruption

<span id="8ded9748"></span>
### Enable Automatic Interruption

Once the system detects the user making a sound, AI immediately stops speaking.


* **Key configuration**:

   When calling `StartVoiceChat`, the following parameters in the `Config` object remain at their default values:

   * `InterruptMode`: Remains at the default value `0`.

   * `VADConfig.SilenceTime`: It is recommended to keep the default value (600 ms) or adjust appropriately according to the specific scenario (for example, 800 ms \- 1200 ms) to ensure the user has enough time to fully express their intent after triggering the interruption, and to avoid incomplete voice input caused by premature termination of VAD (Voice Activity Detection).

* **Sample request**:

   ```JSON
   "Config": {
       // InterruptMode default value is 0, which enables this strategy
       "ASRConfig": {
           // ... Other necessary ASR configurations ...
           "VADConfig": {
               "SilenceTime": 600 // Adjustable as needed
           }
       }
       // ... Other TTSConfig, LLMConfig, and similar configurations ...
   }
   ```
   


<span id=".5Z-65LqO55So5oi35oyB57ut6K-06K-d5pe26Ze05omT5pat"></span>
### Disable Automatic Interruption

To ensure that AI speech is not interrupted by the user's voice, set `Config.InterruptMode` to `1` when calling `StartVoiceChat`.

<span id=".5omL5Yqo5omT5pat"></span>
## Manual Interruption

The user can interrupt AI speech by interacting, such as clicking a button.

<span id=".6YCa6L-H5pyN5Yqh56uv5a6e546w5omL5Yqo5omT5pat"></span>
### Server\-Side Implementation

Call the `UpdateVoiceChat` API and set the `Command` parameter to `interrupt`.

```json
{
  "AppId": "YOUR_AppId",     //  Same as StartVoiceChat
  "RoomId": "YOUR_RoomId",      //  Same as StartVoiceChat
  "TaskId": "YOUR_TaskId",      //  Same as StartVoiceChat
  "Command": "interrupt" // Must be set to "interrupt"
}
```


<span id=".6YCa6L-H5a6i5oi356uv5a6e546w5omL5Yqo5omT5pat"></span>
### Client\-Side Implementation

On the client, call the `ByteRTC SDK` `sendUserBinaryMessage` API to send a binary message in a specific format to interrupt AI speech.


* `userId`: Enter the AI's ID (that is, the AgentConfig.UserId configured in `StartVoiceChat`).

* `buffer`: Content must be in a specific format.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5f49c0ca26d16c6e300267b8fd76ef6.jpg) </span>

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|magic_number |binary |Message format identifier. In the current scenario, the message format is fixed as `ctrl`, used to identify this message as a control message. |
|length |binary |Length of the interrupt message, in bytes, stored in big\-endian format, used to indicate the byte length of the `control_message` field. |
|control_message |binary |Configuration information for interrupt actions, in JSON format. As shown below:<br><br>```JSON```<br>```{```<br>```  "Command": "interrupt"```<br>```}```<br> |


Please refer to the following code sample to construct and send the binary message:


<Tabs>
<Tab zoneid="A8AIddJZGp" title="C++">
<TabTitle>C++</TabTitle>

```C++
// Send interrupt command
void sendInterruptMessage(const std::string &uid) {
    nlohmann::json json_data;
    json_data["Command"] = "interrupt";
    sendUserBinaryMessage(uid, json_data.dump());
}
void buildBinaryMessage(const std::string& magic_number, const std::string& message, size_t& binary_message_length, std::shared_ptr<uint8_t[]>& binary_message) { // Wrap the string in TLV format
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
        return rtcRoom_->sendUserBinaryMessage(uid.c_str(), static_cast<const void*>(binary_message.get()), length);
    }
    return -1;
}
```



</Tab>
<Tab zoneid="AP4CtsLfuD" title="Java">
<TabTitle>Java</TabTitle>

```Java
// Send interrupt command
public void sendInterruptMessage(String userId) {
    JSONObject json = new JSONObject();
    try {
        json.put("Command", "interrupt");
    } catch (JSONException e) {
        throw new RuntimeException(e);
    }
    String jsonString = json.toString();
    byte[] buildBinary = buildBinaryMessage("ctrl", jsonString);
    sendUserBinaryMessage(userId, buildBinary);
}
private byte[] buildBinaryMessage(String magic_number, String content) { // Wrap the string in TLV format
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
<Tab zoneid="aNAsbHLAOb" title="TypeScript">
<TabTitle>TypeScript</TabTitle>

```TypeScript
import VERTC from '@volcengine/rtc';

/**
 *@brief Agent configuration
 */
const BotName = 'RobotMan_'; // Custom agent name
const CommandKey = 'ctrl';
const engine = VERTC.createEngine('Your AppID'); // RTC application AppId

/**
 *@brief Command type
 */
enum COMMAND {
  /**
   *@brief Interrupt command
   */
  INTERRUPT = 'interrupt',
};


/**
 *@brief Wrap the string in TLV format
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
}

/**
 *@brief Send interrupt command
 */
engine.sendUserBinaryMessage(
  BotName,
  stringToTLV(
    JSON.stringify({
      Command: COMMAND.INTERRUPT,
    }),
    CommandKey,
  )
);
```



</Tab>
</Tabs>


<span id=".5o6l5pS25omT5pat6YCa55-l"></span>
## Receive Interruption Notifications

You can subscribe to status callbacks in real time via the application server or client to receive notifications when the AI is interrupted. For specific operations, see [Obtain AI Status](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216).

<span id="faq"></span>
## FAQ

<span id=".5aaC5L2V6K6-572u5omT5pat54G15pWP5bqm77yM5p2l6YG_5YWN6IOM5pmv5Zmq6Z-z5oiW6Ieq5bex5aOw6Z-z5omT5pat5pm66IO95L2T77yf"></span>
### **How to reduce false interruptions caused by background noise?** 

You can try one or more of the following methods:


* **Method 1: Enable noise reduction**

   By adjusting volume gain, enabling AI noise reduction or voiceprint noise reduction, you can remove background noise and reduce invalid interruptions triggered by noise being misrecognized as speech.

* **Method 2: Disable automatic speech interruption and use manual interruption**

   Disable the automatic speech interruption feature, allowing users to proactively initiate interruption based on their needs and judgment. For specific operations, please refer to [Disable Automatic Interruption](https://docs.byteplus.com/docs/byteplus-rtc/docs-1511927#.5Z-65LqO55So5oi35oyB57ut6K-06K-d5pe26Ze05omT5pat) and [Manual Interruption](https://docs.byteplus.com/docs/byteplus-rtc/docs-1511927#.5omL5Yqo5omT5pat).


<span id=".dmFkLeWvueivremfs-aJk-aWreaMgee7reaXtumVv-acieW9seWTjeWQl--8nw=="></span>
### Does VAD affect the duration of speech interruption?

`SilenceTime` does not directly change the `InterruptSpeechDuration` threshold. However, if `SilenceTime` is set too short, the system might detect the end of speech prematurely. This can prevent the user's speaking duration from reaching the `InterruptSpeechDuration` threshold, causing the interruption to fail. Please ensure that `SilenceTime` is greater than `InterruptSpeechDuration`.

<span id=".5aaC5pm66IO95L2T6K-06K-d5pe26KKr5omT5pat77yM5bey57uP6L6T5Ye655qE5YaF5a655Lya5a2Y5YWl5LiK5LiL5paH5ZCX77yf"></span>
### If AI speech is interrupted, will the content already output be stored in the context?

No. The interrupted portion is discarded and is not added to LLM conversation history.
