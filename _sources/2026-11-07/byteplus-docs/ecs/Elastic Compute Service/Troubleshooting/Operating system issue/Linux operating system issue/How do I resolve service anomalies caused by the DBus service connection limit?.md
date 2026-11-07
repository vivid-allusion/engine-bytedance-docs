---
title: "How do I resolve service anomalies caused by the DBus service connection limit?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve_dbus_limit"
---

<span id="Lj6ufDhK"></span>
## Issue description

In scenarios with intensive operation of system services, management components, and automated tasks, some DBus\-dependent features may encounter anomalies. Examples include service startup failures, unresponsive management commands, and abnormal system component responses. When you check instance OS logs, such as by executing the `sudo journalctl -u dbus` command, the DBus service displays the "The maximum number of active connections for UID 0 has been reached (max_connections_per_user=256)" error message.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81412760b1ecacfdf46ba193d3726fdb.png) </span>

<span id="YIamB9xW"></span>
### Causes

The DBus service limits the maximum number of concurrent DBus connections that a single user ID (UID) can establish via the `max_connections_per_user` parameter. When the number of concurrent connections for UID 0 (the root user) hits this limit, new DBus connection requests are rejected. In actual environments, common triggers for this limit include, but are not limited to:


* A large number of background services running as the root user in the system, with each service frequently creating DBus connections.

* Bugs in certain services may prevent timely closure of DBus connections after creation, resulting in connection leaks. The number of accumulated connections will eventually hit the limit of 256.

* Starting a large number of DBus\-dependent root processes at one time creates more than 256 DBus connections in a short period of time.

* The system is in an abnormal state or experiences a retry storm.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The dbus\-broker daemon dynamically adjusts the value of the <code>max_connections_per_user</code> parameter. Therefore, the DBus connection limit issue is usually not triggered. This issue mainly occurs in operating systems that use the dbus\-daemon daemon.</div>


<span id="ZRqjmsPJ"></span>
### Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This solution is intended only to mitigate issues arising from insufficient DBus connections. It does not replace the troubleshooting and resolution of abnormal service or program behaviors that trigger such issues.</div>


* <div data-tips="true" data-tips-type="warning">If the issue occurs frequently, we recommend that you further analyze the sources of DBus connections in the system and troubleshoot potential connection leaks, abnormal retries, or unreasonable system call methods.</div>


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to back up the DBus service configuration file.

   ```Bash
   cp /etc/dbus-1/system.conf /etc/dbus-1/system-local.conf
   ```
   

3. Modify the DBus service configuration file and appropriately adjust the connection limit to mitigate the issue.

   1. Execute the following command to open the DBus service configuration file.

      ```Bash
      vi /etc/dbus-1/system-local.conf
      ```
      

   2. Press `i` to enter edit mode, and add the following configuration to the file to increase the maximum number of DBus connections for the root user to `512`.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">We recommend that you adjust the value of the <code>max_connections_per_user</code> parameter based on your actual needs and workloads. Do not blindly increase the connection limit.      </div>
      

      ```XML
      <!DOCTYPE busconfig
        PUBLIC "-//freedesktop//DTD D-Bus Bus Configuration 1.0//EN" "http://www.freedesktop.org/standards/dbus/1.0/busconfig.dtd">
      <busconfig>
        <limit name="max_connections_per_user">512</limit>
      </busconfig>
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to restart the DBus service for the configuration to take effect.

   ```Bash
   systemctl restart dbus
   ```
