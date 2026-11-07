---
title: "Advanced Feature Usage Instructions for RTC Flutter SDK"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1177504"
---

To access advanced RTC features that are not directly available in the Flutter layer, you can call native platform\-specific APIs. This guide demonstrates how to use a MethodChannel to establish communication between your Flutter code and the native RTC engine.

When using Flutter for cross\-platform application development, due to platform performance limitations, certain advanced audio and video processing functionalities may not be directly available in the Flutter layer. However, RTC Flutter SDK allows you to access the native RTC engine instance, which is specific to each platform. To communicate between the Flutter layer and the native layer in your project, you can use a custom MethodChannel. This allows you to establish a communication channel between Flutter and the native code, enabling you to call the custom functions implemented in the native layer from your Flutter code.

For more information, see Writing custom platform\-specific code to learn how a Flutter app can use native platform features.

Using custom audio processing as an example, you will learn the implementation steps for both iOS and Android to leverage the full capabilities of the native SDK.

<span id="sequence-diagram"></span>
# Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/flutteradvancefeatures.jpg) </span>

> Notes:

> 1. Please ensure that an `RTCVideo` instance has been created on the Flutter side before calling native interfaces.

> 2. Do not call the `destroy` interface on the native side directly, otherwise, it will cause unexpected behavior or runtime errors.


<span id="implementation"></span>
# Implementation

<span id="native-layer"></span>
## Native layer

<span id="ios"></span>
### iOS


1. Create a custom `MethodChannel` and call the native interface as needed.

   ```objectivec
   #import <Flutter/FlutterPlugin.h>
   #import <byteplus_rtc/ByteRTCVideoManager.h>
   #import <BytePlusRTC/BytePlusRTC.h>
   
   @interface RTCEngineFlutterPlugin : NSObject <FlutterPlugin>
   
   @end
   
   @implementation RTCEngineFlutterPlugin
   
   // Flutter Plugin
   
   + (void)registerWithRegistrar:(NSObject<FlutterPluginRegistrar>*)registrar {
       RTCEngineFlutterPlugin *instance = [[RTCEngineFlutterPlugin alloc] init];
       // You can replace the "MethodChannelName" below with a custom name of your choice. Make sure it remains consistent with the Flutter side.
       FlutterMethodChannel *methodChannel = [FlutterMethodChannel methodChannelWithName:@"MethodChannelName"
                                                                       binaryMessenger:registrar.messenger];
       [registrar addMethodCallDelegate:instance channel:methodChannel];
   }
   
   - (void)handleMethodCall:(FlutterMethodCall *)call result:(FlutterResult)result {
       // Forward message.
       // You can replace the "registerAudioProcessor" below with a custom name of your choice. Make sure it remains consistent with the Flutter side. It is recommended to use the native interface name directly.
       if ([call.method isEqualToString:@"registerAudioProcessor"]) {
           [self registerAudioProcessor:call.arguments result:result];
           return;
       }
       result(FlutterMethodNotImplemented);
   }
   
   // Custom method
   
   - (void)registerAudioProcessor:(NSDictionary *)arguments result:(FlutterResult)result {
       // Get the ByteRTCVideo instance.
       ByteRTCVideo *rtcVideo = [ByteRTCVideoManager getVideo];
       if (rtcVideo == nil) {
           result(@(-1));
           return;
       }
       // Register a custom audio processor.
       int res = [rtcVideo registerAudioProcessor:processor];
       result(@(res));
   }
   
   @end
   ```
   

2. Register your custom `MethodChannel` with the Flutter engine.

   ```objectivec
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
       [GeneratedPluginRegistrant registerWithRegistry:self];
       // Override point for customization after application launch.
       [RTCEngineFlutterPlugin registerWithRegistrar:[self registrarForPlugin:@"RTCEngineFlutterPlugin"]];
       return [super application:application didFinishLaunchingWithOptions:launchOptions];
   }
   ```
   


<span id="android"></span>
### Android


