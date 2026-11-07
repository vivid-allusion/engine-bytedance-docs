---
title: "Description of differences between veLinux 2.0 and veLinux 1.0​"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/The-differences-between-veLinux-2-and-1"
---

This topic describes the main differences between veLinux 2.0 image and veLinux 1.0 image.

<span id="Python"></span>
## Python

<span id=".5pSv5oyB54mI5pys"></span>
### Supported versions

Since the [core team of the Python upstream community](https://www.python.org/dev/peps/pep-0373/#update) discontinued support for Python 2 in January 2020, veLinux 2.0 no longer supports Python 2 and only supports Python 3.

<span id=".UHl0aG9u6Kej6YeK5Zmo"></span>
### Python interpreter

To follow the [PEP-668](https://peps.python.org/pep-0668/) (Python Enhancement Proposal), in veLinux 2.0:


* The Python 3 interpreter packages (PyPy 3 and Python 3.11) are marked as externally managed (external management).

* Pip (python3\-pip), the package manager for Python 3, blocks manual package installations in the Python 3 interpreter of veLinux 2.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To manually install packages for the Python 3 interpreter, use the <code>--break-system-packages</code> option in the installation command.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the Python application (or version) you need to install does not have a Deb package, we recommend that you install it with <a href="https://pipx.pypa.io/stable/">pipx</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the Python library module (or version) you need to install does not have a Deb package, we recommend that you install it in a virtual environment (Virtualenv).   </div>
   


<span id="iptables"></span>
## iptables

[iptables](https://netfilter.org/projects/iptables/) is used for packet filtering, network address translation (NAT), and other packet management. Due to limits that can not be easily resolved, iptables is gradually replaced by [nftables](https://netfilter.org/projects/nftables/) and no longer installed in veLinux 2.0 by default.

<span id="systemd"></span>
## systemd

In veLinux 2.0, systemd (system initialization manager) uses the feature of cgroup v2 control group by default.

<span id="DKMS 3.0"></span>
## DKMS 3.0

In veLinux 2.0, the `REMAKE_INITRD` attribute is deleted from DKMS (Dynamic Kernel Module Support) 3.0. Therefore, after installing a new kernel, or installing/updating drivers, you need to manually execute the `update-initramfs -u` command to update the initial RAM file system (initramfs).

<span id="Rsyslog"></span>
## Rsyslog

In ​veLinux 2.0, Rsyslog (Remote System Logging) is of a lower priority and is not installed by default.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you decide to continue using Rsyslog:</div>



* <div data-tips="true" data-tips-type="warning">The default high\-precision timestamps (microsecond level) in Rsyslog may affect tools that analyze system logs. Therefore, you may need to update the rules for matching message creation time in your locally created Logcheck rules to ensure compatibility with the new Rsyslog format.</div>


* <div data-tips="true" data-tips-type="warning">By default, Rsyslog no longer creates certain log files in <code>/var/log</code>. Messages that were originally written to these files will be written to the <code>/var/log/syslog</code> file.</div>


   <div data-tips="true" data-tips-type="warning">Log files that are no longer created by Rsyslog include:   </div>
   

   * <div data-tips="true" data-tips-type="warning"><code>/var/log/mail.{info,warn,err}</code>: These files contain messages from the local mail transfer agent (MTA).</div>


   * <div data-tips="true" data-tips-type="warning"><code>/var/log/lpr.log</code>: These files contain log messages related to printing.</div>


   * <div data-tips="true" data-tips-type="warning"><code>/var/log/{messages,debug,daemon.log}</code>: These files contain different types of system events and messages.</div>



<span id="GRUB"></span>
## GRUB

Traditionally, GRUB has used [os-prober](https://salsa.debian.org/installer-team/os-prober) by default to detect other operating systems installed on the computer and add them to the boot menu. However, this operation may cause issues such as boot delays, cluttered boot menus, and incorrect booting. Therefore, veLinux 2.0 no longer uses os\-prober for GRUB by default.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to use GRUB to boot the system in veLinux 2.0 and to have other operating systems displayed in the boot menu, execute the <code>dpkg-reconfigure <GRUB package name></code> command to change the GRUB configuration.</div>


<span id=".5a-G6ZKl566h55CG5pa55byP"></span>
## Key management method

To improve system security and manageability, veLinux 2.0 no longer recommends the usage of apt\-key to manage the key. **If you continue to use apt\-key, you will receive warning messages**.

We recommend that you manage keys in the form of apt\-key key files (.gpg or .asc) in the `/etc/apt/trusted.gpg.d` directory. For more details, refer to [APT-KEY](https://manpages.debian.org/bookworm/apt/apt-key.8.en.html).

<span id=".57O757uf5qCH6K-G"></span>
## System identifier

In the veLinux 2.0 image, the `/etc/os-release` file has been updated to include veLinux system identifiers. You can use the `lsb_release` tool to display information about the veLinux system.
