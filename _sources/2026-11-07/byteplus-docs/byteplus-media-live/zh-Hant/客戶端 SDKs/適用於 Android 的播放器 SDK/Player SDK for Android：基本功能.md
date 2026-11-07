---
title: "Player SDK for Android：基本功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-2-zh-TW"
---

本主題介紹如何實作 Player SDK for Android 的基本功能。

## 前提條件

你已依照 [整合 Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android) 和 [初始化 Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android) 中提供的說明，完成 Player SDK 的整合與初始化。

## 注意事項

Player SDK 使用多種 Android 音訊和視訊 API，這些 API 可能無法在模擬器上正常運作。建議使用實體裝置進行偵錯。

## 建立播放器

若要實作 Player SDK 的基本功能，你必須先建立播放器。

```Java
// 建立播放器。
VeLivePlayer mLivePlayer = new VideoLiveManager(Env.getApplicationContext());
```

> **警告**

> 為確保最佳播放效果，建議為每次播放工作階段建立新的播放器執行個體，而不是重複使用現有執行個體。

## 設定播放器

使用 [VeLivePlayerConfiguration](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration) 設定播放器的初始設定，並呼叫 [setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig) 套用設定。在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前完成設定。下表說明 `VeLivePlayerConfiguration` 中的參數。

|參數 |類型 |說明 |
|---|---|---|
|enableSei |boolean |是否啟用字串 SEI 訊息剖析。預設值為 `false`。 |
|enableBinarySei |boolean |是否啟用二進位 SEI 訊息剖析。預設值為 `false`。啟用後，播放器會接收二進位 SEI 訊息，且不再觸發字串 SEI 訊息回呼。 |
|enableHardwareDecode |boolean |是否啟用硬體解碼。預設值為 `true`。啟用後，如果硬體解碼無法啟動或在播放期間失敗，播放器會自動切換至軟體解碼。 |
|networkTimeoutMs |int |網路逾時時間，單位為毫秒。預設值為 `5000`。傳送網路請求後，如果在此期間內未收到伺服器回應，播放器會將該請求視為失敗。 |
|retryIntervalTimeMs |int |重試間隔，單位為毫秒。預設值為 `5000`。如果網路錯誤或類似問題中斷直播播放，播放器會依此間隔重試播放。 |
|retryMaxCount |int |網路連線錯誤後的最大重試次數。預設值為 `5`。值為 `0` 會停用播放器的內部重試。 |
|stallRetryTimeout |long |因卡頓而停止重試的逾時閾值，單位為毫秒。預設值為 `10000`（10 秒）。當卡頓持續時間超過此閾值時，播放器會停止重試。 |
|enableLiveDNS |boolean |是否啟用本機 DNS 預取。預設值為 `false`。啟用本機 DNS 預取可縮短開始播放所需時間。<br><br>> **警告**<br><br><br>> 本機 DNS 預取期間發生錯誤，可能會影響播放器正常運作。<br> |
|enableStatisticsCallback |boolean |是否啟用播放資訊的週期性回呼。預設值為 `false`。 |
|statisticsCallbackInterval |int |提供播放資訊的週期性回呼時間間隔，單位為秒。預設值為 `5`。 |

以下範例程式碼示範如何設定播放器的初始設定。

```Java
// 建立 VeLivePlayerConfiguration 執行個體。
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
// 啟用提供播放資訊的週期性回呼。
config.enableStatisticsCallback = true;
// 啟用本機 DNS 預取。
config.enableLiveDNS = true;
// 設定播放器的初始設定。
mLivePlayer.setConfig(config);
```

## 設定播放器觀察者

呼叫 [setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver) 設定播放器觀察者，並實作 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#veliveplayerobserver) 介面，以監聽播放器狀態更新、錯誤、第一個音訊和視訊影格事件，以及週期性播放統計資料。在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前設定觀察者。範例程式碼如下。

