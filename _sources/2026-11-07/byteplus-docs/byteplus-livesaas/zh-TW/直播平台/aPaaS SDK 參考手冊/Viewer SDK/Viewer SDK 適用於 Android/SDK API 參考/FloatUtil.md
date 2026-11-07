---
title: "FloatUtil"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/floatutil-zh-TW"
---

若要管理系統針對直播間功能的浮動視窗權限，可以使用 FloatUtil 類別。此工具類提供靜態方法，用於檢查您的應用程式是否擁有所需權限，並引導使用者前往系統設定頁面以授予權限。

<span id="4b3dc68a"></span>
## checkPermission

檢查應用程式是否擁有系統的浮動視窗權限。

```Java
public static boolean checkPermission(Activity activity) 
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|activity |Activity |直播間目前的 `Activity`。 |


**回傳值**


|資料型別 |說明 |
|---|---|
|Boolean |應用程式是否擁有系統的浮動視窗權限。<br><br><br>* `true`：應用程式已取得權限。<br><br>* `false`：應用程式尚未取得權限。 |


<span id="f53394dc"></span>
## requestPermission

若應用程式尚未取得浮動視窗權限，此方法會開啟系統設定頁面，讓使用者授予權限。

```Java
public static void requestPermission(Context context)
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|context |Context |直播間畫面的 `Context`。 |
