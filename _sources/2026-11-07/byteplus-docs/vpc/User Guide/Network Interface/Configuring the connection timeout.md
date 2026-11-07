---
title: "Configuring the connection timeout"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-the-connection-timeout"
---

## Scenarios

You can modify the timeout for established TCP connections, the TCP wait and close timeout, and the UDP flow timeout.

* **Established TCP connection timeout period**: The maximum retention duration for a TCP connection with no data transmission. Upon timeout, the connection is automatically disconnected and session resources are released.

* **TCP wait and close timeout period**: The maximum waiting time for a response during the TCP four\-way handshake close process. If the handshake is not completed within the timeout, the connection is forcibly disconnected and session resources are released.

* **UDP flow timeout period**: The maximum idle retention duration for a bidirectional UDP session with no round\-trip traffic. Upon timeout, the session is automatically deleted and resources are released.

## Instructions

BytePlus official service Network Interfaces do not support timeout configuration.

## Procedure

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click the name of the target secondary network interface.

   * **Established TCP connection timeout period**:

      1. Click the edit icon next to **Established TCP connection timeout period** **.**

      2. Enter the timeout period. Value range: 30\-7200s.

   * **TCP wait and close timeout period**

      1. Click the edit icon next to **TCP wait and close timeout period** **.**

      2. Enter the timeout period. Value range: 3\-15 seconds.

   * **UDP flow timeout period**

      1. Click the edit icon next to **UDP flow timeout period** **.**

      2. Enter the timeout period. Value range: 10\-180 seconds.

5. Click **Confirm** to complete the action.

## Related documents

[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes)
