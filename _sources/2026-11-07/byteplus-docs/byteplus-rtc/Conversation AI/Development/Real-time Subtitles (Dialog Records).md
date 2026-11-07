---
title: "Real-time Subtitles (Dialog Records)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1337284"
---

During AI conversations, the system automatically generates text for both the user and the AI. You can retrieve this data in real\-time via the client or server for UI display, storage, or to trigger business logic based on dialogue status.


* **Real\-time Subtitle Display**: Convert user and AI speech into text in real\-time and display it on the application interface.

* **Business Analysis & Storage**: Record and store dialogue text for subsequent data analysis, quality monitoring, or model optimization.


<span id="b30890d9"></span>
## Subtitle Modes

We offer four subtitle modes to meet different business requirements. You can select the mode via the `SubtitleConfig.SubtitleMode` parameter when calling the `StartVoiceChat` API. Different modes determine the source of the subtitles, content formatting, synchronization with audio, and reception speed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">When using <strong>Digital Human Services</strong>, <code>SubtitleMode</code> must be set to <code>1</code> (Fast Subtitles).</div>


* <div data-tips="true" data-tips-type="warning">The reception speeds of the modes are ranked as follows: 3 \> 1 \> 0 ≈ 2.</div>



&nbsp;


|Subtitle Type |`SubtitleMode` |Description |
|---|---|---|
|**Timestamp\-Aligned** |0 |Sourced from TTS. Text is aligned with the AI's actual audio playback at the sentence level. Generation is slightly slower; some special symbols might be escaped. Supports Pause and Resume.<br><br>**Note**: This mode is unavailable when `TTSConfig.AutoActive` is false. |
|**Fast Subtitles** |1 |Sourced directly from the LLM response. Returns segments or full sentences immediately. Faster generation and retains all original text (e.g., emojis), but is not timestamp\-aligned with audio.<br><br>**Note**: This mode is unavailable when `TTSConfig.AutoActive` is false. |
|**Audio\-frame Aligned** |2 |Sourced from TTS. Precisely aligns text with audio for karaoke\-style word\-by\-word highlighting. Better resistance to network jitter. Supports Pause and Resume.<br><br>**Note**: Alignment info is embedded in the audio frame's `extraInfo`. |
|**LLM Raw** **Subtitles** |3 |Subtitles originate from the LLM's raw output without any content processing, fully preserving formats such as line breaks. Suitable for scenarios requiring content fidelity and rapid subtitle callbacks. |


<span id="eead8c93"></span>
## Obtaining Subtitle Data

