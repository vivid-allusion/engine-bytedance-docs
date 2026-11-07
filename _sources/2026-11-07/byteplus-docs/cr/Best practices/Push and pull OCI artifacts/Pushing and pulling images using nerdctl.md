---
title: "Pushing and pulling images using nerdctl"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/push-and-pull-images-using-nerdctl"
---

CR supports image push, pull, and other operations through command\-line tools. This topic describes how to push and pull images in CR using the mainstream command\-line tool nerdctl.

## Prerequisites

You need to first obtain the access domain name, namespace name, OCI artifact repository name, and other information for the CR instance. Then, use this information with nerdctl commands to push and pull images.

* [nerdctl](https://github.com/containerd/nerdctl#install) has been installed.

* A CR Standard Edition instance has been created, and its access domain name has been obtained. For detailed operations, see [Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* The username and password for logging in to the instance have been obtained. For details, see [Standard Edition instance access credentials](https://docs.byteplus.com/en/docs/cr/Get-access-credentials).

* A CR namespace has been created, and its name has been obtained. For details, see [Creating namespaces](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

* An OCI artifact repository has been created. For details, see [Creating OCI artifact repositories](https://docs.byteplus.com/en/docs/cr/Creating_OCI_artifact_repositories) **.**

> **tip**

> This topic uses macOS as an example to describe how to use CR through nerdctl. macOS does not support running nerdctl directly. You must use nerdctl with a virtual machine provided by Lima. For details, see [nerdctl/macOS](https://github.com/containerd/nerdctl#macos).

## Step 1: Log in to the CR instance

After obtaining the username, password, and access domain name of the CR instance, execute the following command to log in to the instance:

```Plain Text
lima nerdctl login --username=[Username] --paasword=[Password] [Access domain name]
```

**Example command**

```Plain Text
lima nerdctl login --username=*****@210013**** --paasword=******* enterprise-1-cn-guangzhou.cr.volces.com
```

**Example result**

If `Login Succeeded` appears, the logon is successful.

```Plain Text
WARN[0000] WARNING! Using --password via the CLI is insecure. Use --password-stdin. 
WARNING: Your password will be stored unencrypted in /home/bytedance.linux/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

## Step 2: Obtain the image ID

Before pushing or pulling an image, obtain the ID of the image. In this example, the image ID is `e3b7de64****` in the IMAGE ID column.

**Command**

```Plain Text
lima nerdctl images
```

**Example output**

```Plain Text
REPOSITORY    TAG       IMAGE ID        CREATED              PLATFORM       SIZE        BLOB SIZE
nginx         alpine    e3b7de64****    About an hour ago    linux/amd64    26.4 MiB    9.8 MiB
```

## Step 3: Set an image tag

Create an alias for the image in the target OCI artifact repository and set an image tag. In this example, the alias is `enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****:nerdctl`.

**Command**

```Plain Text
lima nerdctl tag [ImageId]  [Access domain name]/[Namespace]/[OCI repository name]:[Image tag]
```

**Example command**

```Plain Text
lima nerdctl tag e3b7de64**** enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****:nerdctl 
```

**Example output**

After the command is executed, the new image appears under the target OCI artifact repository with the `nerdctl` tag.

```Plain Text
REPOSITORY                                                        TAG        IMAGE ID        CREATED              PLATFORM       SIZE        BLOB SIZE
nginx                                                             alpine     e3b7de64****    About an hour ago    linux/amd64    26.4 MiB    9.8 MiB
enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****    nerdctl    e3b7de64****    10 seconds ago       linux/amd64    26.4 MiB    9.8 MiB

```

## Step 4: Push the image

Push the tagged image to CR.

**Command**

```Plain Text
lima nerdctl push [Access domain name]/[Namespace]/[OCI repository name]:[Image tag]
```

**Example command**

```Plain Text
lima nerdctl push enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****:nerdctl 
```

**Example output**

After the command is executed, you can view the pushed image in the console.

## Step 5: Pull the image

After logging in to CR, you can also pull hosted images from it.

**Command**

```Plain Text
lima nerdctl pull [Access domain name]/[Namespace]/[OCI repository name]:[Image tag]
```

**Example command**

```Plain Text
lima nerdctl pull enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****:latest
```

**Example output**

```Plain Text
REPOSITORY                                                        TAG        IMAGE ID        CREATED           PLATFORM       SIZE        BLOB SIZE
nginx                                                             alpine     e3b7de64****    2 days ago        linux/amd64    26.4 MiB    9.8 MiB
enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****    latest     b04121cfcd5d    28 seconds ago    linux/amd64    1.3 MiB     773.3 KiB
enterprise-1-cn-guangzhou.cr.volces.com/vpc-****/vpc-j7w2****    nerdctl    e3b7de64****    2 days ago        linux/amd64    26.4 MiB    9.8 MiB
```
