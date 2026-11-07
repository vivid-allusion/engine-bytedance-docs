---
title: "Plugin descriptions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-d8idjfeza4"
---

VePlayer supports implementing all functionalities through plugins, including simple feature buttons, playback controls, and complex playback logic, among others. This page will introduce the methods for plugin registration, disabling, and configuration.

<span id="60b4c346"></span>
## Custom plugins

<span id="ff3164db"></span>
### Registering plugins

VePlayer supports two methods for registering plugins: registering during initialization and registering after initialization.

<span id="732e560d"></span>
#### **Method 1: Registering during Initialization**

When initializing a VePlayer instance, you can directly pass the plugin name to register the plugin (built\-in plugins do not require registration). Sample code is given below:

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://testpull.mycloud.com/live/mystream.m3u8',
  plugins: [window.VePlayerTimeShift],
  logger: {
    appId: '5****8',
  },
});
```


<span id="e7b00151"></span>
#### **Method 2: Registering after initialization**

After initializing the VePlayer instance, you can call the `registerPlugin` method and pass the plugin name to register the plugin (built\-in plugins do not require registration). Sample code is given below:

```JavaScript
VePlayer.createLivePlayer({
  //...
}).then(function(veplayer){
        veplayer.registerPlugin(window.VePlayerTimeShift)              
})
```


<span id="2d9e9af8"></span>
### Disabling plugins

VePlayer provides several built\-in functional plugins. If you need to disable a specific built\-in plugin, you can use the following method.


* For most plugins, you can pass the plugin name (case\-insensitive) to the `ignores` property in the VePlayer configuration to disable it. Taking the Picture\-in\-Picture plugin as an example, sample code is given below:

   ```JavaScript
   ignores: ['pip']
   ```
   

* For certain plugins, you can also disable them by configuring their specific options. Please refer to the documentation for the [Built-in plugins with UI](https://docs.byteplus.com/docs/byteplus-media-live/docs-d8idjfeza4#f3cebefe) for more details.


<span id="382a06f9"></span>
### Configuring plugins

VePlayer allows you to pass the names of individual plugins to configure their specific logic. For example, to configure the error plugin and its related parameters, you can do the following:

```JavaScript
error: {
   errorTipsText: 'error message', // error message
   showRefresh: true, // whether to refresh the button
}
```


<span id="87497923"></span>
### Replacing plugin icons

You can replace the button icons of built\-in plugins by configuring them. The list of plugins that support icon replacement can be found in the [Built-in plugin icons](https://docs.byteplus.com/docs/byteplus-media-live/docs-d8idjfeza4#2422295c) configuration. For example, to replace the icon of the play/pause button with a custom icon, simply pass the URL or DOM node of the desired replacement image in the configuration. The sample code is given below.

```JavaScript
import MyPlayIcon from '../icons/my-play-icon.svg';
import MyPauseIcon from '../icons/my-pause-icon.svg';

VePlayer.createLivePlayer({
  icons: {
    play: <img src={MyPlayIcon}>,
    pause: <img src={MyPauseIcon}>
  }
})
```


<span id="8e098451"></span>
## Built\-in plugins

VePlayer provides some built\-in functional plugins that are displayed by default or under specific conditions without the need for any additional imports.

<span id="f3cebefe"></span>
### Built\-in plugins with UI


|Plugin name |Description |Display by default |Disable display/ No displaycontrols |
|---|---|---|---|
|controls |Control bar plugin |Yes |```JavaScript```<br>```controls: false,```<br>``````<br>```// Or```<br>```controls: {```<br>```  disable: true,```<br>```}```<br> |
|fullscreen |The fullscreen toggle plugin, located in the control bar, is used to switch the current video to fullscreen mode. By default, the fullscreen plugin invokes the system's fullscreen functionality. |Yes |```JavaScript```<br>```fullscreen: false```<br>``````<br>```// Or```<br>```fullscreen: {```<br>```  disable: true```<br>```}```<br> |
|definition |Definition switching plugin |Display when multiple definitions are configured |When configuring a single playback URL or a playlist with only one definition available. |
|poster |Plugin to preview the first frame of player |Display when picture URLs are configured |Not to configure picture URLs |
|play |Play/Pause control plugin on the control bar |Yes |*  |
|refresh |Refresh control plugin on the control bar |Yes |*  |
|volume |Volume control plugin on the control bar |Yes |*  |
|loading |Plugin to display buffering information |Yes |*  |
|start |Play/Pause toggle button in the Center of the player |Yes |*  |
|enter |The loading button displayed during the initial initialization of the player |Yes |*  |
|refresh |Refresh button in the control bar |Yes |*  |
|pip |Whether to enable the PiP plugin |No |```JavaScript```<br>```pip: false```<br> |
|toast |Plugin for sending warning messages |Display warning message when switching definitions |*  |
|autoplayPlugin |Plugin to unmute |Take effects when `autoplay`is set to be `{muted:true}` |*  |
|error |Plugin for displaying error messages |Display when a severe error occurs that obstructs playback. Error message will be shown and a retry function will be provided. |*  |
|miniscreen |Plugin for entering the miniscreen |No |```JavaScript```<br>```mini: false, // default value```<br>```// Or```<br>```// miniscreen: {```<br>```//   disable: true,```<br>```// }```<br> |


