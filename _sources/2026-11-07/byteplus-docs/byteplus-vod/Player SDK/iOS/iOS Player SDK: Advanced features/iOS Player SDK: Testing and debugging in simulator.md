---
title: "iOS Player SDK: Testing and debugging in simulator"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/testing-and-debugging-in-simulator-ios"
---

This document describes how to test and debug using the simulator. While the simulator provides a convenient environment for UI debugging and early testing, it's essential to remember that it doesn't perfectly replicate real device performance, especially for playback\-related features. For optimal results, we recommend testing these features on a real device.

<span id="d1375ea5"></span>
## Requirements


* SDK Version: 1.45.200.7 or higher

* Simulator Version: iOS 18 or higher


<span id="975e30d8"></span>
## Integration

The BytePlus Player SDK defaults to using [Metal rendering](https://developer.apple.com/metal/). Since simulators do not support Metal rendering, you need to specify to use OpenGL rendering.

```objectivec
#if TARGET_OS_IPHONE && TARGET_OS_SIMULATOR
    [self.videoEngine setOptionForKey:VEKKeyPlayerIsSimulator_BOOL value:@(YES)];
    [self.videoEngine setOptionForKey:VEKKeyViewRenderEngine_ENUM value:@(TTVideoEngineRenderEngineOpenGLES)];
#endif
```