```Java
// 建立播放器觀察者執行個體。
VeLivePlayerObserver mLivePlayerObserver = new VeLivePlayerObserver() {
        
   @Override
   public void onError(VeLivePlayer player, VeLivePlayerError error) {
      // 播放器發生錯誤時觸發。
   }

   @Override
   public void onInfo(VeLivePlayer player, VeLivePlayerError error) {
      // 播放器遇到內部錯誤時觸發。
   }
   
   @Override
   public void onFirstVideoFrameRender(VeLivePlayer player, boolean isFirstFrame) {
      // 第一個視訊影格完成算繪時觸發。
   }

   @Override
   public void onFirstAudioFrameRender(VeLivePlayer player, boolean isFirstFrame) {
      // 第一個音訊影格完成算繪時觸發。
   }

   @Override
   public void onStallStart(VeLivePlayer player) {
    // 播放卡頓開始時觸發。
  }

  @Override
   public void onStallEnd(VeLivePlayer player) {
    // 播放卡頓停止時觸發。
  }

  @Override
   public void onVideoRenderStall(VeLivePlayer player, long stallTime) {
    // 視訊算繪卡頓時觸發。
  }

  @Override
   public void onAudioRenderStall(VeLivePlayer player, long stallTime) {
    // 音訊算繪卡頓時觸發。
  }

  @Override
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
    // 播放器切換至不同畫質層級時觸發。
  }

  @Override
   public void onVideoSizeChanged(VeLivePlayer player, int width, int height) {
    // 視訊大小變更時觸發。
  }

  @Override
   public void onReceiveSeiMessage(VeLivePlayer player, String message) {
    // 播放器收到字串 SEI 訊息時觸發。
  }

  @Override
   public void onReceiveBinarySeiMessage(VeLivePlayer player, byte[] message) {
    // 播放器收到二進位 SEI 訊息時觸發。啟用 enableBinarySei 以接收此回呼。啟用後，不再觸發字串 SEI 訊息回呼。
  }

  @Override
   public void onMainBackupSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStreamType streamType, VeLivePlayerError error) {
    // 播放器在主要和備用串流之間切換時觸發。
  }

  @Override
   public void onStreamFormatSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerFormat fromStreamFormat, VeLivePlayerDef.VeLivePlayerFormat toStreamFormat, VeLivePlayerError error, Bundle extraInfo) {
    // 播放器切換串流格式時觸發。
  }

  @Override
   public void onPlayerStatusUpdate(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStatus status) {
    // 播放器狀態變更時觸發。
  }

  @Override
   public void onPlayerStatusUpdate(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStatus status, Bundle extraInfo) {
    // 播放器狀態變更時觸發。extraInfo 參數提供目前播放串流的補充資訊。
  }

  @Override
   public void onStatistics(VeLivePlayer player, VeLivePlayerStatistics statistics) {
    // 定期觸發以回報播放統計資料。
  }

  @Override
   public void onSnapshotComplete(VeLivePlayer player, Bitmap bitmap) {
    // 完成螢幕截圖時觸發。
  }

  @Override
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
    // 播放器解碼視訊影格時觸發。
  }

  @Override
   public void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
    // 播放器解碼音訊影格時觸發。
  }

  @Override
   public void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error) {
    // SDK 無法啟用超解析度時觸發。
  }

  @Override
   public void onStreamFailedOpenSharpen(VeLivePlayer player, VeLivePlayerError error) {
    // SDK 無法啟用視訊銳化時觸發。
  }
};

// 設定播放器觀察者。
mLivePlayer.setObserver(mLivePlayerObserver);
```

## 設定算繪檢視

若要讓播放器顯示視訊，你需要設定用於視訊算繪的檢視。播放器提供兩種算繪檢視選項：`SurfaceView` 和 `TextureView`。

|維度 |SurfaceView |TextureView |
|---|---|---|
|特性 |提供獨立的繪圖表面，並為複雜 UI 提供高效率算繪。 |作為一般檢視運作，並支援動畫和轉換。 |
|執行緒 |在獨立執行緒上繪製，不佔用主執行緒資源。 |使用與 `Activity` 或 `Fragment` 相同的生命週期。 |
|建議情境 |複雜 UI 算繪、高效率繪圖、遊戲及類似情境。 |圖片顯示、動畫效果，以及需要與一般檢視相容的情境。 |

