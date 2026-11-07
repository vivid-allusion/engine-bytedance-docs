---
title: "Enabling detection"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Enabling-detection"
---

To activate real\-time security protection for your cloud assets like ECS, CLB, and NAT gateways, you can use the NDR detection switch. This guide provides step\-by\-step instructions on how to sync your assets and enable the detection function, ensuring their traffic is continuously inspected for threats. The detection switch page enables you to enable or disable protection for your assets. You can sync your ECS, CLB, and NAT gateway asset IP addresses on the cloud to this page either automatically or manually. After asset sync is completed, you can enable NDR detection for the assets as needed. Once the detection function is enabled or disabled for an asset, NDR starts security detection and protection for the asset immediately.

<span id="7a83d4c3"></span>
## Notes

To protect your assets, we recommend enabling or disabling detection as needed. Once detection is disabled, traffic to the asset won't be inspected by NDR. Please proceed with caution.

<span id="7d8f6fd2"></span>
## Procedure


1. Log in to the NDR console.

2. In the left navigation pane, select **System settings** \> **Detection Switch**.

3. Click **Sync assets**.

   The NDR system will automatically sync the assets under your account.

4. After the sync is complete, select an asset to enable detection.

   * Enable detection for a single asset

      Enable detection for the asset instance.

   * Enable detection for multiple assets

      Select multiple assets and click **Turn on protection**.

5. Click **Confirm**.

   Once you enable detection, the traffic from all the selected public IP addresses will be inspected by NDR to protect your services and assets in real time.
