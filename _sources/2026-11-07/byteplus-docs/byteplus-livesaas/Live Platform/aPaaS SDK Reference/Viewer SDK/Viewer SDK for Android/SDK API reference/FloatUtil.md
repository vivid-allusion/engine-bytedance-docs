---
title: "FloatUtil"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/floatutil"
---

The utility class for the floating window in a live room.

<span id="4b3dc68a"></span>
## checkPermission

Checks whether the app has the system's floating window permission.

```Java
public static boolean checkPermission(Activity activity) 
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|activity |Activity |The Activity of the live room. |


**Return value**


|Data Type |Description |
|---|---|
|Boolean |Whether the app has the system's floating window permission.<br><br><br>* `true`: The app has the permission.<br><br>* `false`: The app does not have the permission. |


<span id="f53394dc"></span>
## requestPermission

When the app does not have the floating window permission, it redirects to the system's page to request this permission. This method only takes effect when the app does not have the floating window permission.

```Java
public static void requestPermission(Context context)
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |
