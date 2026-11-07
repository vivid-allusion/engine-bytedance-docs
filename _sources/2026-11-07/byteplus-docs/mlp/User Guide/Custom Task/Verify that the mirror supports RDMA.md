---
title: "Verify that the mirror supports RDMA."
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Verify_that_the_mirror_supports_RDMA"
---

This article describes how to verify whether the current image supports RDMA capabilities. Users can verify whether an image meets the conditions for RDMA use on V100 RDMA (ml.hpcg1v.21xlarge or ml.hpcg1ve.21xlarge) and A100 RDMA (ml.hpcpni2.28xlarge) models according to the steps below.

<span id="背景"></span>
# background

The RDMA network interface card hardware of V100 and A100 is different, and the Cloud as a Service supports the virtualization of the RDMA network interface card of V100 and A100 differently, so the versions of the relevant software libraries/packages in the image are also slightly different for different models.

<span id="确认操作系统的发行版本"></span>
# Verify the release version of the operating system

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The installation commands of different distributions may vary slightly. The current mainstream training container images are based on Ubuntu (the Ubuntu version below is 20.04). There will be images of other distributions in the future, and this document will be updated iteratively.</div>


<div data-tips="true" data-tips-type="tip">:::Execute the <code>cat /etc/os-release</code>inside the container, the output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```Plain
root@iv-ybqs2pif757grbqpwubx:/workspace# cat /etc/os-release 
NAME="Ubuntu"
VERSION="18.04.5 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.5 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=bionic
UBUNTU_CODENAME=bionic
```
</div>


<span id="根据机型配置测试环境"></span>
# <div data-tips="true" data-tips-type="tip">Configure the testing environment according to the model</div>


<span id="v100-rdma"></span>
## <div data-tips="true" data-tips-type="tip">V100 RDMA</div>


<span id="ubuntu"></span>
### <div data-tips="true" data-tips-type="tip">Ubuntu</div>



1. <div data-tips="true" data-tips-type="tip">Run the following command to install the test package.</div>



<div data-tips="true" data-tips-type="tip">```plain
apt update && apt install -y infiniband-diags
```
</div>



2. <div data-tips="true" data-tips-type="tip">Use the <code>ibstatus</code>command to view the network interface card rate. You can see that the network interface card (mlx5_1) rate in this example is <code>100Gb/s</code>, which is expected for V100 RDMA models.</div>



<div data-tips="true" data-tips-type="tip">```plain
# ibstatus
Infiniband device 'mlx5_0' port 1 status:
        default gid:     fe80:0000:0000:0000:0216:3eff:fe5a:2a70
        base lid:        0x0
        sm lid:          0x0
        state:           4: ACTIVE
        phys state:      5: LinkUp
        rate:            25 Gb/sec (1X EDR)
        link_layer:      Ethernet
Infiniband device 'mlx5_1' port 1 status:
        default gid:     fe80:0000:0000:0000:0216:3fff:fe0e:db1b
        base lid:        0x0
        sm lid:          0x0
        state:           4: ACTIVE
        phys state:      5: LinkUp
        rate:            100 Gb/sec (4X EDR)
        link_layer:      Ethernet
```
</div>



3. <div data-tips="true" data-tips-type="tip">Execute the following command to check whether the RDMA related libraries are installed.</div>



