---
title: "Methods to change the system limit parameters for Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_adjusting_the_limits_system_parameters_in_a_Linux_instance"
---

This topic describes how to resolve instance remote access failures caused by the `nofile` parameter value exceeding the `nr_open` parameter value by adjusting the `nofile` parameter in the `limits.conf` configuration file.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The `/etc/security/limits.conf` configuration file in Linux systems is used to restrict system resources. For example, it limits the number of files, threads, and memory that users can use, thereby improving system stability. The `nofile` parameter in this configuration file represents the maximum number of files that all users in the system can open. `/proc/sys/fs/nr_open` represents the maximum number of files that a single process in the system can allocate. If the `nofile` parameter value exceeds the `nr_open` parameter value, the instance may become inaccessible via remote connection.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

Before you modify the configuration or data of an instance, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) first to improve fault tolerance and ensure data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Enter the Linux operating system in single\-user mode. For more information, see [Entering single-user mode](https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode).

2. Execute the following command to edit the `/etc/security/limits.conf` configuration file.

   ```Plain Text
   vim /etc/security/limits.conf
   ```
   

3. Locate the `root soft nofile` and `root hard nofile` parameters, and set the parameters to the following values.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This method makes the parameter settings take effect permanently. If you need to set the <code>nofile</code> parameter temporarily, use the <code>ulimit -n [$Nofile]</code> command to configure the <code>nofile</code> parameter.   </div>
   

   ```Plain Text
   root soft nofile 65535
   root hard nofile 65535
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">soft nofile   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This is the warning threshold for the number of open files. We recommend that you set this parameter to the default value 65535.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you understand the purpose of this system parameter, you can modify it to a desired value, but the <code>soft nofile</code> value must not exceed the <code>hard nofile</code> value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">hard nofile   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This is the actual threshold for the number of open files. An error will occur if the number of open files exceeds this value. We recommend that you set this parameter to the default value 65535.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you understand the purpose of this system parameter, you can modify it to a desired value, but the <code>hard nofile</code> value must not exceed the value of <code>/proc/sys/fs/nr_open</code>. If the <code>nofile</code> parameter value exceeds the <code>nr_open</code> parameter value, you may fail to log in to the instance as expected.   </div>
   

4. After the configuration file is modified, press the "Esc" key to exit edit mode and enter `wq`.

5. Press the "Enter" key to save and exit the file.

6. Restart the instance to make the configuration take effect.
