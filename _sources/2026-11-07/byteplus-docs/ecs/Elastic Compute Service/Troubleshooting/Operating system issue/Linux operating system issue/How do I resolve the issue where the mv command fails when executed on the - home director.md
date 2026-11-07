---
title: "How do I resolve the issue where the mv command fails when executed on the /home directory in CentOS 7?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/failing_to_execute_the_mv_command_on_the_home_directory_in_CentOS7"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

In CentOS 7, executing the `mv` command on the /home directory fails.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7802b6e9833040e82f3dbb9f6bb92d44.png) </span>

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

This issue occurs because `ProtectHome=yes` is specified for the chronyd.service service by default, which protects the /home directory.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_856d1fb352455ee09973bc9f436a01db.png) </span>

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

You can modify the chronyd service configuration to set `ProtectHome` to `no`, thereby removing protection for the /home directory.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Modify chronyd service configuration.

   1. Execute the following command to open the chronyd service configuration file.

      ```Plain Text
      vi /usr/lib/systemd/system/chronyd.service
      ```
      

   2. Press the `i` key to enter edit mode. Then, change `ProtectHome=yes` to `ProtectHome=no`.

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and press the Enter key to save the changes and exit the file.

3. Execute the following command to reload the configuration file.

   ```Plain Text
   systemctl daemon-reload
   ```
   

4. Execute the following command to restart the chronyd service.

   ```Plain Text
   systemctl restart chronyd.service
   ```
