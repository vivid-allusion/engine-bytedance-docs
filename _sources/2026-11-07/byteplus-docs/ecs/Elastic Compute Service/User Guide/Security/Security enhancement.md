---
title: "Security enhancement"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Security-enhancement"
---

ECS instances offer a security enhancement feature that provides real\-time monitoring and analysis of system activities. It generates alerts for risks detected during file and process monitoring, as well as threats like abnormal logins, helping reduce host intrusion risks and safeguard your hosts.

<span id=".6K6h6LS55pa55byP"></span>
## Billing method

You are not charged for using the security enhancement feature of ECS.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* When you create an instance by using a public image of Linux or Windows, security enhancement is enabled by default.

* Security enhancement is disabled by default in the following scenarios. 

   * When you create an instance by using a custom image or switching to any other image, security enhancement is disabled by default.

   * When you change a public image of Linux or Windows to a custom image, security enhancement is disabled by default.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="6reecnZP"></span>
### Enable security enhancement when you create an instance


1.  Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project of the target instance.

4. Click the "Create instance" button.

5. In the "Image" section of the "Basic configuration" step, select "Security enhancement" (selected by default). The system automatically installs the security enhancement feature for new instances.

6. Configure the remaining parameters based on your business requirements. For more information, see [Purchasing instances via wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

<span id=".5p-l55yL5a6J5YWo54q25oCB"></span>
### View security status

The colors of the icons in the "Security" column on the Instances page indicate the security enhancement status of each instance. The following table describes the mappings between the icon colors and the status.


|Security enhancement |Icon |Description |
|---|---|---|
|Enabled |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_807709ffba4269117ade174d04eda840.png) </span> |The instance security score is greater than or equal to 70, which indicates that the instance is secure. |
||<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa6cacaf3c96d0c821f9af29b386d30d.png) </span> |The instance security score is greater than or equal to 35 and less than 70, which indicates that the ECS instance has vulnerabilities or security alerts. |
||<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dcc5fdca04f8949a6b0f087727d15830.png) </span> |The instance security score is less than 35, which indicates that the ECS instance has vulnerabilities or severe security alerts. |
|Disabled |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b1a7d1785f65346ea640d5940713ba1.png) </span> |Security enhancement is not enabled.  |
