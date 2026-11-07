---
title: "Pause or Resume AI Playback"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-2389913"
---

While the AI is speaking, you can pause or resume audio playback at any time via a server API or client command—just like controlling a music player.

<span id="25b908f4"></span>
## Use Cases

&nbsp;


|Scenario |Description |
|---|---|
|Interactive Teaching |While an AI instructor is explaining a concept, students can pause the audio at any time to take notes or reflect deeply, and then resume playback when ready. |
|Content Listening |When listening to long articles or stories, users can pause and resume as needed, giving them full control over their listening pace. |
|Task Guidance |In multi\-step operational guidance, users can pause after each instruction, complete the current step, and then proceed to receive the next one. |


<span id="50f17082"></span>
## Limitation

This feature only works while the AI is actively performing TTS narration and is valid only for the current conversation turn. If the user interrupts and starts a new conversation turn, the pause state from the previous turn is automatically invalidated.

<span id="2e61c321"></span>
## Implementation

Based on your business requirements, you can choose to control the AI's narration state by sending commands through either a server\-side API or a client\-side SDK.

<span id="050818b6"></span>
### Method 1: Server\-Side Implementation

Call the `UpdateVoiceChat` API, set the `Command` field to `AudioCtrl`, and use `AudioConfig.Action` to control pausing or resuming playback.

> Replace `Your_AppId`, `Your_RoomId`, and `Your_TaskId` with your actual App ID, Room ID, and Task ID.


```JSON
{
    "AppId": "Your_AppId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Command": "AudioCtrl",
    "AudioConfig": {
         "Action": "pause"  // Use "pause" to pause, "play" to resume
    }
}
```


<span id="5c49b558"></span>
### Method 2: Client\-Side Implementation

On the client, call the ByteRTC SDK's `sendUserBinaryMessage` method (using the Android platform as an example) to send a binary message in a specific format to control the playback.


* `userId`: Fill in the AI's ID (i.e., the `AgentConfig.UserId` configured in `StartVoiceChat`).

* `buffer`: The content must be in a specific format.

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |magic_number |binary |Message identifier, fixed as `ctrl`. |
   |length |binary |Length of the `control_message`, 4 bytes, in big\-endian order. |
   |control_message |binary |A JSON\-formatted control command, with the following structure:<br><br>```JSON```<br>```{```<br>```    "Command": "AudioCtrl",  // Fixed value```<br>```    "AudioConfig": {```<br>```        "Action": "pause" // Use "pause" to pause, "play" to resume```<br>```    }```<br>```}```<br> |
   

   Code Examples:



<Tabs>
<Tab zoneid="fQUqfn9tuB" title="Java">
<TabTitle>Java</TabTitle>

```Java
// Example of pausing playback
public void pauseAudio(String botUserId) {
    JSONObject json = new JSONObject();
    try {
        JSONObject audioConfig = new JSONObject();
        audioConfig.put("Action", "pause");
        
        json.put("Command", "AudioCtrl");
        json.put("AudioConfig", audioConfig);
    } catch (JSONException e) {
        e.printStackTrace();
    }

    byte[] buildBinary = buildBinaryMessage("ctrl", json.toString());
    rtcRoom.sendUserBinaryMessage(botUserId, buildBinary, MessageConfig.RELIABLE_ORDERED);
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
```



</Tab>
<Tab zoneid="ruhDUdjkc9" title="C++">
<TabTitle>C++</TabTitle>

```C++
// Example of pausing playback
void sendPauseMessage(const std::string &botUserId) {
    nlohmann::json json_data;
    json_data["Command"] = "AudioCtrl";
    json_data["AudioConfig"]["Action"] = "pause";
    
    std::string message = json_data.dump();
    std::string magic = "ctrl";
    uint32_t msg_len = message.size();

// Construct binary packet: magic (4 bytes) + length (4 bytes) + body
    std::vector<uint8_t> buffer;
    buffer.insert(buffer.end(), magic.begin(), magic.end());
    buffer.push_back((msg_len >> 24) & 0xFF);
    buffer.push_back((msg_len >> 16) & 0xFF);
    buffer.push_back((msg_len >> 8) & 0xFF);
    buffer.push_back(msg_len & 0xFF);
    buffer.insert(buffer.end(), message.begin(), message.end());

    rtcRoom_->sendUserBinaryMessage(botUserId.c_str(), buffer.size(), buffer.data());
}
```



</Tab>
<Tab zoneid="id0YbIWF1I" title="TypeScript">
<TabTitle>TypeScript</TabTitle>

```TypeScript
// Example of pausing playback
const message = JSON.stringify({
  Command: 'AudioCtrl',
  AudioConfig: { Action: 'pause' }
});

function stringToTLV(message: string, magic_number: string): Uint8Array {
  const encoder = new TextEncoder();
  const prefixBytes = encoder.encode(magic_number);
  const contentBytes = encoder.encode(message);
  const contentLength = contentBytes.length;

  const buffer = new ArrayBuffer(prefixBytes.length + 4 + contentLength);
  const view = new DataView(buffer);
  const uint8Array = new Uint8Array(buffer);

  uint8Array.set(prefixBytes, 0);
  view.setUint32(prefixBytes.length, contentLength, false);
  uint8Array.set(contentBytes, prefixBytes.length + 4);

  return uint8Array;
}

// Use the stringToTLV method to wrap the message
engine.sendUserBinaryMessage(
  botUserId,
  stringToTLV(message, 'ctrl')
);
```



</Tab>
</Tabs>


<span id="c1786e15"></span>
## Advanced: Synchronized Pause and Resume for Audio and Subtitles

The pause/resume playback feature itself does not depend on subtitles. However, if you wish the subtitles to also pause and resume rendering in sync with the audio, you must set `SubtitleConfig.SubtitleMode` to `2` (Audio Frame\-Aligned Subtitles) when calling the `StartVoiceChat` API. For more details, please refer to [Audio-Subtitle Synchronization (Audio-frame Aligned)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#8c3d69df).
