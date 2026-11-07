---
title: "Manage development machines"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Manage_development_machines"
---

This document describes the rules and key points for critical operations such as shutting down, editing, and deleting development machines.

<span id="2e8ad8fb"></span>
## Shut down development machines

To discontinue use of a development machine or change its configuration, perform the **shut down** operation. After shutting down, computing and network resources will be released, but cloud disk storage, operation records, and configuration environments will be retained. To use the machine again, simply **power on**.

<span id="995db064"></span>
## Edit development machines

The configurable items available for editing depend on the current status of the development machine. Changes take effect after powering on the machine again. For details, refer to:


|Development machine status |Configurable items |
|---|---|
|Running |* Development machine name<br><br>* Description<br><br>* Cloud disk (only supports expansion)<br><br>* SSH access key information<br><br>* Access port configuration |
|Shut down |* Development machine name<br><br>* Description<br><br>* Resource size<br><br>* Cloud disk (only supports expansion)<br><br>* SSH network mode<br><br>* Replace image<br><br>* Advanced network configuration (private network, subnet, security group)<br><br>* Access configuration (SSH public key, access port)<br><br>* Storage mount (TOS, vePFS, NAS configuration information) |
|Creation failed |* Development machine name<br><br>* Description<br><br>* Resource size<br><br>* Cloud disk (only supports expansion)<br><br>* SSH network mode<br><br>* Replace image<br><br>* Advanced network configuration (private network, subnet, security group)<br><br>* Access configuration (SSH public key, access port)<br><br>* Storage mount (TOS, vePFS, NAS configuration information) |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The development machine's cloud disk only supports expansion and does not support reducing capacity.</div>


* <div data-tips="true" data-tips-type="warning">After replacing the image, all data in the root directory (/) will be cleared and cannot be recovered. Please back up your data before replacing the image. You can save the data in the / directory to shared storage before replacing the image.</div>


* <div data-tips="true" data-tips-type="warning">After replacing the image, the machine will re\-enter the image download phase. You must manually power on the machine after replacing the image, and the power\-on time will vary depending on the image size.</div>



<span id="01e1d758"></span>
## Delete development machines

When you no longer need a development machine, you can delete it. Deletion releases the machine's cloud disk resources. If the machine is running, deletion also releases computing and network resources.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deletion, the data in the cloud storage will be permanently erased and cannot be recovered. Be sure to back up important data in advance.</div>