<div data-tips="true" data-tips-type="tip">```plain
dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```shell
# dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1// Below is the output
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                               Version                        Architecture                   Description
+++-==================================================-==============================-==============================-==========================================================================================================
ii  ibverbs-providers:amd64                            17.1-1ubuntu0.2                amd64                          User space provider drivers for libibverbs
ii  libibverbs1:amd64                                  17.1-1ubuntu0.2                amd64                          Library for direct userspace use of RDMA (InfiniBand/iWARP)
ii  libnl-3-200:amd64                                  3.2.29-0ubuntu3                amd64                          library for dealing with netlink sockets
ii  libnl-route-3-200:amd64                            3.2.29-0ubuntu3                amd64                          library for dealing with netlink sockets - route interface
dpkg-query: no packages found matching perftest
dpkg-query: no packages found matching libibumad3
dpkg-query: no packages found matching librdmacm1
```
</div>


<div data-tips="true" data-tips-type="tip">The above output information includes installed (such as <code>ibverbals-providers: amd64</code>, <code>libibverbs1: amd64</code>, etc.) and uninstalled (such as <code>perftest</code>, <code>libibumad3</code>, etc.) software.</div>


<div data-tips="true" data-tips-type="tip"><strong>If any packages are not installed, please follow up, otherwise you can use the above software normally to verify whether the current image supports RDMA.</strong> 4. Execute the following command:</div>


<div data-tips="true" data-tips-type="tip">```plain
apt update && apt install -y perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>



5. <div data-tips="true" data-tips-type="tip">Execute the following command to check the package installation status again.</div>



<div data-tips="true" data-tips-type="tip">```plain
dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```shell
# dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                               Version                        Architecture                   Description
+++-==================================================-==============================-==============================-==========================================================================================================
ii  ibverbs-providers:amd64                            28.0-1ubuntu1                  amd64                          User space provider drivers for libibverbs
ii  libibumad3:amd64                                   28.0-1ubuntu1                  amd64                          InfiniBand Userspace Management Datagram (uMAD) library
ii  libibverbs1:amd64                                  28.0-1ubuntu1                  amd64                          Library for direct userspace use of RDMA (InfiniBand/iWARP)
ii  libnl-3-200:amd64                                  3.4.0-1                        amd64                          library for dealing with netlink sockets
ii  libnl-route-3-200:amd64                            3.4.0-1                        amd64                          library for dealing with netlink sockets - route interface
ii  librdmacm1:amd64                                   28.0-1ubuntu1                  amd64                          Library for managing RDMA connections
ii  perftest                                           4.4+0.5-1                      amd64                          Infiniband verbs performance tests
```
</div>


<div data-tips="true" data-tips-type="tip">If there is no <code>dpkg-query: no packages found matching</code>error, it can be used normally, and the version number does not need to be consistent with this example.</div>


<div data-tips="true" data-tips-type="tip">6. <strong>If the nccl version is lower than </strong><strong><code>2.12</code></strong><strong>you can try to install the Sharp plugin to enable GDR (not being able to use GDR will cause about 10% performance degradation):</strong></div>


<div data-tips="true" data-tips-type="tip">```Plain
apt install automake autoconf libtool libibverbs-dev=28.0-1ubuntu1 libibverbs1=28.0-1ubuntu1
cd /tmp \
 && git clone https://github.com/Mellanox/nccl-rdma-sharp-plugins.git \
 && cd nccl-rdma-sharp-plugins \
 && ./autogen.sh \
 && ./configure --prefix=/usr/local/nccl-rdma-sharp-plugins --with-cuda=/usr/local/cuda \
 && make && make install \
 && rm -rf /tmp/nccl-rdma-sharp-plugins
 
 export LD_LIBRARY_PATH="/usr/local/nccl-rdma-sharp-plugins/lib:${LD_LIBRARY_PATH}"