根據需求選擇算繪檢視，並參考以下範例程式碼進行設定。

### 設定 SurfaceView

1. 在版面配置 XML 檔案中宣告 `SurfaceView`。

   ```XML
   <SurfaceView
       android:id="@+id/surfaceView"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```

2. 呼叫 [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) 使用 `SurfaceView` 設定視訊算繪。

   ```Java
   SurfaceView surfaceView = findViewById(R.id.surfaceView);
   mLivePlayer.setSurfaceHolder(surfaceView.getHolder());
   ```

> **警告**

> 如果你使用 `SurfaceView` 算繪視訊影格，裝置的 API level 必須為 24 或更高。否則，可能會發生檢視階層問題、動畫不同步或其他問題。如果裝置的 API level 低於 24，建議使用其他算繪方法，或升級 API level 以取得最佳播放體驗。

### 設定 TextureView

1. 在版面配置 XML 檔案中宣告 `TextureView`。

   ```XML
   <TextureView
       android:id="@+id/textureView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:background="@null" />
   ```

2. 呼叫 [setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) 使用 `TextureView` 設定視訊算繪。

   ```Java
   TextureView textureView = findViewById(R.id.textureView);
   
   // 設定 SurfaceTexture 監聽器。
   textureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
   
       @Override
       public void onSurfaceTextureAvailable(SurfaceTexture surfaceTexture, int width, int height) {
          // TextureView 的 SurfaceTexture 可用時觸發。
           mLivePlayer.setSurface(new Surface(surfaceTexture));
       }
       
       @Override
       public void onSurfaceTextureSizeChanged(SurfaceTexture surfaceTexture, int width, int height) { 
           // TextureView 的大小變更時觸發。
       }
       
       @Override
       public boolean onSurfaceTextureDestroyed(SurfaceTexture surfaceTexture) {
          // SurfaceTexture 即將被銷毀時觸發。傳回 true 可讓 TextureView 自動釋放 SurfaceTexture。如果此方法傳回 false，請呼叫 surfaceTexture.release() 手動釋放 SurfaceTexture。
           return true;
       }
       
       @Override
       public void onSurfaceTextureUpdated(SurfaceTexture surfaceTexture) {
          // TextureView 更新時觸發。    
       }
   });
   ```

## 設定播放 URL

呼叫 [setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) 設定單一播放 URL。此方法支援 RTMP、FLV 和 HLS 等直播串流通訊協定。將範例程式碼中的 URL 替換為你的實際直播播放 URL。請在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前呼叫此方法。範例程式碼如下。

```Java
String playUrl = "http://pull.example.com/live/stream.flv";
mLivePlayer.setPlayUrl(playUrl); // 設定播放 URL。
```

> **說明**

> 若要設定多個播放 URL，請呼叫 [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata)。此方法支援 RTM 拉流、QUIC 拉流、主備串流切換、多個畫質層級和自適應位元率 (ABR) 等功能。請在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前呼叫此方法。如需詳細資訊，請參閱 [Player SDK for Android：進階功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)。

## 調整播放畫面

你可以設定填滿模式、鏡像和旋轉，以取得更好的播放體驗。

### 設定填滿模式

呼叫 [setRenderFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) 設定播放畫面的填滿模式。播放器支援以下填滿模式。

|填滿模式 |說明 |
|---|---|
|VeLivePlayerFillModeAspectFit |顯示完整視訊影格。視訊影格會等比例縮放，直到整個影格符合畫布。如果視訊影格的長寬比與畫布不同，未填滿的區域會顯示為黑色。 |
|VeLivePlayerFillModeFullFill |讓視訊影格適應畫布。視訊影格會非等比例縮放，直到填滿畫布。在此過程中，視訊影格的長寬比可能會改變。 |
|VeLivePlayerFillModeAspectFill |以視訊填滿畫布。視訊影格會等比例縮放，直到填滿畫布。超出螢幕的視訊影格部分會被裁切。因此，視訊影格的某些部分可能不可見。 |

