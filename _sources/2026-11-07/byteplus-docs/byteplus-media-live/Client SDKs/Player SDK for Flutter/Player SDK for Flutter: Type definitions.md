---
title: "Player SDK for Flutter: Type definitions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions"
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


The configurations for the playback URL.

<span id="453345bb"></span>
## Member Property

<span id="9d48e75c"></span>
### enableABR

```Dart
bool? enableABR;
```


Whether to enable the adaptive bitrate (ABR) feature. The default value is `false`. Valid values:


* `true`: Enable.

* `false`: Disable.


<span id="43df963c"></span>
### enableMainBackupSwitch

```Dart
bool? enableMainBackupSwitch;
```


Whether to enable the primary and backup streams feature. The default value is `false`. Valid values:


* `true`: Enable.

* `false`: Disable.


<span id="82b62d43"></span>
### defaultResolution

```Dart
VeLivePlayerResolution? defaultResolution;
```


The player's default resolution. The default value is the original stream resolution. For more information, see [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#42f7c972).

<span id="74cbd102"></span>
### defaultFormat

```Dart
VeLivePlayerFormat? defaultFormat;
```


The player's default playback format. The default value is FLV. For more information, see [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#53fdcf30).

<span id="ae27a644"></span>
### defaultProtocol

```Dart
VeLivePlayerProtocol? defaultProtocol;
```


The player's default transport layer protocol for playback. The default value is TCP. For more information, see [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#0386f298).

<span id="229168d0"></span>
### mainStream

```Dart
List<VeLivePlayerStream>? mainStream;
```


A list of primary stream addresses. For more information, see [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd).

<span id="f3209eee"></span>
### backupStream

```Dart
List<VeLivePlayerStream>? backupStream;
```


A list of backup stream addresses. For more information, see [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd).

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


Stream address information.

<span id="e9bed6a9"></span>
## Member Property

<span id="5dfebbf4"></span>
### url

```Dart
String url;
```


Playback URL.

<span id="77fc1c4e"></span>
### resolution

```Dart
VeLivePlayerResolution? resolution;
```


The resolution. The default value is the original stream resolution. For more information, see [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#42f7c972).

<span id="2e233c67"></span>
### bitrate

```Dart
int? bitrate;
```


Playback bitrate, measured in kbps.

<span id="035cf9b4"></span>
### protocol

```Dart
VeLivePlayerProtocol? protocol;
```


Transport layer protocol. The default value is TCP. For more information, see [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#0386f298).

<span id="abdb3c73"></span>
### format

```Dart
VeLivePlayerFormat? format;
```


Playback format. The default value is FLV. For more information, see [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#53fdcf30).

<span id="7772b028"></span>
### type

```Dart
VeLivePlayerStreamType? type;
```


The playback stream type, which is either primary stream or backup stream. The default value is primary stream. For more information, see [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#bcf3b0e9).

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


The player's resolution.

<span id="effe48af"></span>
## Enumerated Value


|Type |Value |Description |
|---|---|---|
|origin |0 |Original stream. |
|uhd |1 |Ultra High Definition (UHD). |
|hd |2 |High Definition (HD). |
|sd |3 |Standard Definition (SD). |
|ld |4 |Low Definition (LD). |


<span id="53fdcf30"></span>
# VeLivePlayerFormat

```Dart
enum VeLivePlayerFormat {
  flv, 
  hls, 
  rtm, 
}
```


Playback format.

<span id="41d65f5e"></span>
## Enumerated Value


|Type |Value |Description |
|---|---|---|
|flv |0 |FLV format. |
|hls |1 |HLS format. |
|rtm |2 |RTM format. |


<span id="0386f298"></span>
# VeLivePlayerProtocol

```Dart
enum VeLivePlayerProtocol {
  tcp, 
  quic, 
  tls, 
}
```


Transport layer protocol.

<span id="303313fc"></span>
## Enumerated Value


|Type |Value |Description |
|---|---|---|
|tcp |0 |Transmission Control Protocol (TCP). |
|quic |1 |QUIC protocol. |
|tls |2 |TLS protocol. |


<span id="bcf3b0e9"></span>
# VeLivePlayerStreamType

```Dart
enum VeLivePlayerStreamType {
  main, 
  backup, 
}
```


Playback stream type.

<span id="93b62d79"></span>
## Enumerated Value


|Type |Value |Description |
|---|---|---|
|main |0 |Primary stream. |
|backup |1 |Backup stream. |