```
</div>


<span id="centos"></span>
### <div data-tips="true" data-tips-type="tip">CentOS</div>



1. <div data-tips="true" data-tips-type="tip">This example uses the CentOS 7.9.2009 image in Docker Hub ( <a href="https://hub.docker.com/layers/library/centos/centos7.9.2009/images/sha256-dead07b4d8ed7e29e98de0f4504d87e8880d4347859d839686a31da35a3b532f?context=explore">Image Layer Details \- centos: centos7.9.2009 | Docker Hub </a>), and executes <code>cat /etc/os-release</code>in the container. The sample output is as follows:</div>



<div data-tips="true" data-tips-type="tip">```Plain
[root@ncggrd8mrsfegjm28qvqg /]# cat /etc/os-release 
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"
CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```
</div>


<div data-tips="true" data-tips-type="tip">Execute the following command to install the test package:</div>


<div data-tips="true" data-tips-type="tip">```Plain
yum install -y infiniband-diags
```
</div>


<div data-tips="true" data-tips-type="tip"><strong>Note: Since CentOS 8 has been migrated to CentOS 8 Stream, the following error may be encountered when using the above command:</strong></div>


<div data-tips="true" data-tips-type="tip">```Plain
# yum install -y infiniband-diags
Failed to set locale, defaulting to C.UTF-8
CentOS Linux 8 - AppStream                                                                                                                                                                           89  B/s |  38  B     00:00    
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist
```
</div>


<div data-tips="true" data-tips-type="tip"><strong>At this point, you can use the following two commands first, and then execute</strong> <code>yum install -y infiniband-diags</code><strong>again.</strong></div>


<div data-tips="true" data-tips-type="tip">```Plain
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Linux-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.epel.cloud|g' /etc/yum.repos.d/CentOS-Linux-*
```
</div>



2. <div data-tips="true" data-tips-type="tip">Using the <code>ibstatus</code>command to view the network interface card rate, you can see that the network interface card (mlx5_1) rate in this example is <code>100 Gb/sec</code>, which is expected for V100 RDMA models.</div>



<div data-tips="true" data-tips-type="tip">```Plain
# ibstatus
Infiniband device 'mlx5_1' port 1 status:
        default gid:     fe80:0000:0000:0000:d069:89ff:fe00:e864
        base lid:        0x0
        sm lid:          0x0
        state:           4: ACTIVE
        phys state:      5: LinkUp
        rate:            100 Gb/sec (4X EDR)
        link_layer:      Ethernet
```
</div>



3. <div data-tips="true" data-tips-type="tip">Execute the following command to check whether the RDMA related libraries are installed:</div>



<div data-tips="true" data-tips-type="tip">```Plain
rpm -q perftest libibumad libibverbs libnl3 librdmacm
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```Plain
# rpm -q perftest libibumad libibverbs libnl3 librdmacm
// Below is the output
package perftest is not installed
libibumad-22.4-6.el7_9.x86_64
package libibverbs is not installed
package libnl3 is not installed
package librdmacm is not installed
```
</div>


<div data-tips="true" data-tips-type="tip">The above output information includes installed (such as <code>libibumad</code>) and uninstalled (such as <code>perftest</code>, <code>libibverbs</code>, etc.) software. <strong>If the package is not installed, please follow up, otherwise you can use the above software normally to verify whether the current image supports RDMA</strong> <strong>.</strong></div>



4. <div data-tips="true" data-tips-type="tip">Execute the following command:</div>



<div data-tips="true" data-tips-type="tip">```Plain
yum install -y perftest libibumad libibverbs libnl3 librdmacm
```
</div>



5. <div data-tips="true" data-tips-type="tip">Execute the following command to check the package installation status again.</div>



<div data-tips="true" data-tips-type="tip">```Plain
rpm -q perftest libibumad libibverbs libnl3 librdmacm
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```Plain
# rpm -q perftest libibumad libibverbs libnl3 librdmacm
perftest-4.2-2.el7.x86_64
libibumad-22.4-6.el7_9.x86_64
libibverbs-22.4-6.el7_9.x86_64
libnl3-3.2.28-4.el7.x86_64
librdmacm-22.4-6.el7_9.x86_64
```
</div>


<div data-tips="true" data-tips-type="tip">If there is no <code>package x is not installed</code>error, it can be used normally, and the version number does not need to be consistent with this example.</div>


<span id="a100-rdma"></span>
## <div data-tips="true" data-tips-type="tip">A100 RDMA</div>


<span id="ubuntu"></span>
### <div data-tips="true" data-tips-type="tip">Ubuntu</div>



1. <div data-tips="true" data-tips-type="tip">To determine the network interface card rate, please refer to steps 1 and 2 in V100 RDMA. For A100 RDMA models, the network interface card rate should be 200Gb/s.</div>


2. <div data-tips="true" data-tips-type="tip">Execute the following command to confirm the Ubuntu version:</div>



<div data-tips="true" data-tips-type="tip">```plain
lsb_release -c
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```plain
# lsb_release -c
// Below is the output
Codename:       bionic
```
</div>


