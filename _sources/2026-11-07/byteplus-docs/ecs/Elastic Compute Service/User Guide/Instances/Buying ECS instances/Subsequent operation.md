---
title: "Subsequent operation"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/What-to-do-next"
---

After you purchase an ECS instance, refer to this topic to learn how to use it. For more information on ECS instance purchase, refer to [Overview of methods for purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

<span id=".5p-l55yL5bey6LSt5Lmw5a6e5L6L5Y-K5YW26YWN572u5L-h5oGv"></span>
## View created instances and instance configuration information

To view purchased instances and relevant information, such as the EIPs, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1).

<span id=".5re75Yqg5a6J5YWo57uE6KeE5YiZ"></span>
## Add security group rules

[Security groups](https://docs.byteplus.com/en/docs/ecs/Security-group-overview) are used to control the inbound and outbound traffic of network interfaces. Make sure the inbound rules of the security group associated with the primary network interface allow the protocols and ports through which the instance provides services, such as TCP port 22 used for remote login to Linux instances. Otherwise, you cannot connect to or access the ECS instance.

If you have not allowed protocols and ports yet, [modify the security group access rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).

<span id=".55m75b2V5a6e5L6L"></span>
## Log in to the ECS instance

Multiple methods are available for you to log in to ECS instances, such as ECS Terminal, VNC, and third\-party tools. For more information, refer to [Login method overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

<span id=".5YiG5Yy65qC85byP5YyW5pWw5o2u55uY"></span>
## Partition and format data volume

If you purchase a data volume when creating the instance, partition and format the data volume after you log in to the instance. After this, you can use the data volume. For detailed operation, refer to:


* [Partition and format volumes (less than or equal to 2 TiB)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-larger-than-2-TiB)

* [Partition and format volumes (larger than 2 TiB)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB)


<span id=".5L2_55So5a6e5L6L"></span>
## Use ECS instances

<span id=".5paH5Lu25Lyg6L6T"></span>
### Transfer files

You can upload your local files to ECS instances, or download data from ECS instances to your local host. For more information, refer to [File transfer overview](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

<span id=".5bu656uZ5rGH5oC7"></span>
### Set up environments, applications, or websites

After [logging in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/What-to-do-next#.55m75b2V5a6e5L6L), you can set up different environments, applications, or websites on the instance based on business needs. Common setup scenarios are shown below:

<span id=".5pCt5bu6546v5aKD"></span>
#### Set up environments


|Practice |Description |
|---|---|
|[Building a Node.js environment](https://docs.byteplus.com/en/docs/ecs/Building-a-Node-js-environment) |Taking an ECS instance running the CentOS 8.3 operating system as an example, this guide introduces how to build a Node.js environment. |
|[Building a Java Web environment](https://docs.byteplus.com/en/docs/ecs/Building-a-Java-web-environment) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build a Java Web environment. |
|[Building an LNMP environment (CentOS 8)](https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-CentOS-8) |Taking an ECS instance running the CentOS 8.3 operating system as an example, this guide introduces how to build an LNMP environment. |
|[Building an LNMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-CentOS-7) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build an LNMP environment. |
|[Building an LNMP environment (Ubuntu 18.04)](https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-Ubuntu-18) |Taking an ECS instance running the Ubuntu 18.04 operating system as an example, this guide introduces how to build an LNMP environment. |
|[Building a LAMP environment (CentOS 8)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-8) |Taking an ECS instance running the CentOS 8.3 operating system as an example, this guide introduces how to build a LAMP environment. |
|[Building a LAMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build a LAMP environment. |
|[Building a LAMP environment (Ubuntu 18.04)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-Ubuntu-18) |Taking an ECS instance running the Ubuntu 18.04 operating system as an example, this guide introduces how to build a LAMP environment. |
|[Building a Web environment (Windows)](https://docs.byteplus.com/en/docs/ecs/Manually_build_a_Web_Environment) |Taking an ECS instance running Windows Server 2022 operating system as an example, this guide introduces how to build a Web environment. |


<span id=".5pCt5bu65bqU55So"></span>
#### Set up applications


|Practice |Description |
|---|---|
|[Building an FTP site (Linux)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Linux) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build an FTP site. |
|[Building an FTP site (Windows)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Windows) |Taking an ECS instance running Windows Server 2019 operating system as an example, this guide introduces how to build an FTP site. |
|[Building GitLab](https://docs.byteplus.com/en/docs/ecs/Building-GitLab) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build and use the Gitlab application. |
|[Building RabbitMQ](https://docs.byteplus.com/en/docs/ecs/Building-RabbitMQ) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build and use RabbitMQ. |
|[Building a PostgreSQL primary-replica architecture](https://docs.byteplus.com/en/docs/ecs/Building-a-PostgreSQL-primary-replica-architecture) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build and use PostgreSQL. |
|[Building Oracle](https://docs.byteplus.com/en/docs/ecs/Building-Oracle) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build Oracle. |
|[Building Ceph](https://docs.byteplus.com/en/docs/ecs/Building-Ceph) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build Ceph. |


<span id=".5pCt5bu6572R56uZ"></span>
#### Set up websites


|Practice |Description |
|---|---|
|[Building a WordPress blog (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-a-WordPress-blog-CentOS-7) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build a WordPress blog website. |
|[Building a WordPress blog (Ubuntu 18.04)](https://docs.byteplus.com/en/docs/ecs/Building-a-WordPress-blog-Ubuntu-18) |Taking an ECS instance running the Ubuntu 18.04 operating system as an example, this guide introduces how to build a WordPress blog website. |
|[Manually building a WordPress blog site (Windows)](https://docs.byteplus.com/en/docs/ecs/Manually_building_a_WordPress_blog_site) |Taking an ECS instance running the Windows Server 2022 operating system as an example, this guide introduces how to build a WordPress blog website. |
|[Building a Discuz forum](https://docs.byteplus.com/en/docs/ecs/Building-a-Discuz-forum) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build a Discuz forum. |
|[Building a Ghost blog](https://docs.byteplus.com/en/docs/ecs/Building-a-Ghost-blog) |Taking an ECS instance running the Ubuntu 18.04 operating system as an example, this guide introduces how to build a Ghost blog website in a production environment. |
|[Building a Magento website](https://docs.byteplus.com/en/docs/ecs/Building-a-Magento-website) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build a Magento website in a production environment. |
|[Building a Drupal website](https://docs.byteplus.com/en/docs/ecs/Building-Drupal-website) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build a Drupal website in a production environment. |
|[Building a Moodle online course management system](https://docs.byteplus.com/en/docs/ecs/Building-a-Moodla-online-course-management-system) |Taking an ECS instance running the CentOS 8.3 operating system as an example, this guide introduces how to build a Moodle online course management system. |
|[Building a Joomla basic management platform](https://docs.byteplus.com/en/docs/ecs/Building-a-Joomla-basic-management-platform) |Taking an ECS instance running the CentOS 7.8 operating system as an example, this guide introduces how to build a Joomla basic management platform. |
|[Building AMH and setting up a website](https://docs.byteplus.com/en/docs/ecs/Building-an-AMH-website) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build an AMH website in a production environment. |
|[Setting up multiple websites](https://docs.byteplus.com/en/docs/ecs/Building-multiple-websites) |Taking an ECS instance running the CentOS 7.6 operating system as an example, this guide introduces how to build two static web pages on an ECS instance. |


<span id=".6YWN572u5Z-f5ZCN"></span>
### Configure domain name

After you set up a website on an instance, accessing the website directly through the instance's public IP address reduces server\-side security and is more complex. Therefore, for ease of access and use, you can customize a domain name for the website, and then use it to access the website. Specific steps are as follows:


1. Purchase a domain name.

   If you do not have an available domain name, we recommend that you purchase one by using [BytePlus Domain Servic](https://www.byteplus.com/en/product/domain-service)[e](https://www.byteplus.com/en/product/domain-service). Purchase adomain name from the domain name provider.

2. Complete ICP filing.

   If your domain name points to a server in the Chinese mainland that hosts your website, submit an ICP filing application through your server provider (access provider). Otherwise, you can not access the website.

3. Configure website resolution.resolutionresolution

   You need to resolve your domain name to the EIP to access your website.  

4. After completing the above steps, you can input `http://<domain_name>` in the local browser to access the website you build.


<span id="gFsv9vNB"></span>
### Release ECS instances

If you no longer need an ECS instance, you can refer to [Deleting instances](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances) to delete it. After deletion, billing stops and the data cannot be recovered.
