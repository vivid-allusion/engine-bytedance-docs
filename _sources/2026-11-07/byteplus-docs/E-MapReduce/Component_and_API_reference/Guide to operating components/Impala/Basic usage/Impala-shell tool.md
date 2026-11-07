---
title: "Impala-shell tool"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Impala-shell_tool"
---

Impala\-shell is the official command\-line tool provided by Impala that allows you to connect to Impala.

The emr\-master\-1\-1 node of Volcano Engine E\-MapReduce (EMR) (that is, the node where statestored and catalogd are located) has impala\-shell installed, and impala\-shell has been added to the system environment variables. You can use it directly from the command line.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The domain naming conventions for nodes may differ between EMR versions, so the "emr\-master\-1\-1" above can be adjusted according to EMR's <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.</div>


<span id="_1-使用前提"></span>
## **1. Prerequisites for use**


1. An EMR cluster containing the Impala component service has been created. For details, see [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).

2. Currently, the Impala component is available only to users on the allowlist. You can apply for access using the method described in [Impala-shell tool](https://docs.byteplus.com/docs/E-MapReduce/109294).


<span id="_2-访问未开启-ldap-的-impala"></span>
## 2. Accessing Impala without LDAP enabled


1. Use SSH to log in to the emr\-master\-1\-1 node of the cluster, that is, the node where statestored and catalogd are located. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Use the impala\-shell command


```shell
root@emr-4nw5w1f78f3lxxx-master-1:~# impala-shell
/opt/emr/2.0.0/impala-3.4.1/shell/impala-shell-3.4.1-RELEASE/ext-py2/bitarray-0.9.0-py2.7-linux-x86_64.egg/bitarray/_bitarray.py:3: UserWarning: Module backports was already imported from None, but /usr/lib/python2.7/dist-packages is being added to sys.path
Starting Impala Shell without Kerberos authentication
Opened TCP connection to emr-4nw5w1f78f3lxxx-master-1:21000
Connected to emr-4nw5w1f78f3lxxx-master-1:21000
Server version: impalad version 3.4.1-RELEASE RELEASE (build eb1ed66fa435a722fa8c6a7c58ff53edc10c572e)
***********************************************************************************
Welcome to the Impala shell.
(Impala Shell v3.4.1-RELEASE (eb1ed66) built on Fri Sep 16 15:03:38 CST 2022)
 
Press TAB twice to see a list of available commands.
***********************************************************************************
[emr-4nw5w1f78f3lxxx-master-1:21000] default>
```


<span id="_3-访问已开启-ldap-的-impala"></span>
## 3. Accessing Impala with LDAP enabled


1. Use SSH to log in to the emr\-master\-1\-1 node of the cluster, that is, the node where statestored and catalogd are located. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Use the impala\-shell command


```shell
impala-shell -l --auth_creds_ok_in_clear -u impala
```


Enter the Impala password at the prompt.

For information on how to obtain the Impala username and password, see: [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).
