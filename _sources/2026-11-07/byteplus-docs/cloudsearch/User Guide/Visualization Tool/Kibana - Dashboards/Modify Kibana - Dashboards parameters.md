---
title: "Modify Kibana/Dashboards parameters"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Modifying-Kibana-parameters"
---

You can modify Kibana/Dashboards parameters according to business needs, such as session activity hold, session duration, and interface request timeout. This article describes how to modify Kibana/Dashboards parameters.

## Scenario

* Login status timeout expiration

   The **Session activity hold** parameter of Kibana/Dashboards is set to **Yes** by default, which means each page request extends the session validity period. When the Kibana/Dashboards frontend page remains open, it periodically reports interface indicators to the backend (Elasticsearch/OpenSearch), so the user login status will not expire.

   If you want to enhance environment security by enforcing session timeout expiration, set **Session activity hold** to **No** and configure **Session duration** as needed. Once the login duration reaches the session duration, the system will automatically log out.

   Set the session duration based on your business needs to balance security and convenience. Generally, a shorter session duration improves security but requires more frequent logins; a longer session duration offers better experience but may increase the risk of unauthorized use when unattended.

* Reduce backend 503 errors

   The default Kibana API request timeout is 30000 milliseconds, meaning a backend response exceeding 30 seconds triggers a `503 Request timed out` error.

   You can increase the API timeout based on business query needs to receive responses normally and reduce 503 errors.

* Switch between Chinese and English

   Kibana’s user interface language defaults to English; you can switch to Chinese according to business needs.

## Procedure

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation bar, select **Instance management \> Visulization configuration**, then click **edit** in **Configure parameters**.

5. In the **Edit parameter configuration** dialog, modify session duration, API request timeout, and other parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Session duration |Session duration defaults to 3,600,000 milliseconds (1 hour).<br><br>If you choose to set **session activity hold** to **no**, the user will automatically log out when the login duration reaches the session duration. |
   |Session activity hold |Whether to actively extend the session duration.<br><br><br>* Yes: default value; each page request will extend the session duration.<br><br>* No: does not actively extend the session duration. This configuration achieves session timeout; when the login duration reaches the **session duration**, the user will automatically log out. |
   |Request timed out |Interface request timeout duration defaults to 30000 milliseconds, meaning a `503 Request timed out` error occurs if the backend response time exceeds 30 seconds.<br><br>To receive responses normally and reduce 503 errors, increase the request timeout duration. |
   |Language |Select the language for the Kibana/Dashboards user interface. The Kibana/Dashboards user interface defaults to English, which you can switch to Chinese as needed. |

6. View parameter configuration progress.

   After confirming the modification of Kibana/Dashboards parameters, the instance status shows **updating**, and the backend will restart the visualization node. When the instance status shows **running**, the parameter changes have taken effect.