1. Add dependencies to the `build.gradle` file in the Android project.

   ```Groovy
   dependencies {
       // The Android SDK version must match the version that the Flutter SDK depends on. 
       // Check the version in `SDK root/android/build.gradle`.
       implementation 'com.byteplus:BytePlusRTC:X.X.X'
   }
   ```
   

2. Create a custom `MethodChannel` and call the native interface as needed.

   ```Java
   import androidx.annotation.NonNull;
   
   import com.ss.bytertc.engine.RTCVideo;
   import com.ss.bytertc.engine.flutter.base.RTCVideoManager;
   
   import java.util.Objects;
   
   import io.flutter.embedding.engine.plugins.FlutterPlugin;
   import io.flutter.plugin.common.BinaryMessenger;
   import io.flutter.plugin.common.MethodCall;
   import io.flutter.plugin.common.MethodChannel;
   import io.flutter.plugin.common.StandardMethodCodec;
   
   public class RTCEngineFlutterPlugin implements FlutterPlugin, MethodChannel.MethodCallHandler {
   
       private MethodChannel channel;
   
       @Override
       public void onAttachedToEngine(@NonNull FlutterPluginBinding binding) {
           BinaryMessenger binaryMessenger = binding.getBinaryMessenger();
           // You can replace the "MethodChannelName" below with a custom name of your choice. Make sure it remains consistent with the Flutter side.
           channel = new MethodChannel(binaryMessenger, "MethodChannelName", StandardMethodCodec.INSTANCE);
           channel.setMethodCallHandler(this);
       }
   
       @Override
       public void onDetachedFromEngine(@NonNull FlutterPluginBinding binding) {
           channel.setMethodCallHandler(null);
       }
   
       @Override
       public void onMethodCall(@NonNull MethodCall call, @NonNull MethodChannel.Result result) {
           // Forward message.
           // You can replace the "registerAudioProcessor" below with a custom name of your choice. Make sure it remains consistent with the Flutter side. It is recommended to use the native interface name directly.
           if (Objects.equals(call.method, "registerAudioProcessor")) {
               registerAudioProcessor(call, result);
               return;
           }
           result.notImplemented();
       }
   
       void registerAudioProcessor(@NonNull MethodCall call, @NonNull MethodChannel.Result result) {
           RTCVideo rtcVideo = null;
           try {
               // Get the RTCVideo instance.
               rtcVideo = RTCVideoManager.getRTCVideo();
           } catch (Exception e) {
               result.success(-1);
               return;
           }
           // Register a custom audio processor.
           int res = rtcVideo.registerAudioProcessor(processor);
           result.success(res);
       }
   }
   ```
   

3. Register your custom `MethodChannel` with the Flutter engine.

   ```Java
   public class MainActivity extends FlutterActivity {
   
       @Override
       public void configureFlutterEngine(@NonNull FlutterEngine flutterEngine) {
           super.configureFlutterEngine(flutterEngine);
           flutterEngine.getPlugins().add(new RTCEngineFlutterPlugin());
       }
   }
   ```
   


<span id="flutter-layer"></span>
## Flutter layer

Create a custom `MethodChannel`.

```Dart
class RTCEngineExtension {
  // You can replace the "MethodChannelName" below with a custom name of your choice. Make sure it remains consistent with the native side.
  static const MethodChannel _staticChannel = MethodChannel('MethodChannelName');

  static Future<int?> registerAudioProcessor() {
    // You can replace the "registerAudioProcessor" below with a custom name of your choice. Make sure it remains consistent with the native side. It is recommended to use the native interface name directly.
    return _staticChannel.invokeMethod<int>("registerAudioProcessor");
  }
}
```


<span id="more-tutorials"></span>
# More Tutorials

After calling native APIs as described in this article, refer to [Custom Audio Processing](https://docs.byteplus.com/en/docs/12/docs-80635) to complete the feature integration.

You can also use the approach described in this article to implement other advanced RTC features.
