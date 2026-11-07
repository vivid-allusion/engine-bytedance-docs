---
title: "Flutter 播放器 SDK：类型定义"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-CN"
---

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

## 成员属性

### enableABR

```Dart
bool? enableABR;
```

是否开启自适应码率（ABR）功能。默认值为 `false`。有效值：

* `true`：开启。

* `false`：关闭。

### enableMainBackupSwitch

```Dart
bool? enableMainBackupSwitch;
```

指定是否开启主流和备流之间的切换。默认值为 `false`。有效值：

* `true`：开启。

* `false`：关闭。

### defaultResolution

```Dart
VeLivePlayerResolution? defaultResolution;
```

播放器的默认分辨率。默认值为原始流分辨率。更多信息，请参见 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#42f7c972)。

### defaultFormat

```Dart
VeLivePlayerFormat? defaultFormat;
```

播放器的默认播放格式。默认值为 FLV。更多信息，请参见 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#53fdcf30)。

### defaultProtocol

```Dart
VeLivePlayerProtocol? defaultProtocol;
```

播放器的默认传输层协议。默认值为 TCP。更多信息，请参见 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#0386f298)。

### mainStream

```Dart
List<VeLivePlayerStream>? mainStream;
```

主流地址列表。更多信息，请参见 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd)。

### backupStream

```Dart
List<VeLivePlayerStream>? backupStream;
```

备流地址列表。更多信息，请参见 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#6c9e31fd)。

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

流地址信息。

## 成员属性

### url

```Dart
String url;
```

播放 URL。

### resolution

```Dart
VeLivePlayerResolution? resolution;
```

分辨率。默认值为原始流分辨率。更多信息，请参见 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#42f7c972)。

### bitrate

```Dart
int? bitrate;
```

播放码率，单位为 kbps。

### protocol

```Dart
VeLivePlayerProtocol? protocol;
```

传输层协议。默认值为 TCP。更多信息，请参见 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#0386f298)。

### format

```Dart
VeLivePlayerFormat? format;
```

播放格式。默认值为 FLV。更多信息，请参见 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#53fdcf30)。

### type

```Dart
VeLivePlayerStreamType? type;
```

播放流类型，可以是主流或备流。默认值为主流。更多信息，请参见 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions#bcf3b0e9)。

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

播放器的分辨率。

## 枚举值

|类型 |值 |描述 |
|---|---|---|
|origin |0 |原始流。 |
|uhd |1 |超高清（UHD）。 |
|hd |2 |高清（HD）。 |
|sd |3 |标清（SD）。 |
|ld |4 |低清（LD）。 |

# VeLivePlayerFormat

```Dart
enum VeLivePlayerFormat {
  flv, 
  hls, 
  rtm, 
}
```

播放格式。

## 枚举值

|类型 |值 |描述 |
|---|---|---|
|flv |0 |FLV 格式。 |
|hls |1 |HLS 格式。 |
|rtm |2 |RTM 格式。 |

# VeLivePlayerProtocol

```Dart
enum VeLivePlayerProtocol {
  tcp, 
  quic, 
  tls, 
}
```

传输层协议。

## 枚举值

|类型 |值 |描述 |
|---|---|---|
|tcp |0 |传输控制协议（TCP）。 |
|quic |1 |QUIC 协议。 |
|tls |2 |TLS 协议。 |

# VeLivePlayerStreamType

```Dart
enum VeLivePlayerStreamType {
  main, 
  backup, 
}
```

播放流类型。

## 枚举值

|类型 |值 |描述 |
|---|---|---|
|main |0 |主流。 |
|backup |1 |备流。 |
