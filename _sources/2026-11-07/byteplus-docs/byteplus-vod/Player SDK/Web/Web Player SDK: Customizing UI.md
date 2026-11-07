---
title: "Web Player SDK: Customizing UI"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-custom-ui-web"
---

VePlayer offers three methods for customizing the player UI. Method 1 and Method 2 allow you to change the color or icon of specific player elements. Method 3, on the other hand, is the most versatile and widely used approach, allowing for full customization of the player UI. By combining these three methods, you can easily meet your UI design needs.

<span id="7055b877"></span>
## **Method 1: Set the colors of** specific player elements

You can set the colors of specific player elements, such as the progress bar color, through the `commonStyle` configuration option. The following examples show the supported settings and explanations:

You can customize the colors of specific player elements, like the progress bar color, by using the `commonStyle` configuration option. The following examples show the supported settings and their explanations:

```JavaScript
commonStyle: {
  // Progress bar background color
  progressColor: '#f4f4f4',
  // Played part of the progress bar color
  playedColor: '#e3db68',
  // Cached part of the progress bar color
  cachedColor: '#ffb027',
  // Slider button style, supports string or Style object
  sliderBtnStyle: {
    backgroundColor: '#6b47e2'
  },
  // sliderBtnStyle: 'rgb(46 70 146)';
  // Volume color
  volumeColor: '#5bed67'
},
```


Please note that this method modifies the styles by setting the style attribute of the elements, which gives it a higher priority than any CSS styles you may have customized.

Example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e362910c5107499194660bc27007d7f2~tplv-goo7wpa0wc-image.image) </span>

<span id="9f2158b1"></span>
## **Method 2: Set the icons of** specific player elements

You can customize the icons of specific player elements by providing SVG icons in the settings.


* To pass the icons, use the `icons` option. Each item should be a function that returns an `HTMLElement`. Here's an example that shows how to change the icon of the button that enables external subtitles:

   ```JavaScript
   icons: {
     // Icon key
     vttSubOpen: () => {
         const img = document.createElement('img');
         img.src = 'https://p6-addone.****img.com/tos-**-i-hhc0kcolqq/92573eef59*****990fcc7a14cf.png~tplv-hhc***lqq-image.image';
         img.width = 20;
         img.height = 20;
         return img;
     }
   },
   ```
   

* Additionally, you can individually set the `icons` option for each plugin that includes icons. This option supports the `string | url | () => HTMLElement` type. Here's an example that shows how to change the icon of the play button in the control bar:

   ```JavaScript
   // Plugin name 
   play: {
     icons: {
       play: '<img src="https://p6-addone.****img.com/tos-**-i-hhc0kcolqq/92573eef59*****990fcc7a14cf.png~tplv-hhc***lqq-image.image',
     }
   },
   ```
   


Example:


|Before |After |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76736c3f122846f49544d79dc2c8cd6b~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88c8bc7e3f2143758f0a61ddf8ab7af3~tplv-goo7wpa0wc-image.image) </span> |


The following table lists the icon keys along with their plugin names.


|**Icon key** |**Icon description** |**Plugin name (Case\-insensitive)**  |**Note** |
|---|---|---|---|
|play |Icon for the play button in the control bar |play |N/A |
|pause |Icon for the pause button in the control bar |play |N/A |
|startPlay |Icon for the play button in the center of the screen |start |N/A |
|startPause |Icon for the pause button in the center of the screen |start |N/A |
|loadingIcon |Icon displayed in the center of the screen during loading |loading |N/A |
|replay |Icon for the replay button in the center of the screen at the end of playback |replay |N/A |
|fullscreen |Icon for the enter fullscreen button |fullscreen |N/A |
|exitFullscreen |Icon for the exit fullscreen button |fullscreen |N/A |
|cssFullscreen |Icon for the enter fullscreen button (CSS) |cssFullscreen |Only effective when CSS fullscreen is enabled |
|exitCssFullscreen |Icon for the exit fullscreen button (CSS) |cssFullscreen |Only effective when CSS fullscreen is enabled |
|pipIcon |Icon for the picture\-in\-picture button in the control bar |pip |N/A |
|pipIconExit |Icon for the exit picture\-in\-picture button in the control bar |pip |N/A |
|volumeSmall |Icon for the volume button when volume is low |volume |N/A |
|volumeLarge |Icon for the volume button when volume is high |volume |N/A |
|volumeMuted |Icon for the volume button when muted |volume |N/A |
|rotate |Icon for the video rotation button |rotate |N/A |
|download |Icon for the download button |download |Only effective when playing MP4 format videos |
|seekTipIcon |Icon displayed during seeking |mobile |Only effective on mobile devices |
|playNext |Icon for the next episode button |playNext |N/A |
|danmuSetting |Icon for the danmaku settings button |danmuPlugin |N/A |
|openDanmu |Icon for the open danmaku badge |danmuPlugin |N/A |
|closeDanmu |Icon for the close danmaku badge |danmuPlugin |N/A |
|vttSubOpen |Icon for the open external subtitle button |Subtitle |N/A |
|vttSubClose |Icon for the close external subtitle button |Subtitle |N/A |


<span id="d4b6095f"></span>
## Method 3: Override CSS Styles

You can override the styles by adding your own CSS. The following example shows how to move the play button in the center of the player to the bottom left corner, change the draggable button of the progress bar, and modify the background style of the bottom control bar.

```CSS
.xgplayer .xgplayer-controls {
    background-color: #7fd3f0;
    background-image: none;
}
.xgplayer .xgplayer-start {
    left: 50px;
    bottom: 50px;
    top: unset;
}
.xgplayer-pc .xgplayer-progress .xgplayer-progress-btn {
    width: 24px;
    height: 24px;
    box-shadow: none;
    background:none;
}
.xgplayer .xgplayer-progress-btn:before {
    background-image: url("https://p6-addone.***img.com/tos-cn-i-hhc0kcolqq/0689ad58f2a9478****9eac7fecc02.png~tplv-hhc0kcolqq-image.image");
    background-size: 100% 100%;
    background-color: transparent;
    width: 20px;
    height: 20px;
}
```


Example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7779e88764694ca987d0ce20faa0a002~tplv-goo7wpa0wc-image.image) </span>
