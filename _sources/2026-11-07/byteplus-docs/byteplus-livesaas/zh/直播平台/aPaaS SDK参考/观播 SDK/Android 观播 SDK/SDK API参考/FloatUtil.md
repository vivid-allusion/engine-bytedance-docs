---
title: "FloatUtil"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/floatutil-zh-CN"
---

要管理直播间功能的系统悬浮窗权限，可以使用 FloatUtil 类。该工具类提供静态方法，用于检查你的应用是否具有所需权限，并可引导用户前往系统设置页面授予权限。

<span id="4b3dc68a"></span>
## checkPermission

检查应用是否具有系统悬浮窗权限。

```Java
public static boolean checkPermission(Activity activity) 
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|activity |Activity |直播间当前的 `Activity`。 |


**返回值**


|数据类型 |接口行为 |
|---|---|
|Boolean |应用是否具有系统悬浮窗权限。<br><br><br>* `true`：应用已获得权限。<br><br>* `false`：应用未获得权限。 |


<span id="f53394dc"></span>
## requestPermission

如果应用没有悬浮窗权限，该方法会打开系统设置页面，方便用户授予权限。

```Java
public static void requestPermission(Context context)
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|context |Context |直播间界面的 `Context`。 |
