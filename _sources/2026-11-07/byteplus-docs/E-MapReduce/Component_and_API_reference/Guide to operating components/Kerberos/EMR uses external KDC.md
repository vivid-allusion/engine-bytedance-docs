---
title: "EMR uses external KDC"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_uses_external_KDC"
---

EMR\-V3.8.0 and later versions support creating Kerberos\-enabled clusters, and open\-source components within the cluster are started in Kerberos security mode. When creating an EMR cluster, you can use a KDC created within the cluster or an external KDC for unified identity management and authentication.

<span id="使用限制"></span>
## Limits


* Kerberos\-mode clusters associated with an external KDC must be established through EMR.

* The correct IP address of the KDC, the IP address of Kadmin, and the name and password of the Principal have been obtained.

* You must ensure network and port connectivity between the EMR cluster and the external KDC. For example, TCP port 88, port 749, and UDP port 88.


<span id="注意事项"></span>
## important notes


* User management of the external KDC cluster is not connected to user management of the cluster where the KDC resides. Users in the cluster where the KDC resides are used for Kerberos authentication. It is recommended to import users from both clusters in sync.

* User Keytab download is only supported in the cluster where the KDC resides.


<span id="操作步骤"></span>
## procedure


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home) and click Create Cluster.

2. During the **software configuration** phase of cluster creation, turn on the **Advanced Settings** section's **Kerberos authentication** switch.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96b5e45096424b5b84f26b470be4be60~tplv-goo7wpa0wc-image.image) </span>


3. Select external KDC as the KDC source. The default is a self\-built KDC in this cluster; that is, the current cluster creates the KDC for you. To use your external KDC, you need to fill in the following information.



|**Parameter** |**Description** |
|---|---|
|KDC Hosts |The IP address and port of the KDC. If there are multiple IP addresses, you can separate them with a comma (,). For example, 192.168. **.** :88,192.168. **.** :88.<br><br>Ensure connectivity between the EMR cluster and the KDC address and port. |
|Realm Name |KDC Realm name |
|KAdmin Hosts |The IP address and port of the Kadmin service. If there are multiple IP addresses, you can separate them with a comma (,). For example, 192.168. **.** :749,192.168. **.** :749.<br><br>Ensure connectivity between the EMR cluster and the Kadmin service address and port. For example, TCP port 88, port 749, and UDP port 88. |
|Admin Principal |The Principal name used to connect to the Kadmin service. The default is root/admin.<br><br>Ensure that this Principal has admin privileges and can create Principals and export keytab files. |
|Set Admin password |The password corresponding to the administrator Principal. The default is the default password of the cluster where the KDC resides. After the cluster is created, it can be viewed in the /root/.emr/secret file on the Master node. Only root users can view it. |
|Confirm password |The two password entries must match. |
