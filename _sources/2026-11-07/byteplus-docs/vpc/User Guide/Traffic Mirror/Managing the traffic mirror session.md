---
title: "Managing the traffic mirror session"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session"
---

## Create a traffic mirror session

**Prerequisites**

* A Traffic Mirror Target already exists. If not, [Create a Mirror Target](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-target).

* A Traffic Mirror Filter already exists. If not, [Create a Mirror Filter](https://docs.byteplus.com/en/docs/vpc/Managing-traffic-mirror-filter).

**Instructions**

* A single account supports creating up to 1,000 mirror sessions in a single region.

* Each mirror session can only be associated with one Mirror Site, one Traffic Mirror Target, and one Traffic Mirror Filter.

**Procedure**

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Session**.

3. Click **Create Traffic Mirror Session**.

4. Configure parameters based on the table below.

   |Parameters |Description |Sample value |
   |---|---|---|
   |Name |Enter the mirror session name. |Session\-X |
   |Mirror site |Select the mirror site from the dropdown list. Supports selecting the primary network interfaces (ENIs) or secondary ENIs already attached to ECSs.<br><br>> **tip**<br><br><br>> Only the primary and secondary network interfaces of ECSs with the following specifications are supported as mirror sites: g1ie, g3il, g3al, c1ie, c3il, c3al, r1ie, r3il, r3al, i2, i2g, d2, d2c, d2s, hfr2, hfg2, hfc2, g2ine, t2, s2. For more restrictions, see [Limits](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview#.5L2_55So6ZmQ5Yi2).<br> |ECS\-A\-eni\-1 |
   |Traffic mirror target |Select the Traffic Mirror Target from dropdown list. |Target\-X |
   |Priority |Set the priority of mirror session. The value range is 1 to 32766, and priority must be unique. Lower numbers have higher priority. |1 |
   |VNI |Set the VNI for the mirror session to distinguish traffic from different mirror sessions at the Mirror Target. The value range is 1–16777215, and the VNI must be unique. |1234 |
   |Packet size |The packet size for Traffic Mirror is configurable as needed. The minimum range is 64 bytes, and the recommended range is 64 to 1450 bytes. If not specified, the default value is 1500 bytes.<br><br>> **tip**<br><br><br>> If the set packet size is < the MTU of the mirror site or \> 1450, some packets may be truncated and the truncated content discarded. To ensure packets are not truncated, it is recommended to set the packet size and the [ENI MTU value](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface) according to the following relationship:<br><br><br>> The MTU of the mirror site ≤ the packet size set in the mirror session ≤ the MTU of the Mirror Target \- 50, and the packet size set in the mirror session must be ≤ 1450.<br> |1000 |
   |Mirror filter |Select Traffic Mirror Filter from the dropdown list. |Filter\-X |
   |Session management status |Start traffic mirror session<br><br><br>* **Enabled**: The mirror session starts replicating traffic, and the corresponding billing item takes effect immediately and starts charging.<br><br>* **Disabled**: The mirror session does not replicate traffic, and the corresponding billing item does not take effect and is not billed. To enable it later, see [Enabling the Traffic Mirror](https://docs.byteplus.com/en/docs/vpc/Starting-Stoping-a-traffic-mirror-session). |Enable |
   |Project |Select the project to which the mirror session belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tag |Add one or more custom tags to the Traffic Mirror Session as needed. A tag consists of a Tag Key and a Tag Value, and is used to categorize and organize Mirror Sessions. For more information, see [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags).<br><br>Click the add icon to add multiple tags. |Session:v1 |

5. Click **Buy now** to complete the action.

## Modify traffic mirror session

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Session**.

3. Click **Modify** on the right side of the target traffic mirror session.

4. Modify the name, description, mirror site, Traffic Mirror Target, priority, VNI, packet size, and Traffic Mirror Filter as needed.

5. Click **Buy now** to complete the action.

## Delete a traffic mirror session

> **tip**

> When you release the mirror source network interface, its attached traffic mirror session will be synchronized and deleted.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Session**.

3. Click **Delete** on the right side of the target traffic mirror session.

4. Click **Delete** to complete the action.

## Related documentation

* [CreateTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorSession)

* [ModifyTrafficMirrorSessionAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorSessionAttributes)

* [DeleteTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorSession)
