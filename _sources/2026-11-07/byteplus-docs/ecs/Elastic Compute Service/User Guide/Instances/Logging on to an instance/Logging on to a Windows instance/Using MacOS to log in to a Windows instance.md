---
title: "Using MacOS to log in to a Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-MacOS-to-log-on-to-a-Windows-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

This topic describes how to log in to a Windows instance on the cloud when your local host runs the macOS operating system.


|Local host OS |ECS instance OS |Local host login tool |Login authentication method |
|---|---|---|---|
|macOS |Windows |Windows App |Password |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure that the ECS instance you log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* Make sure that the ECS instance is associated with an EIP, and can communicate with the Internet.

* If you need data transfer, refer to [Uploading a file from an on-premises macOS system to a Windows ECS instance by using MRD](https://docs.byteplus.com/en/docs/ecs/Using-MRD-to-upload-file-from-a-local-MacOS-to-a-Windows-instance).


<span id=".5a-G56CB55m75b2V5q2l6aqk"></span>
## Login with password


1. Download and install the Windows App client from the App Store on the local host.

2. Open Windows App and click the "+ \> Add PC" button in the upper right corner.

3. Enter the login information for the target Windows instance.

   * PC name: Enter the EIP of the ECS instance.

   * Retain the default settings for other parameters.

4. Double\-click the added server.

5. Enter the login username and password for the target instance, and then click the "Continue" button.

6. Verify the login credentials and click the "Continue" button to log in to the instance.