<span id="32d22472"></span>
#### **Configuring mounting position**

The plugin configuration option `position` can be used to specify the position of the plugin's UI elements within the user interface, i.e., mounting the UI elements of the plugin onto specific DOM nodes. VePlayer defines the following two positions:


* **Default layout:**  The UI elements of the plugin are arranged and displayed according to the predefined layout.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4cf056e7c7044cd82c0a102ca87b828~tplv-goo7wpa0wc-image.image) </span>

* **flex layout:**  A flexible layout method that can automatically adapt the arrangement of UI elements based on screen size and requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/809477e999874cbbbd4bad4bf9b3c7f3~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>position</code> parameter or <code>root</code> parameter is not specified, the UI elements of the plugin will be mounted by default under the root node. This means that the plugin will appear in the default position.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the player loses focus, the plugins positioned at <code>ROOT_TOP</code>, <code>ROOT_RIGHT</code>, and <code>ROOT_LEFT</code> will automatically hide. This provides a better user experience and avoids interfering with the viewing of video content.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For small screens on mobile devices, when using <code>flex</code>layout, the plugin in the center position will adapt to the screen size. This is commonly used to display features such as the progress bar. This ensures that the plugin's functionality is displayed properly within the limited screen space.   </div>
   


<span id="cc61c91f"></span>
#### Configuring layout patterns

Controls plugin configuration option `mode` can be used to specify the layout mode of the control bar. Below are the visual representations of three layout modes:


* Normal: The plugins in the control bar are displayed in the configured order using the normal layout mode.

* Flex: The flex layout mode allows flexible adjustment of the position and size of plugins in the control bar, making them adaptable to different screen sizes and layout requirements.

* Bottom: The bottom layout mode places the control bar at the bottom of the player, which is suitable for display on mobile devices and provides a better touch operation experience.


<span id="5e3f2a1d"></span>
#### **Configuring index**

The plugin configuration option `index` is a numerical value used to determine the position of the plugin within its parent node. A smaller number indicates a higher position within the parent node. When multiple plugins have the same `index` value, their insertion order will be based on the order of registration. By adjusting the `index` value of the plugin, you can optimize the display order to meet specific requirements and layout needs.

<span id="758bbb54"></span>
### Built\-in plugins without UI


|**Plugin name（case\-insensitive）**  |**Description** |**Whether to enable** |
|---|---|---|
|keyboard |PC keyboard shortcut plugin |Enable only on the PC platform |
|mobile |Mobile web interaction plugin for the player |Enable only on the H5 (HTML5) platform |
|pc |Mobile PC interaction plugin for the player |Enable only on the PC platform |
|hlsjs |HLS.js playback plugin |Enable when playing in the format of HLS |
|flv |FLV playback plugin |Enable when playing in the format of FLV |
|rtm |RTM playback plugin |Enable when playing in the format of RTM |
|logger |Quality log reporting plugin |Enable only when `logger` is configured |


<span id="2422295c"></span>
### Built\-in plugin icons


|Key |Description |
|---|---|
|play |Play |
|pause |Pause |
|refresh |Refresh |
|startPlay |Start playing（in the middle of the player） |
|startPause |Pause playing（in the middle of the player） |
|volumeSmall |Reduce volume |
|volumeLarge |Increase volume |
|volumeMuted |Mute |
|openDanmu |Display the bullet comments |
|closeDanmu |Disable the display of bullet comments |
|screenshotIcon |Screenshot |
|fullscreen |Enter fullscreen |
|exitFullscreen |Exit fullscreen |
|screenBack |Exit fullscreen from the the top\-left corner (specifically for mobile devices) |
|cssFullscreen |Web\-page fullscreen |
|exitCssFullscreen |Exit web\-page fullscreen |
|pipIcon |Enter the PiP mode |
|pipIconExit |Exit the PiP mode |
|loadingIcon |Loading |
