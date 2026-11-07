---
title: "Using KubeCm to manage the kubeconfig files of multiple clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-multi-cluster-KubeConfigs-using-KubeCM"
---

KubeCm facilitates you in flexibly switching between multiple clusters when you use kubectl for cluster management. This topic describes how to use KubeCm to manage VKE clusters of BytePlus.

<span id=".6IOM5pmv"></span>
## Background information

kubectl is the native command\-line tool provided by Kubernetes. You can use the kubectl client to connect to a Kubernetes cluster and perform operations, such as creation, viewing, and deletion, on the cluster.

When connecting to the target cluster with kubectl, first obtain the cluster's kubeconfig access credentials. Then copy them to the `$HOME/.kube/config` file on your local computer.

However, if you manage multiple clusters at the same time, you need to constantly modify the content of the `$HOME/.kube/config` file. Manual merging of kubeconfig files for multiple clusters is inefficient and error\-prone. This topic describes a method of efficiently managing the kubeconfig access credentials of multiple clusters to quickly switch the access credentials.

<span id=".5LuA5LmI5pivLWt1YmVjbe-8nw=="></span>
## What is KubeCm?

KubeCm is a tool for managing the kubeconfig credentials of multiple clusters. KubeCm lets you view, switch between, add, and delete kubeconfig credentials in the `$HOME/.kube/conf` file, simplifying multi\-cluster management.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a detailed introduction to KubeCm, see the <a href="https://kubecm.cloud/">official website</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".546v5aKD5YeG5aSH"></span>
### Preparing environment

The kubectl tool has been installed in the local environment. For details, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).

<span id=".5a6J6KOFLWt1YmVjbQ=="></span>
### Installing KubeCm

Install KubeCm in the local environment. For details, see the [official documentation](https://kubecm.cloud/).

After KubeCm is installed, run the `kubecm` command. If the following content is displayed, it indicates that KubeCm is installed.

```bash
                                                   
        Manage your kubeconfig more easily.        
                                                   

██   ██ ██    ██ ██████  ███████  ██████ ███    ███ 
██  ██  ██    ██ ██   ██ ██      ██      ████  ████ 
█████   ██    ██ ██████  █████   ██      ██ ████ ██ 
██  ██  ██    ██ ██   ██ ██      ██      ██  ██  ██ 
██   ██  ██████  ██████  ███████  ██████ ██      ██

 Tips  Find more information at: kubecm.cloud (https://kubecm.cloud)

Usage:
  kubecm [command]

Available Commands:
  add         Add KubeConfig to $HOME/.kube/config
  alias       Generate alias for all contexts
  clear       Clear lapsed context, cluster and user
  cloud       Manage kubeconfig from cloud
  completion  Generate completion script
  create      Create new KubeConfig(experiment)
  delete      Delete the specified context from the kubeconfig
  help        Help about any command
  list        List KubeConfig
  merge       Merge multiple kubeconfig files into one
  namespace   Switch or change namespace interactively
  rename      Rename the contexts of kubeconfig
  switch      Switch Kube Context interactively
  version     Print version info

Flags:
      --config string   path of kubeconfig (default "/Users/bytedance/.kube/config")
  -h, --help            help for kubecm
  -m, --mac-notify      enable to display Mac notification banner
      --ui-size int     number of list items to show in menu at once (default 4)

Use "kubecm [command] --help" for more information about a command.
```


<span id=".6I635Y-W6ZuG576k6K6_6Zeu5Yet6K-B"></span>
### Obtaining cluster access credentials


2. [the VKE console](https://console.byteplus.com/vke) .

3. In the left navigation bar, click **Cluster**.

4. On the Cluster page, click the name of the target cluster to go to the cluster management page.

5. In the left navigation bar, click **Overview**. On the page that appears, click the **Connection** tab.

6. Click the **Public network ** tab, click **Generate KubeConfig**, and then specify the **Valid period** parameter to generate the cluster access credentials.

6. Click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5e94f5d23a951e48583862d0c818fa2d.png) </span>to download the access credentials to your local computer.


<span id=".5bi46KeB5pON5L2c"></span>
## Common operations

<span id=".5re75Yqg6K6_6Zeu5Yet6K-B"></span>
### Adding access credential


1. Run the following command to add an access credential.


```bash
kubecm add -f kube.conf
```


<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5f66f3787de7d7f695c8f3c8c3776ec.mp4" controls></video>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><code>kube.conf</code> is a sample file name for the kubeconfig access credentials. You need to replace it with your file name accordingly.</div>


* <div data-tips="true" data-tips-type="tip">Before you run the command, make sure that the <code>$HOME/.kube</code> directory already contains the <code>config</code> file. If the file does not exist, an error will be reported when you run the command.</div>


* <div data-tips="true" data-tips-type="tip">When you run the command, if you select <code>True</code>, the access credentials will be written to the <code>$HOME/.kube/config</code> file. If you select <code>False</code>, a <code>./kubecm.config</code> file will be generated in the current folder.</div>


2. If you want to modify the name of the cluster access credentials when you add the credentials, you can add the `-c` parameter and use the `--context-name` parameter to specify the name.


```bash
kubecm add -cf kube.conf --context-name demo-cluster
```


<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_331230bccacb6a7f0fbb77a82f07d5fd.mp4" controls></video>


<span id=".5p-l55yL6ZuG576k5YiX6KGo"></span>
### Viewing the cluster list

Run the following command to view all access credentials.

```bash
kubecm list
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fed9b3eac805dca006242cb8e6f4577e.png) </span>

<span id=".5YiH5o2i6ZuG576k"></span>
### Switching clusters

Run the following command to switch to another access credential.

```bash
kubecm switch
```


<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b6dd742b661ab5a595c7788e645f69c.mp4" controls></video>


<span id=".6YeN5ZG95ZCN6K6_6Zeu5Yet6K-B"></span>
### Rename access credentials

Run the following command to rename the cluster access credentials.

```bash
kubecm rename
```


<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ab34272bbb9ece2fbce7d7a46ec5e1d.mp4" controls></video>


<span id=".56e76Zmk6ZuG576k"></span>
### Removing clusters

Run the following command to remove the cluster access credentials.

```bash
kubecm delete
```


<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5b26cc257fe169968ca1b5f8ffb82c1.mp4" controls></video>
