---
title: "How do I disable the GSP configuration in a public image?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_to_turn_off_the_GSP_configuration_in_the_public_image"
---

NVIDIA recommends that you disable GSP in pass\-through or bare metal mode. However, disabling GSP will affect performance by 1% to 2%. Therefore, you need to choose whether to disable GSP based on your business requirements. For more information about GSP, see [GSP Firmware](https://download.nvidia.com/XFree86/Linux-x86_64/550.54.14/README/gsp.html) and [Disabling GSP Firmware](https://docs.nvidia.com/grid/latest/grid-vgpu-user-guide/index.html#disabling-gsp).

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When a container node uses a public image with the 525/535 driver, some GPUs will have the GSP firmware configuration enabled by default, which will result in XID 119 and may affect your business.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Add the parameter to disable the GSP configuration in the configuration file of the 535 version public image.

   ```bash
   vi /etc/modprobe.d/nvidia.conf             # Run the vi command to edit the configuration file of the 535 version public image.
   
   options nvidia NVreg_EnableGpuFirmware=0 # Add this configuration to disable GSP. Save the configuration and exit editing.
   ```
   

2. Restart the ECS instance for the configuration to take effect.
