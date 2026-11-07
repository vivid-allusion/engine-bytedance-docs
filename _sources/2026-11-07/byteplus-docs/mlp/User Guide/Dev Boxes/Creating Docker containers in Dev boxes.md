---
title: "Creating Docker containers in Dev boxes"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Creating_Docker_containers_in_Dev_boxes"
---

Machine Learning Platform supports the use of Docker in Dev boxes. After the Dev boxes are created, the platform has pre\-installed Docker users without installation

<span id="使用限制"></span>
## Usage Limitations


1. When using Docker, please ensure the cloud disk capacity space of the current Dev boxes (check the cloud disk capacity by `df -h`)

2. Creating and running privileged containers through Docker is not supported


<span id="如何在开发机使用docker"></span>
## How to use Docker in Dev boxes


1. Create Dev boxes and log in to Dev boxes WebIDE

2. Use Docker related commands in Dev boxes Terminal

   Example: `Docker run hello-world`, start a `hello world`image in Dev boxes, and see the output to prove that the Docker of Dev boxes can run normally

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5ca2a16042cae23961d13b64f6da0e0.png) </span>

    &nbsp;


<span id="how-to-mount-storage-in-a-docker-container"></span>
## How to mount storage in a Docker container

Dev boxes support mounting shared storage within Docker

<span id="挂载开发机内的路径"></span>
### Mounting Dev boxes


1. Shared storage mounted when creating Dev boxes

2. When the Dev boxes are running, mount the shared storage container path of mount to the Docker container

3. Use the command `docker run -it -v /root/code:/mymount yourdockerimage bash`

   1. `/root/code`: that is, your path inside the Dev box container

   2. `/mymount`: the path you want to mount inside the docker container

   3. `Replace yourdockerimage`with the docker image you need to pull up

   4. If you encounter insufficient permissions during use, please add a command `--userns = host`to change the namespace to be consistent with the host, for example: `docker run -it --userns = host -v /root/code:/mymount yourdockerimage bash`

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_52ec9d156c813b2a7c18a6f6f8d79825.png) </span>


<span id="挂载开发机内共享存储路径（vepfs-cloudfs-nas）"></span>
### Shared storage path inside mount Dev boxes (vePFS/CloudFS/NAS)


1. Shared storage mounted when creating Dev boxes

2. When the Dev boxes are running, mount the shared storage container path of mount to the Docker container

3. Use the command `docker run -it -v /myvepfs:/vepfs yourdockerimage bash`

   1. `/myvepfs`: that is, the vePFS path you mount inside the Dev boxes container

   2. `/vepfs`: that is, the vePFS path you want to mount inside the docker container

   3. `Replace yourdockerimage`with the docker image you need to pull up


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e1cb391e4324f858fd903a1f376c4e8~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c6ee74c8bcce8ea2535aa56cdfe3825.png) </span>

4. If you encounter insufficient permissions during mount vePFS, please add a command `--userns = host`to change the namespace to be consistent with the host, for example: `docker run -it --userns = host -v /myvepfs:/vepfs yourdockerimage bash`

> If you previously used `docker run -it -v /mnt/vepfs`to mount vePFS in a docker container, this feature will not affect the use of the existing container, but the newly created container needs to switch to the new mount method above


<span id="在docker容器指定gpu数量"></span>
## Specify the number of GPUs in the Docker container

The platform supports specifying the number of GPUs used by the Docker container when launching it.

```bash
docker run -d --gpus 4 busybox:latest sleep inf  ##the unmber of assigned GPU docker run -d --gpus '"device=all"' busybox:latest sleep inf ##指定全部GPU
```


If you need to specify a card to run Docker containers, specify it through `NVIDIA_VISIBLE_DEVICES`.

```bash
docker run -d --gpus '"device=GPU-c9fd4329-d60c-0caf-4c2e-2a5a81207d0x,GPU-c9fd4329-d60c-0caf-4c2e-2a5a81207d0y"' busybox:latest sleep inf
```


> How to view the `NVIDIA_VISIBLE_DEVICES`, please find it in the Dev boxes container with the following command:

> ```bash

```



env|grep NVIDIA_VISIBLE_DEVICES

```Plain Text

```
