---
title: "Control Data Sending After Applog Initialization"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Control-Data-Sending-After-Applog-Initialization"
---

<span id="android"></span>
## **Android**

Call setAutoStart (false) when initializing; then initialize, no data will be sent, and then call **AppLog.start () after authorization;** 

The data before uninitialization is cached in memory, with a limit of 300 pieces. After initialization, it can be persisted in db without limit.

<span id="demo"></span>
### **Demo**

```Plain
PHP
/* Initialization begins */
final InitConfig config = new InitConfig("204701", "your_channel"); // appid and channel. If you are not sure about appid, please contact the customer manager.
 // {{REPORT_URL}} For example, https://yourdomain.com, note that do not add “/” after domain name
config.setUriConfig(UriConfig.createByDomain("{{REPORT_URL}}", null));
 // Open circle event tracking
 config.setPicker(new Picker(this, config));
 // Open AB testing
 config.setAbEnable(true);
 //Turn on the circle preset event switch, true turn on，false turn off
 config.setAutoTrackEnabled (truw);
//Whether to report
 config.setAutoStart(false);
 
 AppLog.init(this, config);
 /* Initialization ends */
 
 //After authorization
 AppLog.start();

```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84c619e96c5a4dc28b214510158b8c7f~tplv-goo7wpa0wc-image.image) </span>

<span id="ios"></span>
## **iOS**

5.6.4 and above versions are required

Note: iOS delayed start, the launch timestamp may be later than the event timestamp

Initialize with the following method:

```Plain
 C++ 
 // After the additional configuration is completed, initialize the SDK at the end
 [BDAutoTrack sharedTrackWithConfig:config]; 

```


Call after authorization

```Plain
 C++ 
 // After initialization, the instance can be called to report. If it does not call, it will not report. 
 [BDAutoTrack startTrack]; 

```


Do not call//[BDAutoTrack gastTrack]; the data is stored in the sandbox database, and the expiration time is seven days

<span id="demo"></span>
### **Demo**

```Plain
C++
#import <RangersAppLog/BDAutoTrack.h>
#import <RangersAppLog/BDCommonEnumDefine.h> //The files that need to be introduced to set the private data sending address
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
   BDAutoTrackConfig *config = [BDAutoTrackConfig new];   
   // mandatory for configuration   
   config.appID = @"your appID";   
   config.appName = @"your appName";   
   config.channel = @"App Store";       
   // initialize instance
   BDAutoTrack *track = [BDAutoTrack trackWithConfig:config];       
   /* set private deployment server address */   
   BDAutoTrackRequestHostBlock block =     
^NSString *(BDAutoTrackServiceVendor vendor, BDAutoTrackRequestURLType    requestURLType) {          
       return @"{{REPORT_URL}}"; // here is private deployment server address       
    };  
    [BDAutoTrack setRequestHostBlock:block]; 
    
    // After the additional configuration is completed, initialize the SDK at the end
   [BDAutoTrack sharedTrackWithConfig:config]; 
   
   //custom event
   [BDAutoTrack eventV3:@"video_play_clicks" params: NULL];
   
   // After initialization, the instance can be called to report, and if not called, it will not report.
    [BDAutoTrack startTrack];


```
