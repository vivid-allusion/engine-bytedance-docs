---
title: "Managing Traffic Mirror Target"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-target"
---

<span id="AKm7umY0"></span>
## Create Traffic Mirror Target

<span id=".5pON5L2c6K-05piO"></span>
### Action description

The quota for Mirror Targets is 10,000 per account per region.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Target**.

3. Click **Create Mirror Target**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of Traffic Mirror Target. |Target\-A |
   |Target type |Select the type of Traffic Mirror Target; currently supports Network Interface and Cloud Load Balancer (CLB). |Network interface |
   |Target Instance​​ |Select the Traffic Mirror Target instance from the dropdown list. |Target\-ENI |
   |Related project |Select the project to which the Traffic Mirror Target belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tags |Add one or more custom tags to the Traffic Mirror Target as needed.<br><br>A tag consists of a Tag Key and a Tag Value, and is used to categorize and organize Mirror Targets. For more information, see Tag management.<br><br>Click the add icon to add multiple tags. |Target:v1 |
   

5. Click **Create** to complete the action.


<span id=".5L-u5pS56ZWc5YOP55uu55qE"></span>
## Modify Traffic Mirror Target

You can refer to this procedure to modify the name and description of a Mirror Target.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Target**.

3. Click the **Edit** icon on the right side of the target traffic mirror target.

4. Modify the name and description of the traffic mirror target as needed.

5. Click **Save** to complete the action.


<span id=".5Yig6Zmk6ZWc5YOP55uu55qE"></span>
## Delete Traffic Mirror Target

**Prerequisites**

The traffic mirror target is not associated with any traffic mirror sessions. If attached, delete the [traffic mirror session](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session#.5Yig6Zmk6ZWc5YOP5Lya6K-d) first.

**Procedures**


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Traffic Mirror \> Mirror Target**.

3. Click **Delete** on the right of the traffic mirror target to be deleted.

4. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorTarget)

* [ModifyTrafficMirrorTargetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorTargetAttributes)

* [DeleteTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorTarget)
