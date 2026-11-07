---
title: "How do I resolve container creation errors when mounting the root directory of a TOS bucket to a PV?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-if-a-container-creation-error-occurs-after-I-mount-a-PV-to-the-root-directory-of-a-TOS"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description


* When I attempt to create a dynamic PV from TOS by using the console, I cannot create a PV with the root directory of the bucket set as the subdirectory.

* Although I can create a PV with the root directory of the bucket set as the subdirectory using kubectl, the container fails to start with the "Name or service not known" error.


<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

VKE does not support creating a PV with the subdirectory set as the root directory of the TOS bucket. The subdirectory validation rules are as follows:


* The length is 2 to 128 characters.

* It can start only with the slash (/) character.

* It supports lowercase letters, numbers, and the following special characters: \-._~/:$@=+?!%#


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

When creating dynamic TOS PVs, avoid using the root directory of a TOS bucket. Instead, create dynamic PVs using a subdirectory.
