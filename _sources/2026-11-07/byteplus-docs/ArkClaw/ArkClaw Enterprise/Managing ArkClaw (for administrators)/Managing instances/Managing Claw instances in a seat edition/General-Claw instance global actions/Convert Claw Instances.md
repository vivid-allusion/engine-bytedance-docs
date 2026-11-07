---
title: "Convert Claw Instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Exporting_the_Claw_instance_list"
---

The administrator can export instance data from the Claw list to a local file for offline viewing, statistical analysis, or archiving and backup. **This topic describes how to export all or filtered Claw instance lists.** 

<span id="RosOOBu3"></span>
## Scenario

When the administrator needs to perform bulk auditing, personnel inventory, data archiving, or integration with other systems for Claw instances within the enterprise, the export feature can be used to export the Claw instance list to a local file.

<span id="RCWcnViT"></span>
## Procedure


1. Log in to [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/).

2. In the left navigation pane, click "Claw Management" \> "Claws".

3. On the "Instances" tab, the list of employee Claw/shared Claw instances that have been created is displayed.

4. In the upper\-right corner of the list, click "Convert current list".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The "Export current list" button exports information about all existing Claw instances created.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To convert instances based on specific conditions, first use the search or filter feature to narrow the range, select the target instances that have been filtered, and then click the "Convert" button in the batch actions bar at the bottom of the page.   </div>
   

5. Select the fields to be exported.

   The converted file can contain the following field information. Select the necessary fields according to actual needs.

   
   |**Field** |Description |
   |---|---|
   |Name/ID |The name and unique ID of the Claw instance; this is a required field for Convert. |
   |State |The current status of the Claw instance, such as "Running", "InActive", and so on. |
   |Tag |Custom type tags defined by the administrator, which can be used to classify and filter instances by business line, project, or team. |
   |User |The name of the enterprise employee to whom the Claw instance belongs. |
   |User email |The enterprise email address of the user to whom the instance belongs. |
   |Department |The name of the organization department to which the user belongs, making it easier to analyze the distribution of instances by organizational structure. |
   |Seat grade |The current seat grade of the Claw instance determines the range of available models and compute specifications. |
   |Creation time |The time when the Claw instance was created. |
   

6. Wait for the system to generate the exported file. Once the file is generated, it will be automatically downloaded to the local device.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The file format for conversion is <code>.xlsx</code> (Excel), encoded in UTF\-8. If the number of instances is large, the conversion process may take several seconds. Please wait patiently.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The converted data contains employee names, email addresses, department information, and more. Please keep the converted file properly to prevent data leakage.   </div>
