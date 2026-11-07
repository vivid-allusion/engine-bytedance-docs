---
title: "Starting a co-host with guests"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-starting-a-video-chat"
---

The host can co\-host with up to 25 guests simultaneously.

<span id="Before you start"></span>
## Prerequisites


* The host must have a BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This prerequisite is not required for hosts who enter the live streaming page in a web browser through a URL, which allows direct access without logging in.   </div>
   

* We recommend that the host and guests use devices and browsers that meet the requirements as described in [Live streaming from your web browser](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser#environmental-requirements-to-start-a-live-stream) during the co\-host.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Guests can use either integrated or discrete graphics cards during the co\-host.   </div>
   

<span id="369ac5d3"></span>
## Roles


|Role |Description |
|---|---|
|Host |The initiator of co\-host and live stream. The host has full control permission, including the ability to set the presenter, lock a guest's camera, and remove guests from the co\-host. |
|Presenter |The primary participant in the co\-host. By default, the host is the presenter. The host can set a guest as the presenter and can revoke or transfer the presenter role at any time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The co\-host can only have one presenter at the same time and only the presenter can use the <strong>Share</strong>, <strong>Whiteboard</strong>, or <strong>Document</strong> feature.</div><br> |
|Guest |A participant in the co\-host. |


<span id="4f21ea9e"></span>
## Host

The host can co\-host with guests before or after the live stream starts.


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Select **Web browser** as the broadcast method and go to the live streaming page. For more information, see [Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser).

3. Click **Co\-host with guests**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/689c7ad2fec34948a25ad0cd4b528604~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Guests can also be invited before the co\-host starts, but they are only able to join after the co\-host starts.   </div>
   

4. Select the layout for the host and guest windows. The presenter view is selected by default.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/482851ca634d4284ae44ae4d26def8df~tplv-goo7wpa0wc-image.image) </span>

   * Focus view: displays the presenter's camera as the main screen. This view is suitable for individual speeches.

      If the host locks the camera of a guest, the main screen will display the guest's camera.

   * Presenter view: displays what the presenter is sharing, along with the presenter's camera as the main screen. This view is suitable when the presenter is using the **Share**, **Whiteboard**, or **Document** feature.

      If the host locks the camera of a guest, the main screen will display the guest's camera and what the presenter is sharing.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The camera of the presenter or locked guest can only be displayed when their camera is turned on.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The displayed camera can be dragged to a desired location.      </div>
      

   * Gallery view: displays the cameras of multiple participants and what the presenter is sharing. This view is suitable for multi\-party meetings and multi\-site connections.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Guests can select their own layout for the host and guest windows. Their selected layout will not be changed if the host changes the layout.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the live stream starts, the layout on the viewing page is the same as that on the host side, but the windows of the host and guests are not displayed on the viewing page in the focus view.   </div>
   

5. Invite guests.

   1. Click **Invite guests**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa817f2751b944b79abae76ee2ef550c~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Invite guests** dialog box that appears, select whether to turn on the **Key** switch. By default, the switch is turned on. If turned on, guests must enter the key to join the co\-host.

      The host can also click **Update key** to update the key in real time.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After the key is updated, existing guests can continue the co\-host, while new guests must use the updated key to join.      </div>
      

   3. Click **Copy invitation information** and send the copied information to the guests to be invited. Guests can then join the co\-host by using the Chrome browser. For more information, see [Guests](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-video-chat#98b43ebc).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The copied information consists of the activity ID and name of the live room, and the login URL and key for co\-host. If the <strong>Key</strong> switch is turned off, the copied information consists of the activity ID and name of the live room, and the login URL for co\-host.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The host can also click to copy the login URL or key separately.      </div>
      

6. In the co\-host list, perform the following operations as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bca79f9ca9cc4e94a51c665b998349f5~tplv-goo7wpa0wc-image.image) </span>

   * Click **Mute all** to mute the microphones of all participants except for the host and the presenter. New participants will also be muted when joining the co\-host. Participants can unmute themselves.

   * Click the camera icon on the right of a guest to request turning on or directly turning off the guest's camera. Guests can choose whether to turn on the camera based on the prompts they receive.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25a5f06e9bd647838c15ac1bf8d7fc67~tplv-goo7wpa0wc-image.image) </span>

   * Click the microphone icon on the right of a guest to request turning on or directly turning off the guest's microphone. Guests can choose whether to turn on the microphone based on the prompts they receive.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/706d241798664e379c64653d894d3e6f~tplv-goo7wpa0wc-image.image) </span>

   * Click the **More** icon on the right of a guest to perform the following operations.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f31c73731503419186f02db8d8fc92db~tplv-goo7wpa0wc-image.image) </span>

      * Click **Set as presenter** to set that guest as the presenter.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">If no guest is set as the presenter, the host will be the presenter.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">If the presenter exits the co\-host due to an unexpected issue, the presenter role will automatically revert to the host.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">When the presenter is changed, the system will automatically save the whiteboard, document, and screen (including the entire screen, window, and Chrome tab) shared by the original presenter. If the original presenter is set as the presenter again during the same co\-host session, they can choose to continue sharing the previously shared content.         </div>
         

      * Click **Revoke presenter** to revoke the presenter role. The host can also click the **More** icon on the right of another guest and select **Set as presenter** to change the presenter.

      * Click **Change name** to change the guest's nickname.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The nickname cannot exceed 60 characters.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The host can also click the <strong>More</strong> icon on the right of themselves and select <strong>Change name</strong> to change their own nickname.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Once the host's nickname is changed, the corresponding nickname in the menu for chat interaction of the console, viewing page, and live streaming page is synchronously updated.         </div>
         

      * Click **Lock camera** to lock the guest's camera in the main screen.

      * Click **Unlock** to cancel the lock of the guest's camera. The host can also click the **More** icon on the right of another guest and select **Lock camera** to change the locked camera.

      * Click **Remove** to remove the guest from the co\-host.

   * Click **End co\-host with guests**. All guests will then exit the co\-host automatically.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db42c2a1d45540d78d8faea7a8a10c0e~tplv-goo7wpa0wc-image.image) </span>


