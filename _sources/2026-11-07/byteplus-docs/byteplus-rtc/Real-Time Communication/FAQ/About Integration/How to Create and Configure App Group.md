---
title: "How to Create and Configure App Group"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-125721"
---

In iOS application development, data sharing between multiple apps or components can be achieved by configuring each app or component to belong to the same App Group. For example, to accomplish cross\-app screen sharing, you need to record the screen through the Broadcast Upload Extension component and pass the recorded data to the main process.

This article introduces how to create an App Group and configure the App Group for different apps or components.

<span id="create-an-app-group"></span>
## Create an App Group


1. Log in to [Apple Developer](https://developer.apple.com) using an Apple ID that has already been enrolled in the developer program.

2. Navigate to the "**Certificates, IDs & Profiles**" section, and click on "**Identifiers**" under the section.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/01.png) </span>

3. Click on the " **+** " button to create a new app group.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/02.png) </span>

4. Select App Groups and click on "**Continue**" in the top right corner.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/03.png) </span>

5. In the "**App Group**" creation form, enter a unique **identifier** and a brief **description** for the app group, then click on the "**Continue**" button to create the app group.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/4.png) </span>

6. Review the details and click on the "**Register**" button to complete the app group creation.


<span id="configure-the-app-group-for-an-app-id"></span>
## Configure the App Group for an App ID

In the Apple Developer center, configure the same App Group for the applications and components that need to share data.


1. Click on the "**App IDs**" drop\-down menu in the top right corner of the Identifier section, find and select the specific App ID for which you want to configure the App Group.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/0x.png) </span>

2. Enable "**App Groups**" service, and click on the "**Edit**" button.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/05.png) </span>

3. Select the desired App Group from the list in the pop\-up window, and click on "**Continue**" to return to the editing page. Click on "**Save**" to complete the configuration.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/06.png) </span>

4. Select another app or component that needs to share data with this app, and repeat the above steps.

5. Download and configure the **Provisioning Profile** into XCode.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/00.png) </span>


<span id="configure-the-app-group-in-xcode"></span>
## Configure the App Group in Xcode

Configure the same App Group in your Xcode project for apps or components that require data sharing.


1. Open your Xcode project. Select the target app or component for which you want to configure the App Group.

2. Go to the "**Signing & Capabilities**" tab, and click on " **+ Capacities**" under the tab.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/08.png) </span>

3. Double\-click "**App Groups**" in the pop\-up window.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/09.png) </span>

4. Add and check the App Group created before.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/010.png) </span>

5. Repeat the above steps, and configure the same App Group for other Apps or components that need to share data.