You can receive subtitle data via the client\-side SDK or server\-side callbacks. The data source and timing vary by method. See [Subtitle Source and Return Methods](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#dc557ae7) for details.

<span id="193be6ae"></span>
### Method 1: Client\-side Integration

Applicable to scenarios where subtitles need to be displayed in real time on the terminal interface. Data is obtained through client SDK callbacks.

<span id="01c636c6"></span>
#### Step 1: Enable Configuration

Add `Config.SubtitleConfig` when calling `StartVoiceChat`:


* `DisableRTSSubtitle`: Set to false to enable the client\-side subtitle callback.

* `SubtitleMode`: Choose as needed, refer to [Subtitle Modes](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#b30890d9).


```JSON
// Only subtitle configuration is displayed
"SubtitleConfig": {
  "DisableRTSSubtitle": false, // Enable client-side callbacks
  "SubtitleMode": 0 
}
```


<span id="95f0d412"></span>
#### Step 2: Receive and Parse Subtitles


1. **Listen for callbacks**: Receive subtitle messages (in binary format) via ByteRTC SDK's [onRoomBinaryMessageReceived](https://docs.byteplus.com/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived-2) (use `on_message_received` in embedded hardware scenarios).

2. **Parse data**: Subtitles are sent to the client as a binary message (identified by the magic number subv) via callbacks.

   * `message` format: See [Subtitle Data Format](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#e0f57284).

   * `message` parsing example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example demonstrates the full parsing logic for subtitle data. In actual development, please extract and process relevant fields based on your specific use case (e.g., simple text display vs. audio\-text synchronization with highlighting).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For audio\-frame\-aligned subtitles, you need to parse and store information such as <code>roundId</code>, <code>firstCharPos</code>, and <code>lastCharPos</code> to serve as a subtitle library for subsequent audio frame matching.   </div>
   

   
   <Tabs>
   <Tab zoneid="URW8OEbTcb" title="C++">
   <TabTitle>C++</TabTitle>
   
   ```C++
   // Define structure
   struct SubtitleMsgData {
       bool definite;
       std::string language;
       bool paragraph;
       int sequence;
       std::string text;
       std::string userId;
       int roundId;      
       int firstCharPos;
       int lastCharPos;
   };
   
   // Callbacks
   void onRoomBinaryMessageReceived(const char* uid, int size, const uint8_t* message) {
       std::string subtitles;
       bool ret = Unpack(message, size, subtitles);
       if(ret) {
           ParseData(subtitles);
       }
   }
   
   // Unpacking validation
   bool Unpack(const uint8_t *message, int size, std::string& subtitles) {
       int kSubtitleHeaderSize = 8;
       if(size < kSubtitleHeaderSize) { 
           return false;
       }
       // magic number "subv"
       if(static_cast<uint32_t>((static_cast<uint32_t>(message[0]) << 24) 
              | (static_cast<uint32_t>(message[1]) << 16) 
              | (static_cast<uint32_t>(message[2]) << 8) 
              | static_cast<uint32_t>(message[3])) != 0x73756276U) {
           return false;
       }
       
       uint32_t length = static_cast<uint32_t>((static_cast<uint32_t>(message[4]) << 24) 
              | (static_cast<uint32_t>(message[5]) << 16) 
              | (static_cast<uint32_t>(message[6]) << 8) 
              | static_cast<uint32_t>(message[7]));
              
       if(size - kSubtitleHeaderSize != length) {
           return false;
       }
   
       if(length) {
           subtitles.assign((char*)message + kSubtitleHeaderSize, length);
       } else {
           subtitles = "";
       }
       return true;
   }
   
   // Parse
   void ParseData(const std::string& msg) {
       // Parse JSON string
       nlohmann::json json_data = nlohmann::json::parse(msg);
       // Store parsed data
       std::vector<SubtitleMsgData> subtitles;
       // Iterate through JSON data and populate structure
       for (const auto& item : json_data["data"]) {
           SubtitleMsgData subData;
           subData.definite = item["definite"];
           subData.language = item["language"];
           subData.paragraph = item["paragraph"];
           subData.sequence = item["sequence"];
           subData.text = item["text"];
           subData.userId = item["userId"];
           subData.roundId = item["roundId"];
           subData.firstCharPos = item["firstCharPos"];
           subData.lastCharPos = item["lastCharPos"];
           subtitles.push_back(subData);
       }
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="MfaHEyFfPg" title="Java">
   <TabTitle>Java</TabTitle>
   
   ```Java
   // Data format
   public class SubtitleMsgData {
       public boolean definite;
       public String language;
       public boolean paragraph;
       public int sequence;
       public String text;
       public String userId;
       public int roundId;
       public int firstCharPos;
       public int lastCharPos;
   
       @Override
       public String toString() {
           return "SubtitleMsgData{" +
                   "definite=" + definite +
                   ", language='" + language + '\\'' +
                   ", paragraph=" + paragraph +
                   ", sequence=" + sequence +
                   ", text='" + text + '\\'' +
                   ", userId='" + userId + '\\'' +
                   ", roundId=" + roundId +
                   ", firstCharPos=" + firstCharPos +
                   ", lastCharPos=" + lastCharPos +
                   '}';
       }
   }
   
   // Callbacks
   public void onRoomBinaryMessageReceived(String uid, ByteBuffer buffer) {
       StringBuilder subtitles = new StringBuilder();
       boolean ret = unpack(buffer, subtitles); 
       if (ret) {
           parseData(subtitles.toString());
       }
   }
   
   // Unpacking validation
   public static boolean unpack(ByteBuffer message, StringBuilder subtitles) {
       final int kSubtitleHeaderSize = 8;
       if (message.remaining() < kSubtitleHeaderSize) {
           return false;
       }
   
       // Magic number "subv"
       int magicNumber = (message.get() << 24) | (message.get() << 16) | (message.get() << 8) | (message.get());
       if (magicNumber != 0x73756276) {
           return false;
       }
   
       int length = message.getInt();
   
       if (message.remaining() != length) {
           return false;
       }
   
       // Read subtitle content
       byte[] subtitleBytes = new byte[length];
       message.get(subtitleBytes);
       subtitles.append(new String(subtitleBytes, StandardCharsets.UTF_8));
   
       return true;
   }
   
   // Parse subtitle message
   public static void parseData(String msg) {
       try {
           // Parse JSON string
           ObjectMapper objectMapper = new ObjectMapper();
           JsonNode jsonData = objectMapper.readTree(msg);
   
           // Store parsed data
           List<SubtitleMsgData> subtitles = new ArrayList<>();
   
           // Iterate through JSON data and populate structure
           for (JsonNode item : jsonData.get("data")) {
               SubtitleMsgData subData = new SubtitleMsgData();
               subData.definite = item.get("definite").asBoolean();
               subData.language = item.get("language").asText();
               subData.paragraph = item.get("paragraph").asBoolean();
               subData.sequence = item.get("sequence").asInt();
               subData.text = item.get("text").asText();
               subData.userId = item.get("userId").asText();
               subData.roundId = item.get("roundId").asInt();
               subData.firstCharPos = item.get("firstCharPos").asInt();
               subData.lastCharPos = item.get("lastCharPos").asInt();
               subtitles.add(subData);
           }
       } catch (Exception e) {
           e.printStackTrace();
       }
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="zhY46GvT2v" title="Objective-C">
   <TabTitle>Objective-C</TabTitle>
   
   ```Objective-C
   // Data format
   @interface SubtitleMsgData : NSObject
   
   @property (nonatomic, assign) BOOL definite;
   @property (nonatomic, copy) NSString *language;
   @property (nonatomic, assign) BOOL paragraph;
   @property (nonatomic, assign) NSInteger sequence;
   @property (nonatomic, copy) NSString *text;
   @property (nonatomic, copy) NSString *userId;
   @property (nonatomic, assign) NSInteger roundId;
   @property (nonatomic, assign) NSInteger firstCharPos;
   @property (nonatomic, assign) NSInteger lastCharPos;
   
   @end
   
   @implementation SubtitleMsgData
   @end
   
   // Callbacks
   - (void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSString *_Nonnull)uid message:(NSData *_Nonnull)message {
       NSString *subtitles = unpack(message);
       if (subtitles) {
           parseData(subtitles);
       }
   }
   
   
   // Big-endian conversion
   uint32_t swapUInt32(uint32_t value) {
       return ((value & 0x000000FF) << 24) |
              ((value & 0x0000FF00) << 8) |
              ((value & 0x00FF0000) >> 8) |
              ((value & 0xFF000000) >> 24);
   }
   
   // Unpacking validation
   NSString *unpack(NSData *data) {
       const int kSubtitleHeaderSize = 8;
       NSUInteger size = data.length;
       if (size < kSubtitleHeaderSize) {
           return nil;
       }
       const uint8_t *message = data.bytes;
       // Check magic number "subv"
       uint32_t magic = (message[0] << 24) | (message[1] << 16) | (message[2] << 8) | message[3];
       if (magic != 0x73756276) {
           return nil;
       }
       
       // Get length
       uint32_t length = (message[4] << 24) | (message[5] << 16) | (message[6] << 8) | message[7];
       if (size - kSubtitleHeaderSize != length) {
           return nil;
       }
       
       // Get subtitles
       NSString *subtitles = nil;
       if (length > 0) {
           subtitles = [[NSString alloc] initWithBytes:message + kSubtitleHeaderSize length:length encoding:NSUTF8StringEncoding];
       } else {
           subtitles = @"";
       }
       
       return subtitles;
   }
   // Parse
   void parseData(NSString *msg) {
       NSError *error = nil;
       NSDictionary *json_data = [NSJSONSerialization JSONObjectWithData:[msg dataUsingEncoding:NSUTF8StringEncoding] options:0 error:&error];
       
       if (error) {
           NSLog(@"JSON Parse Error: %@", error);
           return;
       }
       
       NSMutableArray<SubtitleMsgData *> *subtitles = [NSMutableArray array];
       
       for (NSDictionary *item in json_data[@"data"]) {
           SubtitleMsgData *subData = [[SubtitleMsgData alloc] init];
           subData.definite = [item[@"definite"] boolValue];
           subData.language = item[@"language"];
           subData.paragraph = [item[@"paragraph"] boolValue];
           subData.sequence = [item[@"sequence"] integerValue];
           subData.text = item[@"text"];
           subData.userId = item[@"userId"];
           subData.roundId = [item[@"roundId"] integerValue];
           subData.firstCharPos = [item[@"firstCharPos"] integerValue];
           subData.lastCharPos = [item[@"lastCharPos"] integerValue];
           
           [subtitles addObject:subData];
       }
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="9921063d"></span>
### Method 2: Server\-side Integration

Applicable to scenarios where dialog records, storage, and analysis are required on the server side. Data is pushed to the business server via HTTP(S) POST requests.

<span id="268530ce"></span>
#### Step 1: Enable Configuration

Call `StartVoiceChat` when starting AI, and add the `SubtitleConfig` configuration in `Config`:

&nbsp;


|Parameters |Note |
|---|---|
|`ServerMessageUrl` |Your public backend URL to receive subtitle messages. |
|`ServerMessageSignature` |Custom authentication key. This string will be returned as\-is in callback requests and is used to verify the legitimacy of the request. |
|`SubtitleMode` |Choose as needed, refer to [Subtitle Modes](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#b30890d9). |


```JSON
// Only subtitle configuration is shown
"SubtitleConfig": {
  "ServerMessageUrl": "https://example-domain.com/vertc/subtitle",
  "ServerMessageSignature": "b46ab****ad6a",
  "SubtitleMode": 0 // 0: Aligns with audio timestamps
}
```


<span id="ee06d814"></span>
#### Step 2: Receive and Parse Subtitles

Subtitle messages are sent to the URL you specify via HTTP(S) POST requests.


* Callback content:

&nbsp;

   
   |Parameter |Type |Description |
   |---|---|---|
   |message |String |Subtitle data (Base64\-encoded binary message), see format in [Subtitle Data Format](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#e0f57284). |
   |signature |String |Authentication signature. Can be compared with the value of the `ServerMessageSignature` field passed in the `StartVoiceChat` interface for authentication. |
   

* `message` parsing example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example demonstrates the full parsing logic for subtitle data. In actual development, please extract and process relevant fields based on your specific use case (e.g., simple text display vs. audio\-text synchronization with highlighting).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For audio\-frame\-aligned subtitles, you need to parse and store information such as <code>roundId</code>, <code>firstCharPos</code>, and <code>lastCharPos</code> to serve as a subtitle library for subsequent audio frame matching.   </div>
   

   ```Go
   const (
       subtitleHeader   = "subv"
       exampleSignature = "example_signature"
   )
   
   type RtsMessage struct {
       Message   string `json:"message"`
       Signature string `json:"signature"`
   }
   
   type Subv struct {
       Type string `json:"type"`
       Data []Data `json:"data"`
   }
   
   type Data struct {
       Definite  bool   `json:"definite"`
       Paragraph bool   `json:"paragraph"`
       Language  string `json:"language"`
       Sequence  int    `json:"sequence"`
       Text      string `json:"text"`
       UserID    string `json:"userId"`
   }
   
   func HandleSubtitle(c *gin.Context) {
       msg := &RtsMessage{}
       if err := c.BindJSON(&msg); err != nil {
          fmt.Printf("BindJson failed,err:%v\n", err)
          return
       }
       if msg.Signature != exampleSignature {
          fmt.Printf("Signature not match\n")
          return
       }
   
       subv, err := Unpack(msg.Message)
       if err != nil {
          fmt.Printf("Unpack failed,err:%v\n", err)
          return
       }
   
       fmt.Println(subv)
   
       // Business logic
   
       c.String(200, "ok")
   }
   
   func Unpack(msg string) (*Subv, error) {
       data, err := base64.StdEncoding.DecodeString(msg)
       if err != nil {
          return nil, fmt.Errorf("DecodeString failed,err:%v", err)
       }
       if len(data) < 8 {
          return nil, fmt.Errorf("Data invalid")
       }
       dataHeader := string(data[:4])
       if dataHeader != subtitleHeader {
          return nil, fmt.Errorf("Header not match")
       }
       dataSize := binary.BigEndian.Uint32(data[4:8])
       if dataSize+8 != uint32(len(data)) {
          return nil, fmt.Errorf("Size not match")
       }
   
       subData := data[8:]
       subv := &Subv{}
       err = json.Unmarshal(subData, subv)
       if err != nil {
          return nil, fmt.Errorf("Unmarshal failed,err:%v\n", err)
       }
       return subv, nil
   }
   
   func main() {
       r := gin.Default()
       r.POST("/example_domain/vertc/subtitle", HandleSubtitle)
       r.Run()
   }
   ```
   


<span id="7e763d9c"></span>
## Advanced Usage

<span id="ee643049"></span>
### Real\-time UI Display

&nbsp;


|Field combination status |UI processing |
|---|---|
|`paragraph: false`,`definite: false` |Use the subtitle with the higher sequence number to overwrite the one with the lower sequence number. |
|`paragraph: false`,`definite: true` |Start a new sentence and overwrite the previous sentence. |
|`paragraph: true` |If you do not stop processing subtitles after receiving a message with `paragraph: true`, you may display the final sentence repeatedly. |


<span id="4dd73a06"></span>
### Store Subtitles

Store only when `paragraph: true` is parsed, to reduce the amount of stored data and ensure that the saved subtitles are complete.

<span id="efe7ef19"></span>
### Handle Subtitles for Multi\-turn Dialogues

Use the `roundId` field to group subtitles, accurately distinguishing and associating subtitles for each round of dialogue in complex conversation flows.

<span id="8c3d69df"></span>
### Audio\-Subtitle Synchronization (Audio\-frame Aligned)

Standard subtitle delivery over separate channels can lead to desync due to network jitter. `SubtitleMode: 2` solves this by embedding character indices directly into audio frames.


1. **Retrieve and cache subtitles** (can be either client\-side or server\-side). For specific operations, see [Obtaining Subtitle Data](https://docs.byteplus.com/docs/byteplus-rtc/docs-1337284#eead8c93).

   * `SubtitleMode`: Set to `2`.

   * When parsing subtitles, you need to store the text along with `roundId`, `firstCharPos`, `lastCharPos`, etc., as a "subtitle library" for subsequent audio frame matching.

2. **Receive Indexed Audio Frames**.

   1. **Register Observer**: Call `registerAudioFrameObserver` to register an implementation of `IAudioFrameObserver`.

   2. **Enable Callback**: Call `enableAudioFrameCallback` to enable remote user audio frame callbacks.

   3. **Parse ** **`extraInfo`**: In the `onRemoteUserAudioFrame` callback, obtain `extraInfo` from the `IAudioFrame` object. `extraInfo` is 8\-byte data, where the first 4 bytes are the `round_id` and the last 4 bytes are the `subtitle_index`, both in big\-endian order. The `extraInfo` data format is as follows:

   ```Plain
   0                   1                   2                   3
          0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        |                     round_id (uint32_t)                       |
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        |                     subtitle_index (uint32_t)                 |
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   ```
   

   **C++ Example**:

   ```C++
   class MyAudioFrameObserver : public bytertc::IAudioFrameObserver {
   public:
       void onRemoteUserAudioFrame(
               const char* stream_id, 
               const bytertc::StreamInfo& stream_info, 
               const bytertc::IAudioFrame& audio_frame) override {
   
           // Check if extraInfo is 8 bytes
           if (audio_frame.extraInfoSize() == 8) {
               const uint8_t* info = audio_frame.extraInfo();
   
               // Parse round_id (Big-endian)
               uint32_t round_id = (static_cast<uint32_t>(info[0]) << 24) |
                                   (static_cast<uint32_t>(info[1]) << 16) |
                                   (static_cast<uint32_t>(info[2]) << 8)  |
                                   (static_cast<uint32_t>(info[3]));
   
               // Parse subtitle_index (Big-endian)
               uint32_t subtitle_index = (static_cast<uint32_t>(info[4]) << 24) |
                                         (static_cast<uint32_t>(info[5]) << 16) |
                                         (static_cast<uint32_t>(info[6]) << 8)  |
                                         (static_cast<uint32_t>(info[7]));
   
               // Call rendering logic
               renderSubtitleHighlight(round_id, subtitle_index);
           }
       }
       // ... other callback methods
   };
   
   // Register during initialization
   MyAudioFrameObserver g_audio_observer;
   rtc_engine->registerAudioFrameObserver(&g_audio_observer);
   rtc_engine->enableAudioFrameCallback(bytertc::AudioFrameCallbackMethod::kRemoteUser, bytertc::AudioFormat());
   ```
   

3. **Implement Subtitle Rendering and Audio Frame Alignment**.

   After obtaining `round_id` and `subtitle_index` in the `onRemoteUserAudioFrame` callback, you need to implement the specific UI rendering logic.

   **Common Tagging Rules for Subtitle Indices**:

   * Subtitle indices are tagged based on **absolute characters**, including spaces, punctuation, etc., which each occupy one index. The index is tagged at the dimension of the current dialogue turn.

   * Indices may experience "jumps" (e.g., during English liaisons) and are not necessarily absolutely continuous.

   * When processing Chinese characters, note that one Chinese character may occupy multiple bytes under UTF\-8 encoding.

      **Examples**:

   * Chinese Example: （开心）今天天气不错！

&nbsp;

      
      |Extrainfo Subtitle Index |0 |1 |2 |3 |4 |5 |6 |7 |8 |9 |10 |
      |---|---|---|---|---|---|---|---|---|---|---|---|
      |Subtitle |（ |开 |心 |） |今 |天 |天 |气 |不 |错 |！ |
      

   * English Example: Hello! I'm Job.

&nbsp;

      
      |Extrainfo Subtitle Index |0 |1 |2 |3 |4 |5 |6 |7 |8 |9 |10 |
      |---|---|---|---|---|---|---|---|---|---|---|---|
      |Subtitle |H |e |l |l |o |! | |I |' |m | |
      

   **UI Rendering Logic Reference**:

   Find the corresponding subtitle text from your cached "subtitle library" based on `round_id`, then use `subtitle_index` to locate the character that needs to be highlighted. Finally, highlight the corresponding character on the UI based on its relative position.

   **Code Example**:

   The following C++ example code is for logic illustration only; you need to adjust it based on actual conditions (e.g., UI framework used, thread safety).

   ```C++
   // Helper function: Split UTF-8 string into a list of logic characters (each element is 1 logic character)
   std::vector<std::string> split_utf8_to_chars(const std::string& utf8_str) {
       std::vector<std::string> chars;
       size_t i = 0;
       while (i < utf8_str.size()) {
           // Determine the byte length of the UTF-8 character
           unsigned char c = static_cast<unsigned char>(utf8_str[i]);
           int len = 0;
           if (c < 0x80) {
               len = 1;  // ASCII character (English/Punctuation): 1 byte
           } else if (c < 0xE0) {
               len = 2;  // 2-byte UTF-8
           } else if (c < 0xF0) {
               len = 3;  // 3-byte UTF-8 (Core Chinese)
           } else {
               len = 4;  // 4-byte UTF-8
           }
   
           /// Extract current logic character (avoid out of bounds)
           size_t end = std::min(i + len, utf8_str.size());
           chars.push_back(utf8_str.substr(i, end - i));
           i = end;
       }
       return chars;
   }
   
   void print_sub_title_char(std::string text, int size, int char_pos){
       // 1. Validity check: handle negative parameters
       if (char_pos <= 0 || size <= 0) {
           // std::cout << "" << std::endl;  // No character to print
           return;
       }
   
       // 2. Split UTF-8 string into a list of logic characters (each character occupies 1 pos)
       std::vector<std::string> logic_chars = split_utf8_to_chars(text);
   
       // 3. Determine the number of valid logic characters before char_pos (pos starts from 1, corresponding to list indices 0~char_pos-1)
       int available_chars = std::min(char_pos, static_cast<int>(logic_chars.size()));
       if (available_chars <= 0) {
      
           return;
       }
   
       // 4. Extract at most 'size' characters
       int take_chars = std::min(size, available_chars);
       std::string result;
       for (int i = available_chars - take_chars; i < available_chars; ++i) {
           result += logic_chars[i];
       }
   
       printf("print_sub_title_char %s \n", result.c_str());
   }
   
   void print_sub_title(int char_pos, int round_id){
       for (auto it = g_subTitle.begin(); it != g_subTitle.end(); ++it) {
           if (it->round_id == round_id) {
               if(char_pos >= it->firstCharPos && char_pos <= it->lastCharPos + 1) {
                   print_sub_title_char(it->text, 8, char_pos - it->firstCharPos);
                   if(char_pos == it->lastCharPos) {
                       it = g_subTitle.erase(it);
                   }
                   break;
               }
               else {
                   // printf("current sub title: null char_pos %d  it->firstCharPos %d it->lastCharPos %d \n",char_pos,it->firstCharPos,it->lastCharPos);
               }
           }
       }
       
       // Note: No ++it here
       for (auto it = g_subTitle.begin(); it != g_subTitle.end();) {
           if (it->round_id < round_id) {
               // Remove element and update iterator with return value (avoid invalidation)
               it = g_subTitle.erase(it);
           } else {
               // If not removed, move iterator normally
               ++it;
           }
       }
       
       if(round_id == -1) {
           printf("current sub title: null \n");
       }
   }
   ```
   

4.  **(Optional) Implement Synchronized Audio and Subtitle Pause and Resume**.

   After implementing audio\-text synchronized rendering, you can simultaneously pause or resume audio playback and subtitle rendering by sending instructions via the server\-side API or client. For example, after the user presses the pause button, the AI stops playing, and the subtitle also stops rendering simultaneously; when playback resumes, the audio and subtitles will continue from where they were paused. For command sending methods, please see [Pause or Resume AI Playback](https://docs.byteplus.com/docs/byteplus-rtc/docs-2389913).


<span id="20792513"></span>
## Appendix

<span id="e0f57284"></span>
### Subtitle Data Format

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4680825ac48a324a261a993f0e95433.jpg) </span>

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|magic number |binary |Message identifier. A fixed value of `subv`, which indicates subtitle data. |
|length |binary |Subtitle message length, in bytes, stored in big\-endian order. |
|subtitle_message |binary |JSON string of subtitle content, UTF\-8 encoded. |


subtitle_message

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|type |String |Message type, a fixed value of `subtitle`, which indicates that the message is a subtitle. |
|data |object |Detailed subtitle information, including subtitle text, language, speaker ID, and other specific information. |


data

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|text |String |Subtitle text content. |
|language |String |Subtitle language. |
|userId |String |Subtitle source ID. If the subtitle source is a real user, this value is the real user's UserId. If the source is AI, this value is the AI's UserId. |
|sequence |Int |Subtitle sequence number, incremented within a single conversation round. |
|definite |Boolean |Whether the subtitle is a complete clause.<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|paragraph |Boolean |Whether the subtitle is a complete sentence.<br><br><br>* `true`: Yes. Indicates the speaker's complete utterance for this round has ended.<br><br>* `false`: No. |
|roundId |Int |Conversation round number. |
|firstCharPos |Int |The starting character index of this `text` fragment in the full dialogue. |
|lastCharPos |Int |The ending character index of this `text` fragment in the full dialogue. |
|customInfo |Object |Custom business information. When `AdvanceConfig.CustomInfo` is passed through the server\-side `UpdateVoiceChat` or the client\-side `sendUserBinaryMessage` `ExternalTextToSpeech` command, this object is forwarded as\-is with the subtitle for the corresponding `roundId`. RTC does not parse the keys or values in the object.<br><br>`customInfo` is supported when `SubtitleMode` is `0`, `1`, or `3`. |


Subtitle response examples:


<Tabs>
<Tab zoneid="E1205bQ4Ym" title="Subtitles with custom business information">
<TabTitle>Subtitles with custom business information</TabTitle>

The following example shows two subtitle callbacks generated after the same long text is split. Although `paragraph` is `true` in both subtitle segments, `customInfo.finish` is `false` in the first segment, so the client should keep waiting. In the second segment, it is `true`, so the client can mark the entire text as finished.

```JSON
// Segment 1: The current external text input has ended, but the full long text has not yet finished
{
    "type": "subtitle",
    "data": [
        {
            "text": "Start by visiting the city museum and the riverside park.",
            "language": "zh-CN",
            "userId": "bot_id_123",
            "sequence": 0,
            "definite": true,
            "paragraph": true,
            "roundId": 11,
            "customInfo": {
                "finish": false
            }
        }
    ]
}

// Segment 2: The current external text input has ended, and the full long text has been fully delivered
{
    "type": "subtitle",
    "data": [
        {
            "text": "On the final day, explore the botanical garden and enjoy your trip.",
            "language": "zh-CN",
            "userId": "bot_id_123",
            "sequence": 1,
            "definite": true,
            "paragraph": true,
            "roundId": 11,
            "customInfo": {
                "finish": true
            }
        }
    ]
}
```



</Tab>
<Tab zoneid="wWHzgo3Siy" title="Audio-frame-aligned subtitle examples">
<TabTitle>Audio-frame-aligned subtitle examples</TabTitle>

The following example shows the contents of two consecutively received audio\-frame\-aligned subtitle messages. It illustrates how the `sequence`, `definite`, and `text` fields change.

```JSON
// message1: Subtitle for the first round of conversation
{
    "type": "subtitle",
    "data": [
        {
            "text": "Good morning, everyone, and welcome to today’s session.",
            "language": "zh-CN",
            "userId": "bot_id_123",
            "sequence": 0,
            "definite": true,
            "paragraph": true,
            "roundId": 1,
            "firstCharPos": 0,
            "lastCharPos": 11
        }
    ]
}

// message2: Subtitle for the second round of conversation
{
    "type": "subtitle",
    "data": [
        {
            "text": "Let’s begin with a quick overview before we move on.",
            "language": "zh-CN",
            "userId": "bot_id_123",
            "sequence": 0,
            "definite": true,
            "paragraph": true,
            "roundId": 2,
            "firstCharPos": 12,
            "lastCharPos": 23
        }
    ]
}
```



</Tab>
</Tabs>


<span id="dc557ae7"></span>
### Subtitle Source and Return Methods

The source and return methods of subtitles vary depending on the reception method (client callback vs. server callback) and the party involved (real user vs. AI).

&nbsp;


|Receiving method |User subtitles |AI subtitles |
|---|---|---|
|Client receives |**Subtitle source**: ASR module speech recognition content<br><br>**Return method**: Streamed return, each new subtitle contains the cumulative text of the utterance.<br><br>> For example, if the user says, "Hello, query the weather in Shanghai," you will receive a sequence of messages like `Hello,` `Hello, query` `Hello, query the weather in Shanghai`.<br><br><br>**Subtitle status**:<br><br><br>* **During speech**:<br><br>   * `definite`: Always `false`.<br><br>   * `paragraph`: Always `false`.<br><br>* **At the end of speech**:<br><br>   * `definite`: Always `true`.<br><br>   * `paragraph`: Always `true`. |**Subtitle source**: LLM text or TTS reading content (determined by `SubtitleMode`)<br><br>**Return method**: Streaming; returned only after a segment is complete. New segments do not contain previous ones.<br><br>> Example: If the AI says, "The weather is hot, the temperature is 30 degrees Celsius," you will first receive the clause: `The weather is hot,` and then `the temperature is 30 degrees Celsius.`.<br><br><br>**Subtitle status**:<br><br><br>* **During speech**:<br><br>   * `definite`: May be `false` (clause not finished) or `true` (clause finished, but the entire sentence is not complete).<br><br>   * `paragraph`: Always `false`, indicating the entire sentence is not finished.<br><br>* **At the end of speech**:<br><br>   * `definite`: `true`, indicating the clause is finished.<br><br>   * `paragraph`: `true`, indicating the entire sentence is finished. |
|Server receives |**Subtitle source**: ASR content.<br><br>**Return method**: Segmented; returned only after a complete segment is identified.<br><br>> For example, if the user says, "Hello. Query the weather in Shanghai," you will receive two separate subtitle messages in sequence: `Hello.`, and `Query the weather in Shanghai`.<br><br><br>**Subtitle status**:<br><br><br>* **During speech**:<br><br>   * `definite`: Always `true`.<br><br>   * `paragraph`: Always `false`.<br><br>* **At the end of speech**:<br><br>   * `definite`: `true`.<br><br>   * `paragraph`: `true`. |**Subtitle source**: LLM text or TTS reading content (determined by `SubtitleMode`)<br><br>**Return method**: Segmented; returned only after a complete segment is identified.<br><br>> For example, if the AI says "The weather is hot. The temperature is 30 degrees Celsius," you will receive the clauses in sequence: `The weather is hot.` and `The temperature is 30 degrees Celsius.`.<br><br><br>**Subtitle status**:<br><br><br>* **During speech** :<br><br>   * `definite`: Always `true`, indicating the clause is finished.<br><br>   * `paragraph`: Always `false`, indicating the entire sentence is not yet finished.<br><br>* **At the end of speech** :<br><br>   * `definite`: `true`, indicating the clause is finished.<br><br>   * `paragraph`: `true`, indicating the entire sentence is finished. |


<span id="310810c2"></span>
## FAQ


* Q1: Can subtitles be returned to the business side before the user or AI speaks?

   Not supported.

* Q2: Do subtitles support receiving images?

   Not supported.

* Q3: Is the subtitle feature supported in the WeChat Mini Program?

   Supported.

* Q4: The received subtitles contain many homophone errors compared to the actual content.

   Different models produce different recognition results for homophones. You can improve subtitle accuracy by enhancing the accuracy of speech recognition.

* Q5: Do subtitles support returning hyperlink content?

   Not supported.
