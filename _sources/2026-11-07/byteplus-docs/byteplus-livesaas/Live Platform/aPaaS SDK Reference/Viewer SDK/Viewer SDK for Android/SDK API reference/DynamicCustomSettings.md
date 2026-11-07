---
title: "DynamicCustomSettings"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/dynamiccustomsettings"
---

The dynamic configuration class for the live room.

```Java
public class DynamicCustomSettings
```


<span id="c2ac86df"></span>
## Member Functions

<span id="fda4e1e5"></span>
### setFollowText

Sets the button text when the host is not followed.

```Java
public void setFollowText(String followText)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|followText |String |The button text when the host is not followed. |


<span id="d808165a"></span>
### setFollowedText

Sets the button text when the host is followed.

```Java
public void setFollowedText(String followedText)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|followedText |String |The button text when the host is followed. |


<span id="f5babe29"></span>
### setFollowBackgroundImage

Sets the background image of the button when the host is not followed.

```Java
public void setFollowBackgroundImage(Drawable followBackgroundImage)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|followBackgroundImage |Drawable |The background image of the button when the host is not followed. |


<span id="b742d351"></span>
### setFollowedBackgroundImage

Sets the background image of the button when the host is followed.

```Java
public void setFollowedBackgroundImage(Drawable followedBackgroundImage)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|followedBackgroundImage |Drawable |The background image of the button when the host is followed. |


<span id="55766bef"></span>
### setBdlUserFollowListener

Sets the listener for the event of a viewer following the host in custom authentication mode.

```Java
public void setBdlUserFollowListener(BDLUserFollowListener bdlUserFollowListener)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|bdlUserFollowListener |BDLUserFollowListener |The listener for the event of a viewer following the host in custom authentication mode. For more information, see [BDLUserFollowListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#35d14b67). |


<span id="8682c301"></span>
### setInputBoxPrompt

Sets the placeholder text of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxPrompt(String inputBoxPrompt)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxPrompt |String |The placeholder text of the comment text box in non\-editing status, namely when the keyboard is not popped up. |


<span id="04aa818c"></span>
### setInputBoxPromptColor

Sets the placeholder text color of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxPromptColor(int inputBoxPromptColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxPromptColor |Integer |The placeholder text color of the comment text box in non\-editing status, namely when the keyboard is not popped up. |


<span id="4a693500"></span>
### setInputBoxBackgroundColor

Sets the background color of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxBackgroundColor(int inputBoxBackgroundColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxBackgroundColor |Integer |The background color of the comment text box in non\-editing status, namely when the keyboard is not popped up. |


<span id="740ee52f"></span>
### setInputBoxCornerRadius

Sets the corner radius of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxCornerRadius(int inputBoxCornerRadius)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxCornerRadius |Integer |The corner radius of the comment text box in non\-editing status, namely when the keyboard is not popped up. Default value: `19`. Unit: dp. |


<span id="0e05259a"></span>
### setInputBoxBorderWidth

Sets the border width of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxBorderWidth(int inputBoxBorderWidth)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxBorderWidth |Integer |The border width of the comment text box in non\-editing status, namely when the keyboard is not popped up. Default value: `0`. Unit: dp. |


<span id="f81a58ab"></span>
### setInputBoxBorderColor

Sets the border color of the comment text box in non\-editing status, namely when the keyboard is not popped up.

```Java
public void setInputBoxBorderColor(int inputBoxBorderColor)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inputBoxBorderColor |Integer |The border color of the comment text box in non\-editing status, namely when the keyboard is not popped up. |


<span id="71fed577"></span>
### setCommentEditingListener

Sets the event interception listener for the comment text box.

```Java
public void setCommentEditingListener(CommentEditingListener commentEditingListener)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentEditingListener |CommentEditingListener |The event interception listener for the comment text box. For more information, see [CommentEditingListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#e2b06336). |
