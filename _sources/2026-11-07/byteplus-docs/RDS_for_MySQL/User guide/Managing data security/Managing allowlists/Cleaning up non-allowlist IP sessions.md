---
title: "Cleaning up non-allowlist IP sessions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Cleaning_up_non-allowlist_IP_sessions"
---

This topic describes how to clean up non\-allowlist IP sessions for an instance.

<span id="xQnLdOIr"></span>
## Background

Sessions and connections initiated from IP addresses removed from an allowlist are not actively closed at the server level. To ensure data security, RDS for MySQL provides the non\-allowlist IP session cleanup feature.

<span id="dX9Azvr1"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="M44L5vd7"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the instance in the upper\-left corner of the top menu bar.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. Click the **Security** tab at the top of the page.

5. On the **Allowlists** subtab, click **Clean up non\-allowlist IP sessions** in the upper\-right corner.

6. In the **Non\-allowlist IP session cleanup** dialog box, sessions from host IPs not included in the allowlists associated with the instance are displayed (if any). Click **OK** to complete the cleanup.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that all host IPs required by your business are added to the allowlists to prevent business abnormalities.   </div>