<div data-tips="true" data-tips-type="tip">Codename and Ubuntu versions correspond to the following table:</div>


<div data-tips="true" data-tips-type="tip">
|Codename |Version |
|---|---|
|bionic |18.04 |
|focal |20.04 |
|impish |21.10 |
|jammy |22.04 |
</div>



3. <div data-tips="true" data-tips-type="tip">Execute the following command to check whether the RDMA related libraries are installed.</div>



<div data-tips="true" data-tips-type="tip">```plain
dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```shell
# dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1// Below is the output
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                               Version                        Architecture                   Description
+++-==================================================-==============================-==============================-==========================================================================================================
ii  ibverbs-providers:amd64                            17.1-1ubuntu0.2                amd64                          User space provider drivers for libibverbs
ii  libibverbs1:amd64                                  17.1-1ubuntu0.2                amd64                          Library for direct userspace use of RDMA (InfiniBand/iWARP)
ii  libnl-3-200:amd64                                  3.2.29-0ubuntu3                amd64                          library for dealing with netlink sockets
ii  libnl-route-3-200:amd64                            3.2.29-0ubuntu3                amd64                          library for dealing with netlink sockets - route interface
dpkg-query: no packages found matching perftest
dpkg-query: no packages found matching libibumad3
dpkg-query: no packages found matching librdmacm1
```
</div>


<div data-tips="true" data-tips-type="tip">The above output information includes installed (such as <code>ibverbals-providers: amd64</code>, <code>libibverbs1: amd64</code>, etc.) and uninstalled (such as <code>perftest</code>, <code>libibumad3</code>, etc.) software.</div>


<div data-tips="true" data-tips-type="tip"><strong>If a package is not installed or the first two digits of </strong><strong><code>ibverbs1: amd64</code></strong><strong>and </strong><strong><code>libibverbs1: amd64</code></strong><strong>are less than </strong><strong><code>23</code></strong><strong>, follow up.</strong> <strong>Otherwise, you can jump to step 8 to compare the output, and if there is no problem, it can be used normally.</strong> 4. <strong>If the version obtained in step 2 is lower than </strong><strong><code>20.04</code></strong><strong>, please start from step 5. If the version is higher than </strong><strong><code>20.04</code></strong><strong>, please execute the following command directly, and then jump to step 8.</strong></div>


<div data-tips="true" data-tips-type="tip">```plain
apt update && apt install -y perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>



5. <div data-tips="true" data-tips-type="tip">Add <code>deb http://mirrors.ivolces.com/ubuntu/focal main universe</code>to the <code>/etc/apt/sources.list</code>, or execute the following command directly (just add it once):</div>



<div data-tips="true" data-tips-type="tip">```plain
echo "deb http://mirrors.ivolces.com/ubuntu/ focal main universe" >> /etc/apt/sources.list
```
</div>



6. <div data-tips="true" data-tips-type="tip">Add <code>APT :: Default - Release "Codename";</code>to <code>/etc/apt/apt.conf.d/01-vendor-ubuntu</code>, where Codename is replaced with the result obtained in step 1, take <code>18.04</code>as an example and execute the following command (just add it once):</div>



<div data-tips="true" data-tips-type="tip">```plain
echo "APT::Default-Release \"bionic\";" >> /etc/apt/apt.conf.d/01-vendor-ubuntu
```
</div>



