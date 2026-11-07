---
title: "Using a mobile client to log in to a Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-a-mobile-client-to-log-on-to-a-Windows-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

This topic describes how to log in to a Windows ECS instance when the local host uses the iOS or Android operating system.


|Local host OS |ECS instance OS |Local host login tool |Login authentication method |
|---|---|---|---|
|iOS |Windows |Windows APP Mobile |Password |
|Android |Windows |Remote Desktop |Password |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance you log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance is [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), and can communicate with the Internet.


<span id=".5a-G56CB55m75b2V5q2l6aqk"></span>
## Login with password

The following steps use iOS as an example. The procedure on Android is similar.


1. Download the "Windows APP Mobile" app from the App Store of the local host.

2. Open Windows APP Mobile and tap the "+" button at the top of the page.

3. On the "Add" page, tap the "PC" button.

3. Enter the login information for the Windows ECS instance on the cloud.

   * PC name: Enter the EIP of the ECS instance.

   * Credentials: Enter the ECS instance username "Administrator" and its corresponding password.

4. Tap the "Save" button to add the remote server.

5. Tap the added server to log in.