<span id="b1185902"></span>
## Presenter

The presenter can be either the host or one of the guests who joined the co\-host.


* Host: The host serves as the presenter if no guest is set as the presenter.

* Guest: The host can set a guest as the presenter.


After joining the co\-host using the Chrome browser, the presenter can use the **Share**, **Whiteboard**, or **Document** feature.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only the host can use the <strong>Whiteboard</strong> and <strong>Document</strong> features as a presenter. For more information on how to use these features, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/sharing-the-whiteboard">Sharing the whiteboard</a> and <a href="https://docs.byteplus.com/docs/byteplus-livesaas/sharing-documents-and-pictures">Sharing documents and pictures</a>.</div>


* <div data-tips="true" data-tips-type="tip">When using the <strong>Share</strong> feature to share the entire screen, a window, or a Chrome tab, we recommend that you share a Chrome tab for synchronized audio and higher\-definition viewing. When sharing a window, we recommend that you do not minimize the window to avoid affecting viewers' experience.</div>



The following figure shows an example of when a guest is the presenter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01d76cd78baf45b884156bb275e32e93~tplv-goo7wpa0wc-image.image) </span>

<span id="98b43ebc"></span>
## Guests

After receiving the invitation information from the host, guests can enter the co\-host login page by entering the login URL in the address bar of the Google Chrome browser.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Guests cannot join the co\-host using mobile devices.</div>


* <div data-tips="true" data-tips-type="tip">Guests can join the co\-host before or after the host starts the live stream.</div>



Guests can click the **Change name** icon in the co\-host list to change their nicknames.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cfd976290704d1da67b42f6bae51394~tplv-goo7wpa0wc-image.image) </span>


|Scenario |Chrome browser |Description |
|---|---|---|
|Join the co\-host |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2145beb2552d47e49ed5a58fb131bb5f~tplv-goo7wpa0wc-image.image) </span> |Enter the login URL in the address bar of the Chrome browser. On the login page, enter the nickname and key, and then click **Start co\-host**. In the **Test your device** dialog box that appears, select the camera and microphone. Once the camera, microphone, network, and browser are detected to be functioning normally, click **Start co\-host**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the <strong>Key</strong> switch is turned off when the host invites the guest, the key is not required on the login page.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The nickname cannot exceed 60 characters in length.</div><br> |
|Select the layout for the host and guest windows |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa54b3db3e5c401cae856fa141a378c6~tplv-goo7wpa0wc-image.image) </span> |Guests can select their own layout for the host and guest windows. The selection only affects a guest's own viewing experience. |
|Select the gallery view |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b6796e0d534663ab7fd1284f1996d8~tplv-goo7wpa0wc-image.image) </span> |Displays the cameras of multiple participants and what the presenter is sharing. This view is suitable for multi\-party meetings and multi\-site connections. |
|Select the focus view |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/109ac82935c74192b8d32b1ae433e85e~tplv-goo7wpa0wc-image.image) </span> |Displays the presenter's camera as the main screen. This view is suitable for individual speeches.<br><br>If the host locks the camera of a guest, the main screen will display the guest's camera. |
|Select the presenter view |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7df3b6c196ed49fdbe083594c9ffbd08~tplv-goo7wpa0wc-image.image) </span> |Displays what the presenter is sharing, along with the presenter's camera as the main screen. This view is suitable when the presenter is using the **Share**, **Whiteboard**, or **Document** feature.<br><br>If the host locks the camera of a guest, the main screen will display the guest's camera and what the presenter is sharing.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The camera of the presenter or locked guest can only be displayed when their camera is turned on.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The displayed camera can be dragged to a desired location.</div><br> |