7. <div data-tips="true" data-tips-type="tip">Execute the following command:</div>



<div data-tips="true" data-tips-type="tip">```plain
apt update && apt install -t focal perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>



8. <div data-tips="true" data-tips-type="tip">Execute the following command to check the package installation status again.</div>



<div data-tips="true" data-tips-type="tip">```plain
dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```shell
# dpkg -l perftest ibverbs-providers libibumad3 libibverbs1 libnl-3-200 libnl-route-3-200 librdmacm1Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                               Version                        Architecture                   Description
+++-==================================================-==============================-==============================-==========================================================================================================
ii  ibverbs-providers:amd64                            28.0-1ubuntu1                  amd64                          User space provider drivers for libibverbs
ii  libibumad3:amd64                                   28.0-1ubuntu1                  amd64                          InfiniBand Userspace Management Datagram (uMAD) library
ii  libibverbs1:amd64                                  28.0-1ubuntu1                  amd64                          Library for direct userspace use of RDMA (InfiniBand/iWARP)
ii  libnl-3-200:amd64                                  3.4.0-1                        amd64                          library for dealing with netlink sockets
ii  libnl-route-3-200:amd64                            3.4.0-1                        amd64                          library for dealing with netlink sockets - route interface
ii  librdmacm1:amd64                                   28.0-1ubuntu1                  amd64                          Library for managing RDMA connections
ii  perftest                                           4.4+0.5-1                      amd64                          Infiniband verbs performance tests
```
</div>


<div data-tips="true" data-tips-type="tip"><strong>Check the version number of </strong><strong><code>ibverbs-providers: amd64</code></strong><strong>, </strong><strong><code>libibumad3: amd64</code></strong><strong>, </strong><strong><code>libibverbs 1: amd64</code></strong><strong>, </strong><strong><code>librdmacm1: amd64</code></strong><strong>, in this case </strong><strong><code>28.0-1 ubuntu1</code></strong><strong>, the first two digits are not less than </strong><strong><code>23</code></strong><strong>to use normally.</strong></div>


<span id="centos"></span>
### <div data-tips="true" data-tips-type="tip">CentOS</div>



1. <div data-tips="true" data-tips-type="tip">This example uses the CentOS 7.9.2009 image in Docker Hub ( <a href="https://hub.docker.com/layers/library/centos/centos7.9.2009/images/sha256-dead07b4d8ed7e29e98de0f4504d87e8880d4347859d839686a31da35a3b532f?context=explore">Image Layer Details \- centos: centos7.9.2009 | Docker Hub </a>), and executes <code>cat /etc/os-release</code>in the container. The sample output is as follows:</div>



<div data-tips="true" data-tips-type="tip">```Plain
[root@ncggrd8mrsfegjm28qvqg /]# cat /etc/os-release 
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"
CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```
</div>


<div data-tips="true" data-tips-type="tip">Execute the following command to install the test package:</div>


<div data-tips="true" data-tips-type="tip">```Plain
yum install -y infiniband-diags
```
</div>


<div data-tips="true" data-tips-type="tip"><strong>Note: Since CentOS 8 has been migrated to CentOS 8 Stream, the following error may be encountered when using the above command:</strong></div>


<div data-tips="true" data-tips-type="tip">```Plain
# yum install -y infiniband-diags
Failed to set locale, defaulting to C.UTF-8
CentOS Linux 8 - AppStream                                                                                                                                                                           89  B/s |  38  B     00:00    
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist
```
</div>


<div data-tips="true" data-tips-type="tip"><strong>At this point, you can use the following two commands first, and then execute</strong> <code>yum install -y infiniband-diags</code><strong>again.</strong></div>


<div data-tips="true" data-tips-type="tip">```Plain
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Linux-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.epel.cloud|g' /etc/yum.repos.d/CentOS-Linux-*
```
</div>



