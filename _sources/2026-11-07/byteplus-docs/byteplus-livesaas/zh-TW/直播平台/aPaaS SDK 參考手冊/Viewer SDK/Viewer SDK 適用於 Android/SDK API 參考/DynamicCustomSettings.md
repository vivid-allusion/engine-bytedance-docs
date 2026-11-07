---
title: "DynamicCustomSettings"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/dynamiccustomsettings-zh-TW"
---

DynamicCustomSettings 類別提供用於動態配置直播間使用者介面的相關方法。您可以使用此類別自訂主要互動元件的外觀與行為，例如關注按鈕與評論輸入框。這包括設定文字、顏色、背景，以及註冊用戶操作的監聽器，例如關注主播或編輯評論。

```Java
public class DynamicCustomSettings
```


<span id="c2ac86df"></span>
## 成員函式

<span id="fda4e1e5"></span>
### setFollowText

設定未關注主播時按鈕的文字。

```Java
public void setFollowText(String followText)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|followText |String |未關注主播時按鈕的文字。 |


<span id="d808165a"></span>
### setFollowedText

設定已關注主播時按鈕的文字。

```Java
public void setFollowedText(String followedText)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|followedText |String |已關注主播時按鈕的文字。 |


<span id="f5babe29"></span>
### setFollowBackgroundImage

設定未關注主播時按鈕的背景圖片。

```Java
public void setFollowBackgroundImage(Drawable followBackgroundImage)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|followBackgroundImage |Drawable |未關注主播時按鈕的背景圖片。 |


<span id="b742d351"></span>
### setFollowedBackgroundImage

設定已關注主播時按鈕的背景圖片。

```Java
public void setFollowedBackgroundImage(Drawable followedBackgroundImage)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|followedBackgroundImage |Drawable |已關注主播時按鈕的背景圖片。 |


<span id="55766bef"></span>
### setBdlUserFollowListener

設定自訂驗證模式下觀眾關注主播事件的監聽器。

```Java
public void setBdlUserFollowListener(BDLUserFollowListener bdlUserFollowListener)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|bdlUserFollowListener |BDLUserFollowListener |自訂驗證模式下觀眾關注主播事件的監聽器。如需詳細資訊，請參見[BDLUserFollowListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#35d14b67)。 |


<span id="8682c301"></span>
### setInputBoxPrompt

設定評論輸入框在非編輯狀態下的預設提示文字。

```Java
public void setInputBoxPrompt(String inputBoxPrompt)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|inputBoxPrompt |String |評論輸入框在非編輯狀態下的預設提示文字。 |


<span id="04aa818c"></span>
### setInputBoxPromptColor

設定評論輸入框在非編輯狀態（即鍵盤未彈出時）預設提示文字的顏色。

```Java
public void setInputBoxPromptColor(int inputBoxPromptColor)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|inputBoxPromptColor |Integer |評論輸入框在非編輯狀態下的預設提示文字顏色。 |


<span id="4a693500"></span>
### setInputBoxBackgroundColor

設定評論輸入框在非編輯狀態（即鍵盤未彈出時）的背景顏色。

```Java
public void setInputBoxBackgroundColor(int inputBoxBackgroundColor)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|inputBoxBackgroundColor |Integer |評論輸入框在非編輯狀態下的背景顏色。 |


<span id="740ee52f"></span>
### setInputBoxCornerRadius

設定評論輸入框在非編輯狀態（即鍵盤未彈出時）的圓角半徑。

```Java
public void setInputBoxCornerRadius(int inputBoxCornerRadius)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|inputBoxCornerRadius |Integer |評論輸入框在非編輯狀態下的圓角半徑。預設值：`19`。單位：dp。 |


<span id="0e05259a"></span>
### setInputBoxBorderWidth

設定評論輸入框在非編輯狀態（即鍵盤未彈出時）的邊框寬度。

```Java
public void setInputBoxBorderWidth(int inputBoxBorderWidth)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|inputBoxBorderWidth |Integer |評論輸入框在非編輯狀態下的邊框寬度。預設值：`0`。單位：dp。 |


<span id="f81a58ab"></span>
### setInputBoxBorderColor

設定評論輸入框在非編輯狀態（即鍵盤未彈出時）的邊框顏色。

```Java
public void setInputBoxBorderColor(int inputBoxBorderColor)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|inputBoxBorderColor |Integer |評論輸入框在非編輯狀態下的邊框顏色。 |


<span id="71fed577"></span>
### setCommentEditingListener

設定評論輸入框的事件攔截監聽器。

```Java
public void setCommentEditingListener(CommentEditingListener commentEditingListener)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|commentEditingListener |CommentEditingListener |評論輸入框的事件攔截監聽器。如需詳細資訊，請參見[CommentEditingListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#e2b06336)。 |
