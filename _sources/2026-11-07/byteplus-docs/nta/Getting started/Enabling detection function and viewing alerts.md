---
title: "Enabling detection function and viewing alerts"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Getting-started-with-NTA"
---

To protect your services and assets with Network Detection and Response (NDR), you must first enable its detection capabilities. This guide shows you how to sync your assets to turn on protection and then view the resulting security alerts from both an asset and an alert perspective.

<span id="39ad4cce"></span>
## Prerequisites

Your service is already connected to NDR.

<span id="16238f64"></span>
## Step 1: Enable the detection function


1. Log in to the NDR console.

2. Select **System Settings** ＞ **Asset Center** on the left side of the page.

3. Click **Sync assets**.

   The NDR system will automatically sync the assets in your account.

4. After the sync is completed, select an asset to enable the detection function.

   * Enable detection for a single asset

      Enable the detection function for the asset.

   * Enable detection for multiple assets

      Select multiple assets and click **Turn on protection**.

5. Click **Confirm**.

   Once you enable the detection function, traffic from all selected public IP addresses will be inspected by NDR to protect your assets in real time.


<span id="9d989186"></span>
## Step 2: View alert information

You can view risks to your assets by asset or by alert.


* This view displays the total number of assets, categorized by risk level. Risk information is organized by asset.

* This view aggregates alert events of the same type. Information, such as source and destination IP addresses, is organized by alert.


<span id="9d989186"></span>
### Viewing risks by asset


1. Log in to the NDR console.

2. Select


**Threat center** ＞ **Asset perspective** on the left side of the page.


3. View asset risk information.

   Asset risk levels are modeled and evaluated based on factors such as the attack chains, number, types, and attack directions from security alerts unhandled in the last 7 days. The lower the asset score, the higher the likelihood of compromise, and the more urgently the asset requires attention.

   Different asset security scores correspond to different risk levels. For more information, refer to the table below.

   
   |Score |Level |
   |---|---|
   |100 |Security |
   |75–99 |Low risk |
   |50–74 |Moderate risk |
   |25–49 |High risk |
   |0–24 |Fatal |
   

4. Click an asset's IP address to open its details page.

   You can check the overview of security alerts affecting the asset and handle them.

   * **Handled manually**: The alert is handled by following the suggestions and then marked as **Handled manually**.

   * **Add to allowlist**: Add the source and destination IP addresses and destination port to the allowlist. Once configured, traffic from the source IP address to the specified destination IP address and port will no longer be inspected.


<span id="876b0461"></span>
### Viewing risks by alert


1. Log in to the NDR console.

2. Select **Threat center** ＞ **Alert perspective** on the left side of the page.

3. View alert information.

   Alert data in the last 24 hours is displayed by default. You can change the time range in the upper\-right corner of the page.

   * Alert statistics: This section shows statistics for different alert types, based on the number of alerts. You can sort security events by the number of alerts in descending order and collapse or hide certain alerts.

   * Alert trend: You can view the alert trend in real time and select a day with an abnormal number of alerts for targeted analysis. You can also collapse and hide certain alerts.

   * Alert list: The alerts include the time of the last occurrence, threat type, attack status, risk level, asset IP address, external IP address, port, protocol, attack direction, HTTP status code, and processing status.

4. In the alert list, click an event's threat type to open the alert details page.

   You can view all events of this alert type and handle them by following the suggested solution.

   * **Handled manually**: The alert is handled by following the suggestions and then marked as **Handled manually**.

   * **Add to allowlist**: Add the source and destination IP addresses and destination port to the allowlist. Once configured, traffic from the source IP address to the specified destination IP address and port will no longer be inspected.