2. <div data-tips="true" data-tips-type="tip">Using the <code>ibstatus</code>command to view the network interface card rate, you can see that the network interface card (mlx5_1) rate in this example is <code>100 Gb/sec</code>, which is expected for V100 RDMA models.</div>



<div data-tips="true" data-tips-type="tip">```Plain
# ibstatus
Infiniband device 'mlx5_1' port 1 status:
        default gid:     fe80:0000:0000:0000:d069:89ff:fe00:e864
        base lid:        0x0
        sm lid:          0x0
        state:           4: ACTIVE
        phys state:      5: LinkUp
        rate:            100 Gb/sec (4X EDR)
        link_layer:      Ethernet
```
</div>



3. <div data-tips="true" data-tips-type="tip">Execute the following command to check whether the RDMA related libraries are installed:</div>



<div data-tips="true" data-tips-type="tip">```Plain
rpm -q perftest libibumad libibverbs libnl3 librdmacm
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```Plain
# rpm -q perftest libibumad libibverbs libnl3 librdmacm
// Below is the output
package perftest is not installed
libibumad-22.4-6.el7_9.x86_64
package libibverbs is not installed
package libnl3 is not installed
package librdmacm is not installed
```
</div>


<div data-tips="true" data-tips-type="tip">The above output information includes installed (such as <code>libibumad</code>) and uninstalled (such as <code>perftest</code>, <code>libibverbs</code>, etc.) software. <strong>If the package is not installed, please follow up, otherwise you can use the above software normally to verify whether the current image supports RDMA</strong> .</div>



4. <div data-tips="true" data-tips-type="tip">Execute the following command:</div>



<div data-tips="true" data-tips-type="tip">```Plain
yum install -y perftest libibumad libibverbs libnl3 librdmacm
```
</div>



5. <div data-tips="true" data-tips-type="tip">Execute the following command to check the package installation status again:</div>



<div data-tips="true" data-tips-type="tip">```Plain
rpm -q perftest libibumad libibverbs libnl3 librdmacm
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```Plain
# rpm -q perftest libibumad libibverbs libnl3 librdmacm
perftest-4.2-2.el7.x86_64
libibumad-22.4-6.el7_9.x86_64
libibverbs-22.4-6.el7_9.x86_64
libnl3-3.2.28-4.el7.x86_64
librdmacm-22.4-6.el7_9.x86_64
```
</div>


<div data-tips="true" data-tips-type="tip">If there is no <code>package x is not installed</code>error, it can be used normally, and the version number does not need to be consistent with this example (take <code>libibverbs- 22.4-6. el7_9. x86_64</code>as an example, where the version number is <code>22.4-6. el7_9. x86_64</code>, only the first two digits are not less than 22).</div>


<span id="验证是否支持-rdma"></span>
# <div data-tips="true" data-tips-type="tip">Verify whether RDMA is supported.</div>


<div data-tips="true" data-tips-type="tip">After configuring the environment according to the previous text, you can follow the following steps to verify the configuration of the image. For both V100 RDMA and A100 RDMA models, the verification steps are the same.</div>


<span id="在单机上的验证方式"></span>
## <div data-tips="true" data-tips-type="tip">Verification method on a single machine</div>



1. <div data-tips="true" data-tips-type="tip">Enter the following command:</div>



