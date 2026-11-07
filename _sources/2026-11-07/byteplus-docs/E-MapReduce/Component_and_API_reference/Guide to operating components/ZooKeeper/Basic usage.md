---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/zk_basic_usage"
---

<span id="_1-前提条件"></span>
## 1. Prerequisites

A cluster containing the Zookeeper service has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-连接zookeeper"></span>
## 2. Connect to Zookeeper


1. [Log in to the E-MapReduce (EMR) console](https://console.volcengine.com/emr).

2. Click to enter the **Cluster list \> Cluster details \> Service list \> Zookeeper** page.

3. Click the ECS ID of the cluster node (emr\-master\-1\-1 host name) to jump to the cloud server instance page. Click the **Remote connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.

4. Use the following command to enter the **Zookeeper** interactive shell:


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For EMR clusters version 1.3 and later, you can refer to the following path for the location of zkCli.sh. For versions earlier than 1.3, you can use the find command to locate the path of zkCli.sh.</div>


* <div data-tips="true" data-tips-type="warning">The domain name naming method for nodes may differ across EMR versions, so the above "emr\-master\-1\-1 host name" can be adjusted accordingly based on EMR's <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.</div>



```Plain
/usr/lib/emr/current/zookeeper/bin/zkCli.sh -server localhost:2181
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f16447ea52cccf183548372eb158134.png) </span>

A large amount of information will be output during the connection process. Once the connection is successful, you will enter ZooKeeper's interactive mode. You can use the help command to view all available operations.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_370c44b04da73fa5757370fbc94de74a.jpg) </span>

<span id="_3-常见指令"></span>
## 3. Common commands

<span id="_3-1-ls"></span>
### 3.1 ls

```Plain
ls /zookeeper # 查看 zookeeper 节点下的子节点信息
```


<span id="_3-2-get"></span>
### 3.2 get

```Plain
get /zookeeper # 查看该节点上数据信息
```


<span id="_3-3-delete"></span>
### 3.3 delete

```Plain
delete /zookeeper # 删除节点
```


For other commands, refer to the official zk website.
