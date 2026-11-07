---
title: "Configuring general settings"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-general-settings"
---

General settings define the core operational parameters and underlying detection architecture for the Endpoint Security antivirus module. By configuring scanning limits, antivirus engines, signature update frequencies, and user trust zone permissions, administrators can optimize endpoint performance while ensuring timely threat identification.


1. Log in to the Admin Console.

2. In the left navigation bar, select **Endpoint Security** \> **Strategy Center**.

3. On the **Strategy Center** page, click the **General Settings** tab.

4. Refer to the following sections to adjust the configuration parameters based on your business requirements.

   * **Detection configuration**

      Configure scanning thresholds and data synchronization frequencies to balance endpoint scanning performance with real\-time security.

      
      |**Setting** |**Description** |
      |---|---|
      |**Scan file size** |Sets the maximum size for a single file to be scanned. This limit applies to individual files and excludes archives. **Recommendation**: Set to 200 MB or less to maintain system performance. |
      |**Enable compressed file scanning** |Specify whether the engine should decompress and scan archives. If enabled, you can set the recursion depth from 1 to 10 layers. Default: Enabled (5 layers). |
      |**Virus database update** |Sets how often the client checks for and downloads the latest virus signature updates. **Recommendation**: 4 hours. |
      |**Data reporting frequency** |Defines the frequency at which the client uploads collected virus events to the Admin Console. **Recommendation**: 1 minute to ensure real\-time visibility. |
      

   * **Trusted zone configuration**

      Define the intervention permissions for endpoint users regarding detection results, balancing security control with business flexibility.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This configuration only applies to desktop clients running version <strong>3.2.14</strong> or later.      </div>
      

      
      |**Setting** |**Description** |
      |---|---|
      |**Trusted zone management permissions** |Set whether to allow employees to add or remove trusted files and directories in the SealSuite client.<br><br><br>* **Enabled**: Grants endpoint users management permissions to configure their own trust zones. You can apply this to all objects or specify partial scopes by employee or device.<br><br>* **Disabled (default)** : Disables trust zone management for endpoint users. Users can only view policies distributed by administrators and cannot modify them. This prevents users or malicious programs from bypassing security protections. |
      


&nbsp;
