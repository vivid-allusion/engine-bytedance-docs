---
title: "Flutter 播放器 SDK：型別定義"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW"
---

<span id="dfb9d282"></span>
# VeLivePlayerStreamData

```Dart
class VeLivePlayerStreamData {
  bool? enableABR;
  bool? enableMainBackupSwitch;
  VeLivePlayerResolution? defaultResolution;
  VeLivePlayerFormat? defaultFormat;
  VeLivePlayerProtocol? defaultProtocol;
  List<VeLivePlayerStream>? mainStream;
  List<VeLivePlayerStream>? backupStream;

  VeLivePlayerStreamData({
    this.enableABR,
    this.enableMainBackupSwitch,
    this.defaultResolution,
    this.defaultFormat,
    this.defaultProtocol,
    this.mainStream,
    this.backupStream,
  });
} 
```


播放 URL 的配置。

<span id="453345bb"></span>
## 成員屬性

<span id="9d48e75c"></span>
### enableABR

```Dart
bool? enableABR;
```


是否啟用自適應碼率（ABR）功能。預設值為`false`。可用值：


* `true`：啟用。

* `false`：停用。


<span id="43df963c"></span>
### enableMainBackupSwitch

```Dart
bool? enableMainBackupSwitch;
```


指定是否啟用主備流切換。預設值為`false`。可用值：


* `true`：啟用。

* `false`：停用。


<span id="82b62d43"></span>
### defaultResolution

```Dart
VeLivePlayerResolution? defaultResolution;
```


播放器的預設解析度。預設值為原始串流解析度。如需更多資訊，請參閱[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#42f7c972)。

<span id="74cbd102"></span>
### defaultFormat

```Dart
VeLivePlayerFormat? defaultFormat;
```


播放器的預設播放格式。預設值為 FLV。如需更多資訊，請參閱[VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#53fdcf30)。

<span id="ae27a644"></span>
### defaultProtocol

```Dart
VeLivePlayerProtocol? defaultProtocol;
```


播放器的預設傳輸層協議。預設值為 TCP。如需更多資訊，請參閱[VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#0386f298)。

<span id="229168d0"></span>
### mainStream

```Dart
List<VeLivePlayerStream>? mainStream;
```


主串流位址列表。如需更多資訊，請參閱[VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#6c9e31fd)。

<span id="f3209eee"></span>
### backupStream

```Dart
List<VeLivePlayerStream>? backupStream;
```


備用串流位址列表。如需更多資訊，請參閱[VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#6c9e31fd)。

<span id="6c9e31fd"></span>
# VeLivePlayerStream

```Dart
class VeLivePlayerStream {
  String url;
  VeLivePlayerResolution? resolution;
  int? bitrate;
  VeLivePlayerProtocol? protocol;
  VeLivePlayerFormat? format;
  VeLivePlayerStreamType? type;

  VeLivePlayerStream({
    required this.url,
    this.resolution,
    this.bitrate,
    this.protocol,
    this.format,
    this.type,
  });
}
```


串流位址資訊。

<span id="e9bed6a9"></span>
## 成員屬性

<span id="5dfebbf4"></span>
### url

```Dart
String url;
```


播放 URL。

<span id="77fc1c4e"></span>
### resolution

```Dart
VeLivePlayerResolution? resolution;
```


解析度。預設值為原始串流解析度。如需更多資訊，請參閱[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#42f7c972)。

<span id="2e233c67"></span>
### bitrate

```Dart
int? bitrate;
```


播放碼率，單位為 kbps。

<span id="035cf9b4"></span>
### protocol

```Dart
VeLivePlayerProtocol? protocol;
```


傳輸層協議。預設值為 TCP。如需更多資訊，請參閱[VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#0386f298)。

<span id="abdb3c73"></span>
### format

```Dart
VeLivePlayerFormat? format;
```


播放格式。預設值為 FLV。如需更多資訊，請參閱[VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#53fdcf30)。

<span id="7772b028"></span>
### type

```Dart
VeLivePlayerStreamType? type;
```


播放串流型別，可為主串流或備用串流。預設值為主串流。如需更多資訊，請參閱[VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#bcf3b0e9)。

<span id="42f7c972"></span>
# VeLivePlayerResolution

```Dart
enum VeLivePlayerResolution {
  origin, 
  uhd, 
  hd, 
  sd, 
  ld, 
}
```


播放器解析度。

<span id="effe48af"></span>
## 列舉值


|型別 |值 |說明 |
|---|---|---|
|origin |0 |原始串流。 |
|uhd |1 |超高畫質（UHD）。 |
|hd |2 |高畫質（HD）。 |
|sd |3 |標準畫質（SD）。 |
|ld |4 |低畫質（LD）。 |


<span id="53fdcf30"></span>
# VeLivePlayerFormat

```Dart
enum VeLivePlayerFormat {
  flv, 
  hls, 
  rtm, 
}
```


播放格式。

<span id="41d65f5e"></span>
## 列舉值


|型別 |值 |說明 |
|---|---|---|
|flv |0 |FLV 格式。 |
|hls |1 |HLS 格式。 |
|rtm |2 |RTM 格式。 |


<span id="0386f298"></span>
# VeLivePlayerProtocol

```Dart
enum VeLivePlayerProtocol {
  tcp, 
  quic, 
  tls, 
}
```


傳輸層協議。

<span id="303313fc"></span>
## 列舉值


|型別 |值 |說明 |
|---|---|---|
|tcp |0 |傳輸控制協議（TCP）。 |
|quic |1 |QUIC 協議。 |
|tls |2 |TLS 協議。 |


<span id="bcf3b0e9"></span>
# VeLivePlayerStreamType

```Dart
enum VeLivePlayerStreamType {
  main, 
  backup, 
}
```


播放串流型別。

<span id="93b62d79"></span>
## 列舉值


|型別 |值 |說明 |
|---|---|---|
|main |0 |主串流。 |
|backup |1 |備用串流。 |
