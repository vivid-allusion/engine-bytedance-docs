---
title: "FAQ"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/FAQ"
---

* [Why are IAM users unable to view Vortex IP services in the console?](https://docs.byteplus.com/en/docs/147/72771#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5Zyo5o6n5Yi25Y-w5p-l55yLVm9ydGV4IElQ5pyN5Yqh77yf)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/147/72771#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [How to view Vortex IP bandwidth?](https://docs.byteplus.com/en/docs/147/72771#.5aaC5L2V5p-l55yLVm9ydGV4IElQ5bim5a6977yf)

* [How to modify Vortex IP bandwidth?](https://docs.byteplus.com/en/docs/147/72771#.5aaC5L2V5L-u5pS5Vm9ydGV4IElQ5bim5a6977yf)


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5Zyo5o6n5Yi25Y-w5p-l55yLVm9ydGV4IElQ5pyN5Yqh77yf"></span>
## Why are IAM users unable to view Vortex IP services in the console?

The root user must grant the IAM user permissions related to Vortex IP services. IAM users with **FastTrackReadOnlyAccess** or **FastTrackFullAccess** permissions can view or use Vortex IP services in the console. Refer to [Managing users](https://docs.byteplus.com/en/docs/6257/64977#%E7%AE%A1%E7%90%86%E7%94%A8%E6%88%B7) to authorize the IAM user.

<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

If an IAM user has Vortex IP permissions and wants to view monitoring data, the root user of the BytePlus account to which the IAM user belongs must also grant the required permissions on cloud monitor to the IAM user.


1. Log in to the [BytePlus Identity and Access Management (IAM)](https://console.byteplus.com/iam/identitymanage/user) with the root user of the IAM user.

2. In the left\-side navigation pane, click User.

3. On the User page, click the name of the IAM user. The User details page appears.

4. Navigate to **Policy** \> **Global policy**, then click **Add Permission** to attach the default VCM policies to the IAM user as needed.

   
   |Policy Name |Supported Operations |
   |---|---|
   |CloudMonitorFullAccess |Management permissions on VCM. This policy not only allows an IAM user to query monitoring data, but also allows an IAM user to manage VCM. When granted this permission, the IAM user can not only view monitoring data, but also use VCM. |
   |CloudMonitorReadOnlyAccess |Access permissions on VCM. This policy allows an IAM user to view monitoring data. When granted with this permission, the IAM user can only view monitoring data. |
   


<span id=".5aaC5L2V5p-l55yLVm9ydGV4IElQ5bim5a6977yf"></span>
## How to view the bandwidth of Vortex IP?


1. Log in to the [Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. In the Instances, click the name/ID of the target Vortex IP.

3. View the bandwidth limit in the **More Information** section of the instance Overview interface.


<span id=".5aaC5L2V5L-u5pS5Vm9ydGV4IElQ5bim5a6977yf"></span>
## How to modify the bandwidth of Vortex IP?

The bandwidth of Vortex IP can be modified. Please refer to [Modify Bandwidth Limit](https://docs.byteplus.com/en/docs/gavi-sept-test1/Changing_the_maximum_bandwidth).
