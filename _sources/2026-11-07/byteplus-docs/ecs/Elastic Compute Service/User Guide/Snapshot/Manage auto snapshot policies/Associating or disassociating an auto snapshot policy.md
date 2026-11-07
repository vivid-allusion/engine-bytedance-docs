---
title: "Associating or disassociating an auto snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Associate-Cancel-an-auto-snapshot-policies-for-volume"
---

This topic explains how to apply or remove an auto snapshot policy for a volume.

<span id=".5Li65LqR55uY5YWz6IGU6Ieq5Yqo5b-r54Wn562W55Wl"></span>
## Associating an auto snapshot policy with a volume

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

You have created an auto snapshot policy. For more information, see [Creating an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Create-an-auto-snapshot-policy).

<span id=".5rOo5oSP5LqL6aG5"></span>
### Notes


|Category |Considerations |
|---|---|
|Number of associations |* Each volume can be associated with only one auto snapshot policy.<br><br>* A single auto snapshot policy can be applied to multiple volumes. |
|Volume type |You can only associate an auto snapshot policy with ESSD volumes. |
|Volume status |After an auto snapshot policy is associated with a volume, the system will create automatic snapshots only if the following conditions are met:<br><br><br>* The volume must be an ESSD volume.<br><br>* The volume is either "Available" or "Attached".<br><br>* If the volume is "Attached", the instance it is attached to must be either "Running" or "Stopped". |


<span id=".5Zyo6Ieq5Yqo5b-r54Wn562W55Wl5YiX6KGo5YWz6IGU"></span>
### From the Auto Snapshot Policies tab


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the auto snapshot policy resides.

4. On the "Snapshots" page, click the "Auto Snapshot Policies" tab.

5. On the "Auto Snapshot Policies" tab, click "Associate volume" in the "Actions" column of the policy you want to manage.

6. In the side panel that appears, click the "Volume unassociated with this policy" tab. Then, select the volume that you want to associate with the policy and click "Associate".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a volume is already associated with an auto snapshot policy, you must first disassociate the existing policy before you can associate a new one. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Associate-Cancel-an-auto-snapshot-policies-for-volume#.5Li65LqR55uY5Y-W5raI6Ieq5Yqo5b-r54Wn562W55Wl">Disassociating an auto snapshot policy from a volume</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the association between volumes and auto snapshot policies using the following methods:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Navigate to the "Volume associated with this policy" tab of an auto snapshot policy to find all the volumes associated with it.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Navigate to the "Overview" tab of a volume to view the auto snapshot policy associated with it.   </div>
   


<span id=".5Zyo5LqR55uY6K-m5oOF6aG16Z2i5YWz6IGU"></span>
### From the Overview tab


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" tab, click the volume you want to manage.

5. On the "Overview" tab, locate the "Volume information" section. Then click "apply policy" under "Auto snapshot policy".

6. In the "Apply auto snapshot policy" dialog, select the project and the desired snapshot policy. Then, click "Apply auto snapshot policy".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a volume is already associated with an auto snapshot policy, you must first disassociate the existing policy before you can associate a new one. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Associate-Cancel-an-auto-snapshot-policies-for-volume#.5Li65LqR55uY5Y-W5raI6Ieq5Yqo5b-r54Wn562W55Wl">Disassociating an auto snapshot policy from a volume</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the association between volumes and auto snapshot policies using the following methods:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Navigate to the "Volume associated with this policy" tab of an auto snapshot policy to find all the volumes associated with it.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Navigate to the "Overview" tab of a volume to view the auto snapshot policy associated with it.   </div>
   


<span id=".5Li65LqR55uY5Y-W5raI6Ieq5Yqo5b-r54Wn562W55Wl"></span>
## Disassociating an auto snapshot policy from a volume


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the auto snapshot policy resides.

4. On the "Snapshots" page, click the "Auto Snapshot Policies" tab.

5. On the "Auto Snapshot Policies" tab, click "Associate volume" in the "Actions" column of the policy you want to manage.

6. In the side panel that appears, click the "Volume associated with this policy" tab. Then, select the volume that you want to disassociate from the policy and click "Remove".