```Java
// 將填滿模式設定為 aspect fill。
mLivePlayer.setRenderFillMode(VeLivePlayerFillModeAspectFill);
```

### 設定鏡像

呼叫 [setRenderMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrendermirror) 設定播放畫面的鏡像模式。播放器支援以下鏡像模式。

|鏡像模式 |說明 |
|---|---|
|VeLivePlayerMirrorNone |無鏡像。 |
|VeLivePlayerMirrorHorizontal |水平鏡像。 |
|VeLivePlayerMirrorVertical |垂直鏡像。 |

```Java
// 設定水平鏡像。
mLivePlayer.setRenderMirror(VeLivePlayerMirrorHorizontal);
```

### 設定旋轉角度

呼叫 [setRenderRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) 設定播放畫面的旋轉角度。播放器支援以下旋轉角度。

|旋轉角度 |說明 |
|---|---|
|VeLivePlayerRotation0 |不旋轉。 |
|VeLivePlayerRotation90 |將視訊順時針旋轉 90 度。 |
|VeLivePlayerRotation180 |將視訊順時針旋轉 180 度。 |
|VeLivePlayerRotation270 |將視訊順時針旋轉 270 度。 |

```Java
// 將視訊順時針旋轉 90 度。
mLivePlayer.setRenderRotation(VeLivePlayerRotation90);
```

## 開始播放

呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 開始播放。

```Java
mLivePlayer.play(); // 開始播放。
```

你可以呼叫 [isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-isplaying) 取得目前播放狀態。

```Java
boolean isPlaying = mLivePlayer.isPlaying(); // 取得播放狀態。
```

## 停止播放

呼叫 [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop) 停止播放。呼叫 `stop` 不會銷毀播放器。

```Java
mLivePlayer.stop(); // 停止播放。
```

## 銷毀播放器

停止播放後，如果不再需要播放器，請呼叫 [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy) 銷毀播放器並釋放其相關記憶體。

```Java
mLivePlayer.destroy(); // 銷毀播放器並釋放其相關記憶體。
```

## 處理應用程式前景和背景轉換

預設情況下，應用程式進入背景後，播放器會繼續播放音訊。若要防止音訊在背景中繼續播放，請在應用程式進入背景時停止播放，並在應用程式返回前景時恢復播放，如以下程式碼所示：

```Java
@Override
protected void onResume() {
    super.onResume();
    if (mLivePlayer != null) {
        mLivePlayer.play(); // 應用程式切換至前景時恢復播放。
    }
}
 
@Override
protected void onPause() {
    super.onPause();
    if (mLivePlayer != null) {
        mLivePlayer.stop(); // 應用程式切換至背景時停止播放。
    }
}
```

## 靜音

呼叫 [setMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setmute) 將音訊設為靜音或取消靜音。

```Java
mLivePlayer.setMute(true); // 將播放設為靜音。
```

你可以呼叫 [isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-ismute) 查詢音訊是否已靜音。

```Java
boolean isMute = mLivePlayer.isMute(); // 取得靜音狀態。
```

## 設定播放器音量

呼叫 [setPlayerVolume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayervolume) 設定播放器音量。此參數指定音量等級。預設值為 `1.0`。有效範圍為 `[0.0, 1.0]`。

```Java
mLivePlayer.setPlayerVolume(0.5f); // 設定播放器音量。
```

## 設定日誌層級

呼叫 [setLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setloglevel) 設定列印到主控台的日誌層級。

```Java
// 將日誌層級設定為 DEBUG。將輸出 DEBUG、INFO、WARNING 和 ERROR 層級的日誌。
VeLivePlayer.setLogLevel(VeLivePlayerLogConfig.VeLivePlayerLogLevel.VeLivePlayerLogLevelDebug);
```
