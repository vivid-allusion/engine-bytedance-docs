---
title: "Obtaining instance system logs and screenshots"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Obtaining-instance-system-logs-and-screenshots"
---

This topic describes how to view instance system logs and screenshots.

<span id="Gbd9K7Ph"></span>
## Usage notes


|Feature |Description |
|---|---|
|Obtain instance system logs |* This API action is only applicable to instances in the **Running** state.<br><br>* This feature is unavailable for bare metal instance types. For instance type details, refer to [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>* System logs are available for Linux instances only.<br><br>* Maximum size of system logs: 64 KB. |
|Obtain instance screenshot |* You can only obtain the instance screenshot of an instance in the **Running** state.<br><br>* This feature is unavailable for bare metal instance types. For instance type details, refer to [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>* You cannot obtain the instance screenshot of a Windows instance that has the GRID driver installed. |


<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

When an instance encounters a failure, you need to identify the cause based on system logs and screen information. However, the failed instance can not be accessed remotely in most failure cases. Therefore, BytePlus offers you the feature to view instance system logs and screenshots. This allows you to obtain real\-time information in the ECS console or via OpenAPI.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="YN53rub8Us" title="Obtain instance system logs">
<TabTitle>Obtain instance system logs</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).   

2. In the top menu bar, select the region and project where the target instance resides.

3. In the left\-side navigation pane, select "Instances & Images \> Instances". The Instances page appears.

4. Select "... \> Operations and troubleshooting \> Obtain instance system logs" in the "Actions" column on the right side of the target instance for the system logs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d6bacfe34e95859d00611f3152456c3.png) </span>


</Tab>
<Tab zoneid="AMNHbjDDWh" title="Obtain instance screenshot">
<TabTitle>Obtain instance screenshot</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the top menu bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances". The Instances page appears.

4. Select "... \> Operations and troubleshooting \> Obtain instance screenshot" in the "Actions" column on the right side of the target instance for the screenshot.

   * Linux

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f0c5c5f69c727710a94616c7fddb89ed.png) </span>

   * Windows

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ae585e400356d7b354e7aefb61399a7.png) </span>


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [GetConsoleOutput](https://docs.byteplus.com/en/docs/ecs/GetConsoleOutput)

* [GetConsoleScreenshot](https://docs.byteplus.com/en/docs/ecs/GetConsoleScreenshot)
