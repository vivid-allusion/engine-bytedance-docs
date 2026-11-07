---
title: "Dev boxes lifecycle management"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Dev_boxes_lifecycle_management"
---

The life cycle of a Dev box refers to the state experienced by an instance of a Dev box from creation to deletion. In different states, the login and operation of Dev boxes may vary. This paper introduces Dev boxes state description and state transition description.

Dev boxes state is divided into stable state and intermediate state according to properties. The intermediate state is the state in which the instance is temporarily in before reaching a stable state. If the developer is in the intermediate state for a long time, it indicates that there is an abnormality.

The possible states in the life cycle of a Dev box are shown in the table below.

<span id="开发机状态说明"></span>
## Dev boxes status description


|Status |Status attribute |Status description |Supported action items |
|---|---|---|---|
|Creating |Intermediate state |New Dev boxes are created and the instance is about to start. |* "Shutdown": Support closing Dev boxes that are being created;<br><br>* "Delete": Supports deleting Dev boxes. |
|Queueing |Intermediate state |Dev boxes are waiting for resources due to insufficient resources. |* "Shutdown": Support closing queued Dev boxes;<br><br>* "Delete": Supports deleting Dev boxes. |
|Deploying |Intermediate state |Create a new Dev box, or perform a boot or restart operation on an existing Dev box, and the Dev box instance is about to enter the Running state. |* "Shutdown": Supports closing Dev boxes that are being deployed;<br><br>* "Delete": Supports deleting Dev boxes. |
|Running |Steady state |The instance is in the running state. |* "Edit": Support editing name and description information; support expanding cloud disk capacity; support modifying access configuration information, including adding ports and enabling SSH remote access;<br><br>* "Shutdown": Support closing the running Dev boxes;<br><br>* "Restart": Support restarting Dev boxes;<br><br>* "Login": Support logging in to Dev boxes through VPC/public network modes, and also support logging in to Dev boxes using WebIDE or SSH remote access respectively;<br><br>* "Delete": Support deleting Dev boxes;<br><br>* Save image: Supports saving the current development environment as an image. |
|Shutdown |Intermediate state |The instance is in a shutdown state, and computing resources are released after shutdown. |*  |
|Turned off |Steady state |The instance is in a shutdown state and cannot connect to the Dev boxes. |* "Edit": Support editing name and description information; support expanding cloud disk capacity; support modifying access configuration information, including increasing ports and enabling SSH remote access; support modifying shared storage mounts; support updating queues and their calculation specifications;<br><br>* "Boot": Support opening closed Dev boxes;<br><br>* "Delete": Supports deleting Dev boxes. |
|Deleting |Intermediate state |The instance is in the state of being deleted. |*  |
|Image saving |Intermediate state |If you initiate a "mirror save" operation on the environment of the Dev boxes, the sub\-state "mirror save" during the build process. During the image saving process, it is not recommended to do any operation on the Dev boxes, otherwise it will cause the development organization to fail to build the image. |*  |
|Upgrading |Intermediate state |If some system versions of the Dev boxes are upgraded, they will enter the upgrade state after clicking Power. |* "Delete": Supports deleting Dev boxes. |
|Failed to create |Steady state |Dev boxes are in an abnormal state and can be turned on again. |* "Edit": Support editing name and description information;<br><br>* "Boot": Support trying to boot again;<br><br>* "Delete": Supports deleting Dev boxes. |
|Abnormal |Steady state |Dev boxes are in an abnormal state. |* "Delete": Supports deleting Dev boxes. |


<span id="开发机状态转换说明"></span>
## Dev boxes state transition instructions

Dev boxes transition diagram of key states and operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0d08e92eb274c26bef059a6802d1a1c~tplv-goo7wpa0wc-image.image) </span>
