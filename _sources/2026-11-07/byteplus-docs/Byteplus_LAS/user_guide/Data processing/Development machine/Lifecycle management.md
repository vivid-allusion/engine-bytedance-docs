---
title: "Lifecycle management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Lifecycle_management"
---

The lifecycle of a development machine includes the transitions between different states from creation to deletion. The operations available for the development machine vary depending on its current state. This document describes the states of the development machine and the corresponding operational restrictions.

The states of a development machine are categorized by attribute as **stable states** and **intermediate states**. An intermediate state is a temporary state that the instance enters before reaching a stable state. If the development machine remains in an intermediate state for an extended period, this indicates an abnormal situation has occurred.


|State |Description |State attribute |Available operations |
|---|---|---|---|
|Queued |Due to insufficient resources, the development machine is waiting for resources. |Intermediate state |* No operations are supported |
|Starting up |The development machine is being created or is being started after being shut down. This is the state before the development machine enters the running state. |Intermediate state |* Shut down |
|Running |The development machine is in the running state. |Stable state |* Shut down<br><br>* Edit<br><br>* Log in<br><br>* Delete<br><br>* Save image |
|Creation failed |The development machine is in an abnormal state. You can try to start the development machine again. |Stable state |* Start up<br><br>* Edit<br><br>* Delete |
|Shutting down |The development machine is in the process of shutting down. After shutdown, computing resources will be released. |Intermediate state |No operations are supported |
|Shut down |The development machine is shut down and cannot be connected or logged in. |Stable state |* Start up<br><br>* Edit<br><br>* Delete |
|Deleting |The development machine is in the process of being deleted |Intermediate state |No operations are supported |
|Deleted |The development machine is in the deleted state. By default, it is not displayed in the list, but you can view it by filtering for the deleted state. |Stable state |No operations are supported |
|Saving image |When you perform a save image operation on a running development machine, it enters the saving image state. It is not recommended to perform any operations on the development machine in this state, as doing so may cause the image creation to fail. |Intermediate state |No operations are supported |
|Abnormal |The development machine is in an abnormal state. Immediate troubleshooting is recommended. |Stable state |* Shut down<br><br>* Delete |
