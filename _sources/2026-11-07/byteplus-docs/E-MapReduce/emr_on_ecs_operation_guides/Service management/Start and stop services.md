---
title: "Start and stop services"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_start_and_stop_services"
---

This article describes how to start and stop service processes in Volcano Engine E\-MapReduce (EMR) clusters, enabling you to independently maintain your cluster.

<span id="_1-前提条件"></span>
## **Prerequisites**

The cluster has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-查看环境变量"></span>
## **View environment variables**


1. Log in to the cluster. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Enter the `env` command. The output is as follows. The specific environment variable configuration depends on your actual environment.


```shell
SSH_CONNECTION=100.64.15.155 25717 192.168.0.187 22
LANG=en_US.UTF-8
XDG_SESSION_ID=27606
USER=root
PWD=/root
HOME=/root
SSH_CLIENT=100.64.15.155 25717 22
SPARK_HOME=/opt/tiger/current/spark
SSH_TTY=/dev/pts/1
MAIL=/var/mail/root
TERM=xterm
SHELL=/bin/bash
SHLVL=1
LOGNAME=root
XDG_RUNTIME_DIR=/run/user/0
_=/usr/bin/env
shell
```


<span id="_3-启停服务进程"></span>
## **Start and stop service processes**

You can perform **Start**, **Stop**, and **Restart** operations for specified services in the EMR console. The operations for each service process are similar. The following example uses HDFS to demonstrate how to operate the corresponding process on the cluster host.


1. Log in to ([E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)).

2. In the top menu bar, select the region.

3. In the left navigation bar, click **Resource Management \> on ECS \> Cluster Name** to enter the cluster details page.

4. Click the **Service list**tab to enter the cluster service management list.

5. In **Service list**, locate the service you want to operate, for example, the row where HDFS is located.

   In the **Service operations**column, you can perform the following operations:

   1. Start

      * Click the **Service operations**column and then the **Start** button.

      * In **Execution Scope**, select the target instance node where you want to execute the command.

      * Enter operation remarks.

      * Click the **Confirm** button to complete the service start. After refreshing the page, HDFS in **Warning** status will return to **Normal Service** status.

   2. Stop

      * Click the **Service operations**column and then the **Stop** button.

      * In **Execution Scope**, select the target instance node where you want to execute the command.

      * Enter operation remarks.

      * Click the **Confirm** button to complete the service stop. After refreshing the page, the service status of HDFS changes to **Warning**.

   3. Restart component

      * Click the **Service operations**column and then the **Restart** button. Select **Restart all components**all or a single component.

      * In **Execution Scope**, select the target instance node where you want to execute the command.

      * Enter operation remarks.

      * Click the **Confirm** button to complete the service restart. After refreshing the page, HDFS in **Normal** status will enter **Warning status**. After the component has finished restarting, refresh the page. HDFS will then be in **Normal** status.

   4. Rebalance

      * Click the **Service operations**column and then the **Rebalance** button.

      * In **Execution Scope**, select the target instance node where you want to execute the rebalance command.

      * Enter operation remarks.

      * Click the **OK** button to initiate the Rebalance operation. Wait for the execution to finish to achieve balanced disk space usage across nodes.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The Rebalance usage balancing operation can only be performed in the HDFS service.      </div>
