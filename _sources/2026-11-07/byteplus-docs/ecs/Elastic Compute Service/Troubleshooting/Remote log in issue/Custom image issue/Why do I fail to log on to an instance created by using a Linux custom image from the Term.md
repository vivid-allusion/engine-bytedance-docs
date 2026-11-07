---
title: "Why do I fail to log on to an instance created by using a Linux custom image from the Terminal or encounter network inaccessibility?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/fail_to_log_on_to_an_instance_created_by_Linux_custom_image"
---

The issue is most likely caused by abnormal Cloud\-init execution, which leads to a connection anomaly. If you update the Python 3 version and modify the default Python interpreter (that is, creating a new symbolic link for the new Python 3 version) in the instance used to create a custom image, abnormal execution of the installed Cloud\-init may occur. For example, when you execute the `cloud-init --version` command, the following error message is displayed:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a531450f1b274f32d262ad629d59608b.png) </span>

You can update the custom image configuration and then recreate an instance by using one of the following methods.


* Method 1: Update the Python 3 version and reinstall Cloud\-init. For more information, see [Installing Cloud-init](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5Zub5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWQtaW5pdA==).

* Method 2: Modify the Cloud\-init executable file. Refer to the following configuration to change the path corresponding to the Python interpreter to the path of the legacy Python 3 version. In this topic, Python 3.6 is used as the legacy Python 3 version.

   1. Execute the `vim /usr/local/bin/cloud-init` command to open the cloud\-init file.

   2. Press `i` to enter edit mode and modify the content following `#!` at the beginning of the file to the path to Python 3.6.

      `#!/usr/bin/python3.6`

   3. Press the `Esc` key to exit edit mode, and then enter `:wq` and press Enter to save and exit the file.
