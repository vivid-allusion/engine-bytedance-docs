---
title: "Real-time Call Subtitles and Translation"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/real-time-call-subtitles-and-translation-server-side"
---

Transcribe speech in an RTC room or a WTN stream into real\-time subtitle text, with optional translation into one or more target languages. RTC room subtitle results can be delivered to the client, the server, or both. WTN subtitle results can be delivered only to the server. You can use the results for scenarios such as live captions, server\-side conversation logging, cross\-language communication, and downstream text analysis.

> **Note**

> For Conversation AI scenarios where subtitles are implemented through [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163), see [Real\-time Subtitles (Dialog Records)](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284).

## Billing

Using real\-time subtitles incurs additional charges. For billing details, see [Billing of Subtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-2608589).

## Before you begin

Before calling the subtitle OpenAPI, complete the following setup:

1. Enable **Realtime subtitle** in the [RTC console](https://console.byteplus.com/rtc/cloudRTC?tab=subtitle).

2. Prepare an HTTP or HTTPS callback endpoint if you want RTC room subtitle results to be returned to your server. A callback endpoint is required for WTN subtitle tasks.

## Start a subtitle task

### RTC room subtitles

Call [StartSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402681) to start a subtitle task.

**Transcription only**

If you want to generate subtitles in the speaker's original language without translation:

* Configure `LanguageConfig.SourceLanguages` for the users whose audio should be processed.

* Do not pass `LanguageConfig.RoomTargetLanguages`, or pass it as an empty array.

* Set `DistributionMode` to `1` for client only, `2` for server only, or `3` for both.

* You can optionally pass `ASRConfig.AdvancedParams`:

   `context` passes hotwords to ASR. `output_zh_variant` controls whether Chinese ASR results are returned in Simplified Chinese or Traditional Chinese. If `output_zh_variant` is not passed, the default output is Simplified Chinese. Set it to `traditional`, `tw`, or `hk` to return Traditional Chinese.

Example:

```JSON
{
  "AppId": "661e****543cf",
  "RoomId": "<YOUR_ROOM_ID>",
  "TaskId": "<YOUR_TASK_ID>",
  "LanguageConfig": {
    "SourceLanguages": [
      {
        "UserId": "<YOUR_USER_ID_1>",
        "LanguageCode": ["zh-CN"]
      },
      {
        "UserId": "<YOUR_USER_ID_2>",
        "LanguageCode": ["en-US"]
      }
    ]
  },
  "DistributionMode": 3,
  "ServerMessage": {
    "Signature": "<YOUR_SIGNATURE>",
    "Url": "https://example.com/subtitle/callback"
  },
  "ReceiverList": [
    "<YOUR_USER_ID_1>",
    "<YOUR_USER_ID_2>"
  ],
  "ASRConfig": {
    "AdvancedParams": {
      "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}",
      "output_zh_variant": "traditional"
    }
  }
}
```

**Translation**

If you want to translate subtitles into one or more target languages:

* Configure `LanguageConfig.SourceLanguages`.

* Pass `LanguageConfig.RoomTargetLanguages` with one or more target languages.

* Set `DistributionMode` to `1` for client only, `2` for server only, or `3` for both.

* You can optionally pass `ASRConfig.AdvancedParams`:

   `context` passes hotwords to ASR. `output_zh_variant` controls whether Chinese ASR results are returned in Simplified Chinese or Traditional Chinese. If `output_zh_variant` is not passed, the default output is Simplified Chinese. Set it to `traditional`, `tw`, or `hk` to return Traditional Chinese.

Example:

```json
{
  "AppId": "661e****543cf",
  "RoomId": "<YOUR_ROOM_ID>",
  "TaskId": "<YOUR_TASK_ID>",
  "LanguageConfig": {
    "SourceLanguages": [
      {
        "UserId": "<YOUR_USER_ID_1>",
        "LanguageCode": ["zh-CN"]
      },
      {
        "UserId": "<YOUR_USER_ID_2>",
        "LanguageCode": ["ja-JP"]
      }
    ],
    "RoomTargetLanguages": ["en"]
  },
  "DistributionMode": 3,
  "ServerMessage": {
    "Signature": "<YOUR_SIGNATURE>",
    "Url": "https://example.com/subtitle/callback"
  },
  "ReceiverList": [
    "<YOUR_USER_ID_1>",
    "<YOUR_USER_ID_2>"
  ],
  "ASRConfig": {
    "AdvancedParams": {
      "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}",
      "output_zh_variant": "traditional"
    }
  }
}
```

### WTN subtitles

Call [StartSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402681) to start a subtitle task.

**Transcription only**

* Configure `LanguageConfig.SourceLanguages[].WtnStreamId` in [StartSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402681).

* If the request contains only `WtnStreamId`, `RoomId` can be omitted.

* Do not pass `LanguageConfig.RoomTargetLanguages`, or pass it as an empty array.

* For WTN subtitles, `DistributionMode` must be set to `2`, so `ServerMessage.Url` and `ServerMessage.Signature` are required.

* You can optionally pass `ASRConfig.AdvancedParams`:

   `context` passes hotwords to ASR. `output_zh_variant` controls whether Chinese ASR results are returned in Simplified Chinese or Traditional Chinese. If `output_zh_variant` is not passed, the default output is Simplified Chinese. Set it to `traditional`, `tw`, or `hk` to return Traditional Chinese.

Example:

```JSON
{
  "AppId": "661e****543cf",
  "TaskId": "<YOUR_TASK_ID>",
  "LanguageConfig": {
    "SourceLanguages": [
      {
        "WtnStreamId": "<YOUR_WTN_STREAM_ID>",
        "LanguageCode": ["zh-CN"]
      }
    ]
  },
  "DistributionMode": 2,
  "ServerMessage": {
    "Signature": "<YOUR_SIGNATURE>",
    "Url": "https://example.com/subtitle/callback"
  },
  "ASRConfig": {
    "AdvancedParams": {
      "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}",
      "output_zh_variant": "traditional"
    }
  }
}
```

**Translation**

* Configure `LanguageConfig.SourceLanguages[].WtnStreamId` in [StartSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402681).

* If the request contains only `WtnStreamId`, `RoomId` can be omitted.

* Pass `LanguageConfig.RoomTargetLanguages` with one or more target languages.

* For WTN subtitles, `DistributionMode` must be set to `2`, so `ServerMessage.Url` and `ServerMessage.Signature` are required.

* You can optionally pass `ASRConfig.AdvancedParams`:

   `context` passes hotwords to ASR. `output_zh_variant` controls whether Chinese ASR results are returned in Simplified Chinese or Traditional Chinese. If `output_zh_variant` is not passed, the default output is Simplified Chinese. Set it to `traditional`, `tw`, or `hk` to return Traditional Chinese.

Example:

```json
{
  "AppId": "661e****543cf",
  "TaskId": "<YOUR_TASK_ID>",
  "LanguageConfig": {
    "SourceLanguages": [
      {
        "WtnStreamId": "<YOUR_WTN_STREAM_ID>",
        "LanguageCode": ["zh-CN"]
      }
    ],
    "RoomTargetLanguages": ["en"]
  },
  "DistributionMode": 2,
  "ServerMessage": {
    "Signature": "<YOUR_SIGNATURE>",
    "Url": "https://example.com/subtitle/callback"
  },
  "ASRConfig": {
    "AdvancedParams": {
      "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}",
      "output_zh_variant": "traditional"
    }
  }
}
```

## Update a subtitle task

Call [UpdateSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402683) to update the language configuration of an ongoing RTC room or WTN subtitle task. For an RTC room subtitle task, you can also update the client\-side receiver list. Use the same `AppId`, `TaskId`, and, when applicable, `RoomId` that were used to start the task.

For a WTN subtitle task:

* Configure `LanguageConfig.SourceLanguages[].WtnStreamId` to update the source language configuration.

* If the task was started with only `WtnStreamId`, `RoomId` can be omitted.

* `ReceiverList` does not take effect because WTN subtitles support only server\-side delivery.

## Subtitle data format

For both client\-side and server\-side delivery, the decoded subtitle `message` uses the same binary format:

|Field |Type |Description |
|---|---|---|
|`magic number` |Binary |Message format identifier. The fixed value is `subc`. |
|`length` |Binary |Length of `subtitle_message` in bytes, stored in big\-endian format. |
|`subtitle_message` |Binary |Subtitle details in JSON format. |

The decoded `subtitle_message` JSON has this structure:

|Field |Type |Description |
|---|---|---|
|`type` |String |Always `subtitle`. |
|`startTime` |Integer |UTC timestamp of the first valid audio frame. |
|`data` |Array |Subtitle entries. |

Each entry in `data` contains:

|Field |Type |Description |
|---|---|---|
|`text` |String |Subtitle text. |
|`language` |String |Subtitle language. |
|`userId` |String |Speaker ID. |
|`sequence` |Integer |Subtitle sequence number. |
|`definite` |Boolean |Whether the subtitle is a finalized sentence fragment. |
|`mode` |Integer |Subtitle type.<br><br><br>* `0` indicates speech recognition text.<br><br>* `1` indicates translated text. |
|`offset` |Integer |Time offset relative to `startTime`, in milliseconds (`ms`). |
|`duration` |Integer |Subtitle duration, in milliseconds (`ms`). |

## Receive and parse subtitles

After the subtitle task starts, subtitle results can be delivered in different ways:

* `DistributionMode=1`: client only

* `DistributionMode=2`: server only

* `DistributionMode=3`: client and server

This page covers the OpenAPI\-based task lifecycle. It does not describe starting or stopping subtitle tasks through the client SDK. However, subtitle results can still be received on the client after the task has been started by OpenAPI.

### Receive and parse subtitles on the server

When `DistributionMode` is `2` or `3`, the platform sends subtitle callback messages to your `ServerMessage.Url` by HTTP(S) POST.

* The request body contains:

   |Field |Type |Description |
   |---|---|---|
   |`message` |String |Base64\-encoded binary subtitle payload |
   |`signature` |String |Callback signature. Compare it with the signature configured in `StartSubtitle` |

* To parse the callback payload:

   1. Verify that the `signature` in the callback body matches the `ServerMessage.Signature` you configured.

   2. Base64\-decode the `message` field.

   3. Read the first 4 bytes as the magic number. The expected value is `subc`.

   4. Read the next 4 bytes as a big\-endian integer representing the subtitle payload length.

   5. Extract the remaining bytes and parse them as a JSON object.

      **Python example**

   ```Python
   import base64
   import json
   import struct
   from flask import Flask, request, jsonify
   
   app = Flask(__name__)
   
   SUBTITLE_HEADER = "subc"
   EXPECTED_SIGNATURE = "replace-with-your-signature"
   
   def parse_subtitle_message(message: str):
       decoded = base64.b64decode(message)
       if len(decoded) < 8:
           raise ValueError("invalid subtitle payload")
   
       magic = decoded[:4].decode()
       if magic != SUBTITLE_HEADER:
           raise ValueError(f"unexpected magic number: {magic}")
   
       length = struct.unpack(">I", decoded[4:8])[0]
       if len(decoded) != length + 8:
           raise ValueError("subtitle payload length mismatch")
   
       payload = json.loads(decoded[8:])
       if payload.get("type") != "subtitle":
           raise ValueError("unexpected subtitle payload type")
       return payload
   
   @app.route("/subtitle/callback", methods=["POST"])
   def handle_subtitle():
       body = request.get_json(force=True)
       if body.get("signature") != EXPECTED_SIGNATURE:
           return jsonify({"error": "unauthorized"}), 403
   
       payload = parse_subtitle_message(body["message"])
       for item in payload.get("data", []):
           print(item["userId"], item["language"], item["text"])
       return jsonify({"status": "ok"}), 200
   ```

### Receive and parse subtitles on the client

When `DistributionMode` is `1` or `3`, the client receives subtitle results through the room binary message callback.

WTN subtitles do not support client\-side delivery. For WTN streams, use `DistributionMode=2` and receive subtitle results on the server.

The callback data contains:

|Field |Type |Description |
|---|---|---|
|`uid` |String |Sender ID |
|`message` |Binary |Subtitle message in binary format. The structure is the same as the decoded server\-side `message`, so no Base64 decoding is needed on the client. |

* If you pass `ReceiverList`, only the specified users can receive client\-side subtitle callbacks.

* On the client, listen to the RTC callback that receives room binary messages, for example `onRoomBinaryMessageReceived`.

**Client parsing example**

The following examples show how to parse subtitle data on the client after `onRoomBinaryMessageReceived` returns a binary message.

**Web**

```TypeScript
type SubtitleItem = {
  text: string;
  language: string;
  userId: string;
  sequence: number;
  definite: boolean;
  mode: number;
  offset: number;
  duration: number;
};

type SubtitlePayload = {
  type: "subtitle";
  startTime: number;
  data: SubtitleItem[];
};

function parseSubtitleMessage(message: ArrayBuffer): SubtitlePayload {
  const bytes = new Uint8Array(message);
  if (bytes.length < 8) {
    throw new Error("invalid subtitle payload");
  }

  const magic = new TextDecoder().decode(bytes.slice(0, 4));
  if (magic !== "subc") {
    throw new Error(`unexpected magic number: ${magic}`);
  }

  const view = new DataView(message);
  const length = view.getUint32(4, false);
  if (bytes.length !== length + 8) {
    throw new Error("subtitle payload length mismatch");
  }

  const payloadText = new TextDecoder().decode(bytes.slice(8));
  const payload = JSON.parse(payloadText) as SubtitlePayload;
  if (payload.type !== "subtitle") {
    throw new Error("unexpected subtitle payload type");
  }
  return payload;
}

engine.on("onRoomBinaryMessageReceived", ({ userId, message }) => {
  const payload = parseSubtitleMessage(message);
  payload.data.forEach((item) => {
    console.log(userId, item.userId, item.language, item.text);
  });
});
```

**Java**

```Java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import java.nio.ByteBuffer;
import java.nio.charset.StandardCharsets;

public class SubtitleParser {
    private static final int HEADER_SIZE = 8;
    private static final int MAGIC_NUMBER = 0x73756263; // "subc"

    public void onRoomBinaryMessageReceived(String uid, ByteBuffer message) {
        try {
            JsonNode payload = parseSubtitleMessage(message);
            for (JsonNode item : payload.get("data")) {
                System.out.println(
                        uid + " " +
                        item.get("userId").asText() + " " +
                        item.get("language").asText() + " " +
                        item.get("text").asText());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private JsonNode parseSubtitleMessage(ByteBuffer message) throws Exception {
        ByteBuffer buffer = message.slice();
        if (buffer.remaining() < HEADER_SIZE) {
            throw new IllegalArgumentException("invalid subtitle payload");
        }

        if (buffer.getInt() != MAGIC_NUMBER) {
            throw new IllegalArgumentException("unexpected magic number");
        }

        int length = buffer.getInt();
        if (buffer.remaining() != length) {
            throw new IllegalArgumentException("subtitle payload length mismatch");
        }

        byte[] body = new byte[length];
        buffer.get(body);
        ObjectMapper objectMapper = new ObjectMapper();
        JsonNode payload = objectMapper.readTree(new String(body, StandardCharsets.UTF_8));
        if (!"subtitle".equals(payload.path("type").asText())) {
            throw new IllegalArgumentException("unexpected subtitle payload type");
        }
        return payload;
    }
}
```

**C++**

```C++
#include <cstdint>
#include <iostream>
#include <stdexcept>
#include <string>
#include <vector>
#include <nlohmann/json.hpp>

struct SubtitleItem {
    std::string text;
    std::string language;
    std::string userId;
    int sequence;
    bool definite;
    int mode;
    int64_t offset;
    int64_t duration;
};

nlohmann::json ParseSubtitleMessage(const uint8_t* message, int size) {
    constexpr int kHeaderSize = 8;
    constexpr uint32_t kMagicNumber = 0x73756263U;  // "subc"

    if (size < kHeaderSize) {
        throw std::runtime_error("invalid subtitle payload");
    }

    uint32_t magic = (static_cast<uint32_t>(message[0]) << 24) |
                     (static_cast<uint32_t>(message[1]) << 16) |
                     (static_cast<uint32_t>(message[2]) << 8) |
                     static_cast<uint32_t>(message[3]);
    if (magic != kMagicNumber) {
        throw std::runtime_error("unexpected magic number");
    }

    uint32_t length = (static_cast<uint32_t>(message[4]) << 24) |
                      (static_cast<uint32_t>(message[5]) << 16) |
                      (static_cast<uint32_t>(message[6]) << 8) |
                      static_cast<uint32_t>(message[7]);
    if (size - kHeaderSize != static_cast<int>(length)) {
        throw std::runtime_error("subtitle payload length mismatch");
    }

    std::string payloadText(reinterpret_cast<const char*>(message + kHeaderSize), length);
    auto payload = nlohmann::json::parse(payloadText);
    if (payload.value("type", "") != "subtitle") {
        throw std::runtime_error("unexpected subtitle payload type");
    }
    return payload;
}

void onRoomBinaryMessageReceived(const char* uid, int size, const uint8_t* message) {
    try {
        auto payload = ParseSubtitleMessage(message, size);
        for (const auto& item : payload["data"]) {
            std::cout << uid << " "
                      << item["userId"].get<std::string>() << " "
                      << item["language"].get<std::string>() << " "
                      << item["text"].get<std::string>() << std::endl;
        }
    } catch (const std::exception& e) {
        std::cerr << e.what() << std::endl;
    }
}
```

**Objective-C**

```Objective-C
@interface SubtitleParser : NSObject
- (NSDictionary *)parseSubtitleMessage:(NSData *)message error:(NSError **)error;
@end

@implementation SubtitleParser

- (NSDictionary *)parseSubtitleMessage:(NSData *)message error:(NSError **)error {
    const NSUInteger kHeaderSize = 8;
    const uint32_t kMagicNumber = 0x73756263; // "subc"

    if (message.length < kHeaderSize) {
        if (error) {
            *error = [NSError errorWithDomain:@"SubtitleParser"
                                         code:-1
                                     userInfo:@{NSLocalizedDescriptionKey: @"invalid subtitle payload"}];
        }
        return nil;
    }

    const uint8_t *bytes = message.bytes;
    uint32_t magic = (bytes[0] << 24) | (bytes[1] << 16) | (bytes[2] << 8) | bytes[3];
    if (magic != kMagicNumber) {
        if (error) {
            *error = [NSError errorWithDomain:@"SubtitleParser"
                                         code:-2
                                     userInfo:@{NSLocalizedDescriptionKey: @"unexpected magic number"}];
        }
        return nil;
    }

    uint32_t length = (bytes[4] << 24) | (bytes[5] << 16) | (bytes[6] << 8) | bytes[7];
    if (message.length - kHeaderSize != length) {
        if (error) {
            *error = [NSError errorWithDomain:@"SubtitleParser"
                                         code:-3
                                     userInfo:@{NSLocalizedDescriptionKey: @"subtitle payload length mismatch"}];
        }
        return nil;
    }

    NSData *payloadData = [message subdataWithRange:NSMakeRange(kHeaderSize, length)];
    NSDictionary *payload = [NSJSONSerialization JSONObjectWithData:payloadData options:0 error:error];
    if (![[payload objectForKey:@"type"] isEqualToString:@"subtitle"]) {
        if (error) {
            *error = [NSError errorWithDomain:@"SubtitleParser"
                                         code:-4
                                     userInfo:@{NSLocalizedDescriptionKey: @"unexpected subtitle payload type"}];
        }
        return nil;
    }
    return payload;
}

@end

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom
onRoomBinaryMessageReceived:(NSString *)uid
         message:(NSData *)message {
    NSError *error = nil;
    NSDictionary *payload = [[[SubtitleParser alloc] init] parseSubtitleMessage:message error:&error];
    if (error) {
        NSLog(@"%@", error.localizedDescription);
        return;
    }

    for (NSDictionary *item in payload[@"data"]) {
        NSLog(@"%@ %@ %@ %@", uid, item[@"userId"], item[@"language"], item[@"text"]);
    }
}
```

## Handle subtitle results

If you process subtitle results on the server, use these rules:

* If `definite` is `false`, treat the message as an incremental update and use a later `sequence` value to overwrite earlier partial text.

* If `definite` is `true`, treat the message as a finalized sentence fragment.

* Use `mode` to distinguish result types: `0` indicates speech recognition text, while `1` indicates translated text.

* If you need durable storage, store subtitle content only when `definite` is `true`.

## Stop the subtitle task

To stop subtitle generation for an RTC room or WTN stream, call [StopSubtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-1402682). If the task was started with only `WtnStreamId`, you can omit `RoomId` when stopping it.

The task may also stop automatically if the system detects no audio upload from the source for 3 consecutive minutes.