<div data-tips="true" data-tips-type="tip">```plain
ib_write_bw -d mlx5_1 &
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```shell
# ib_write_bw -d mlx5_1 &[1] 104777
root@iv-ybrf933mwd8rx7gs2na5:/workspace# 
************************************
* Waiting for client to connect... *
************************************
```
</div>



2. <div data-tips="true" data-tips-type="tip">On the same machine, continue to enter the following commands:</div>



<div data-tips="true" data-tips-type="tip">```plain
ib_write_bw -d mlx5_1 127.0.0.1 --report_gbits
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```shell
# ib_write_bw -d mlx5_1 127.0.0.1 --report_gbits---------------------------------------------------------------------------------------
                    RDMA_Write BW Test
 Dual-port       : OFF          Device         : mlx5_1
 Number of qps   : 1            Transport type : IB
 Connection type : RC           Using SRQ      : OFF
 CQ Moderation   : 100
 Mtu             : 4096[B]
 Link type       : Ethernet
 GID index       : 2
 Max inline data : 0[B]
 rdma_cm QPs     : OFF
 Data ex. method : Ethernet
---------------------------------------------------------------------------------------
 local address: LID 0000 QPN 0x090a PSN 0x723cbf RKey 0x082200 VAddr 0x007f67e0c4c000
 GID: 00:00:00:00:00:00:00:00:00:00:255:255:198:18:06:59
---------------------------------------------------------------------------------------
                    RDMA_Write BW Test
 Dual-port       : OFF          Device         : mlx5_1
 Number of qps   : 1            Transport type : IB
 Connection type : RC           Using SRQ      : OFF
 TX depth        : 128
 CQ Moderation   : 100
 Mtu             : 4096[B]
 Link type       : Ethernet
 GID index       : 2
 Max inline data : 0[B]
 rdma_cm QPs     : OFF
 Data ex. method : Ethernet
---------------------------------------------------------------------------------------
 local address: LID 0000 QPN 0x090b PSN 0xe78073 RKey 0x082300 VAddr 0x007fd7b287f000
 GID: 00:00:00:00:00:00:00:00:00:00:255:255:198:18:06:59
 remote address: LID 0000 QPN 0x090b PSN 0xe78073 RKey 0x082300 VAddr 0x007fd7b287f000
 GID: 00:00:00:00:00:00:00:00:00:00:255:255:198:18:06:59
 remote address: LID 0000 QPN 0x090a PSN 0x723cbf RKey 0x082200 VAddr 0x007f67e0c4c000
 GID: 00:00:00:00:00:00:00:00:00:00:255:255:198:18:06:59
---------------------------------------------------------------------------------------
 #bytes     #iterations    BW peak[MB/sec]    BW average[MB/sec]   MsgRate[Mpps]---------------------------------------------------------------------------------------
 #bytes     #iterations    BW peak[Gb/sec]    BW average[Gb/sec]   MsgRate[Mpps] 65536      5000             93.90              93.67              0.178661
---------------------------------------------------------------------------------------
 65536      5000             93.90              93.67              0.178661
---------------------------------------------------------------------------------------
```
</div>


<div data-tips="true" data-tips-type="tip">For V100 RDMA models, the bandwidth value ( <code>BW peak</code>, <code>BW average</code>) should be close to <code>100Gb/s</code>, A100 RDMA models should be close to <code>200Gb/s</code>, if it meets the requirements, it means that there is no problem with the configuration. If there is no output or error, please go back to the section of the configuration environment according to the model to check whether there is any omission of configuration items.</div>


<span id="在多机上的验证方式"></span>
## <div data-tips="true" data-tips-type="tip">Verification methods on multiple machines</div>



1. <div data-tips="true" data-tips-type="tip">Enter the following command into a machine</div>



<div data-tips="true" data-tips-type="tip">```plain
ib_write_bw -d mlx5_1 -x $NCCL_IB_GID_INDEX
```
</div>


<div data-tips="true" data-tips-type="tip">The output example is as follows:</div>


<div data-tips="true" data-tips-type="tip">```plain
# ib_write_bw -d mlx5_1 -x $NCCL_IB_GID_INDEX
************************************
* Waiting for client to connect... *
************************************
```
</div>



2. <div data-tips="true" data-tips-type="tip">Enter the following command in machine B, <code>< MACHINE_A_HOST ></code>please replace it with the RDMA network port IP of machine A.</div>



<div data-tips="true" data-tips-type="tip">```plain
ib_write_bw -d mlx5_1 -x $NCCL_IB_GID_INDEX <MACHINE_A_HOST> --report_gbits
```
</div>
