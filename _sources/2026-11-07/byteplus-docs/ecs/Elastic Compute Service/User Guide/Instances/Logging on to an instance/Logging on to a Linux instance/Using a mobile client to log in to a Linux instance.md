---
title: "Using a mobile client to log in to a Linux instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-a-mobile-client-to-log-on-to-a-Linux-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic describes how to log in to a Linux ECS instance when the local host uses the iOS or Android operating system.


|Operating system of the local host |Operating system of the ECS instance |Login tool on local host |Login authentication method |
|---|---|---|---|
|iOS |Linux |Termius\-SSH client |Password |
|Android |Linux |JuiceSSH |Password |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance to log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance is [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), and can communicate with the Internet.


<span id=".5a-G56CB55m75b2V5q2l6aqk"></span>
## Password login procedure


<Tabs>
<Tab zoneid="HXFqBa5s4e" title="iOS host">
<TabTitle>iOS host</TabTitle>

1. Download the Termius\-SSH client app from the App Store to your mobile device. Then, follow the prompts to create an account, log in, and set a password.

2. Open the app, and then tap "New Host".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bfda6e16a65e52baa82ea537b7f6ec4.png) </span>

3. Enter the login information for the Linux ECS instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3528bf9884ad9355ddc287c0cac77499.png) </span>

   * Label: Specify a name for this connection.

   * IP or Hostname: Input the EIP of the Linux ECS instance.

   * Use SSH: Turn on this option to enable SSH login.

   * Port: Input the port used by the Linux ECS instance. In this case, port 22 is used.

   * Username/Password: Input the username and password that are used to log in to the Linux ECS instance.

4. Tap "Save" to save the login information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_668c5bcf1f2caeceaf78742bee186fe0.png) </span>

5. Tap the added host to log in.


</Tab>
<Tab zoneid="m1T5qHkk5I" title="Android host">
<TabTitle>Android host</TabTitle>

1. Download the JuiceSSH app to your mobile. Then, follow the prompts to create an account, log in, and set a password.

2. Open the JuiceSSH app and tap "Manage Connections".

3. Tap the "+" icon. On the "New Identity" page, enter the credentials used to log in to the Linux ECS instance.

   * Nickname: Specify a name for this connection.

   * Username/Password: Input the username and password that are used to log in to the Linux ECS instance.

4. Tap the "Checkmark" icon in the upper\-right corner of the screen. On the "New Connection" page, continue to input the login information for the Linux ECS instance.

   * Address: Input the EIP of the Linux ECS instance.

   * Type: Select SSH.

   * Port: Input the port used by the Linux ECS instance. In this case, the port is 22.

5. Tap the "Checkmark" icon in the upper\-right corner to save this connection.

6. Double\-tap the added Linux ECS instance and then tap "ACCEPT" to log in to the target instance.


</Tab>
</Tabs>
