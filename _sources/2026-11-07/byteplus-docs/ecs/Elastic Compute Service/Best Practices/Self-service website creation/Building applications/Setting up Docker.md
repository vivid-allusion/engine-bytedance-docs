---
title: "Setting up Docker"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-Docker"
---

This topic describes how to deploy Docker CE on Linux instances, as well as common Docker operations and the image creation process.

<span id=".5YWz5LqORG9ja2Vy"></span>
## About Docker

Docker is an open\-source application container engine. It packages applications and their dependencies into virtual containers, which can run on any computer with Linux, Windows, or macOS. This capability allows applications to operate seamlessly across diverse environments, including local systems, public clouds, and private clouds. For more information, visit [Docker docs](https://docs.docker.com/).

The following items describe the main components of Docker:


* Docker client

* Docker Daemon

* Docker image

* Docker container


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [associated an EIP with it](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The ECS instance status is **Running**.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5a6J6KOFIERvY2tlcg=="></span>
### Install Docker


<Tabs>
<Tab zoneid="Et0fiQLHpw" title="veLinux 1.0/veLinux 2.0">
<TabTitle>veLinux 1.0/veLinux 2.0</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the packages that allow APT to use software repositories over HTTPS:

   ```Bash
   sudo apt install -y ca-certificates curl gnupg lsb-release
   ```
   

3. Execute the following command to add the official Docker GPG key.

   ```Bash
   sudo mkdir -p /etc/apt/keyrings
   curl -fsSL https://mirrors.ivolces.com/docker/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```
   

4. Execute the following command to add the Docker software repository information.

   
   <Tabs>
   <Tab zoneid="Iphwps4oQC" title="veLinux 1.0">
   <TabTitle>veLinux 1.0</TabTitle>
   
   ```Bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/debian buster stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="aRZ06maDBJ" title="veLinux 2.0">
   <TabTitle>veLinux 2.0</TabTitle>
   
   ```Bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Execute the following command to update the software repository.

   ```Bash
   sudo apt update
   ```
   

6. Execute the following command to install Docker CE.

   ```Bash
   sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
   ```
   

7. Execute the following command to run Docker.

   ```Bash
   systemctl start docker
   ```
   

8. Execute the following command to check whether Docker is installed as expected.

   ```Bash
   docker info
   ```
   

   If the output is as shown below, Docker has been successfully installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03f74bc6e7e2ce00c0bcd30e001e12da.png) </span>


</Tab>
<Tab zoneid="dBGHYjg9q8" title="CentOS 7.x/Stream 8/Stream 9">
<TabTitle>CentOS 7.x/Stream 8/Stream 9</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the required system tools.

   ```Bash
   sudo yum install -y yum-utils 
   ```
   

3. Execute the following command to add the Docker software repository information.

   ```Bash
   sudo yum-config-manager --add-repo https://mirrors.ivolces.com/docker/linux/centos/docker-ce.repo
   sudo sed -i 's+download.docker.com+mirrors.ivolces.com/docker+' /etc/yum.repos.d/docker-ce.repo
   ```
   

4. Execute the following command to update the software repository.

   ```Bash
   sudo yum makecache
   ```
   

5. Execute the following command to install Docker CE.

   ```Bash
   sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```
   

6. Execute the following command to run Docker.

   ```Bash
   systemctl start docker
   ```
   

7. Execute the following command to check whether Docker is installed as expected.

   ```Bash
   docker info
   ```
   

   If the output is as shown below, Docker has been successfully installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0da44c8592c21b39f125698f183fb6cc.png) </span>





</Tab>
<Tab zoneid="gCoWltAe4M" title="Ubuntu 18.04/20.04/22.04/24.04">
<TabTitle>Ubuntu 18.04/20.04/22.04/24.04</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the packages that allow APT to use software repositories over HTTPS:

   ```Bash
   sudo apt install -y ca-certificates curl gnupg lsb-release
   ```
   

3. Execute the following command to add the official Docker GPG key.

   ```Bash
   sudo mkdir -p /etc/apt/keyrings
   curl -fsSL https://mirrors.ivolces.com/docker/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```
   

4. Execute the following command to add the Docker software repository information.

   ```Bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
   

5. Execute the following command to update the software repository.

   ```Bash
   sudo apt update
   ```
   

6. Execute the following command to install Docker CE.

   ```Bash
   sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
   ```
   

7. Execute the following command to run Docker.

   ```Bash
   systemctl start docker
   ```
   

8. Execute the following command to check whether Docker is installed as expected.

   ```Bash
   docker info
   ```
   

   If the output is as shown below, Docker has been successfully installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17193b4d4f1a82eb7be7d209da2180ee.png) </span>


</Tab>
<Tab zoneid="HgzL3Triy1" title="Debian 10/11/12">
<TabTitle>Debian 10/11/12</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install the packages that allow APT to use software repositories over HTTPS:

   ```Bash
   sudo apt install -y ca-certificates curl gnupg lsb-release
   ```
   

3. Execute the following command to add the official Docker GPG key.

   ```Bash
   sudo mkdir -p /etc/apt/keyrings
   curl -fsSL https://mirrors.ivolces.com/docker/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```
   

4. Execute the following command to add the Docker software repository information.

   ```Bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
   

5. Execute the following command to update the software repository.

   ```Bash
   sudo apt update
   ```
   

6. Execute the following command to install Docker CE.

   ```Bash
   sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
   ```
   

7. Execute the following command to run Docker.

   ```Bash
   systemctl start docker
   ```
   

8. Execute the following command to check whether Docker is installed as expected.

   ```Bash
   docker info
   ```
   

   If the output is as shown below, Docker has been successfully installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_faae2c38f5b14ea91241294c33a553a9.png) </span>


</Tab>
</Tabs>


<span id=".5L2_55SoIERvY2tlcg=="></span>
### Use Docker

<span id=".566h55CGIERvY2tlciDlrojmiqTov5vnqIs="></span>
#### Manage the Docker daemon

```Bash
systemctl start docker    # Run the Docker daemon.
systemctl stop docker     # Stop the Docker daemon.
systemctl restart docker  # Restart the Docker daemon.
```


<span id="AxYnE41m"></span>
#### Manage mirror sites

When image pulls from the official Docker repository fail, you can configure one or multiple reliable and available mirror sites. Docker will pull images from the mirror site you specify, improving pull reliability and speed.


1. Edit the Docker configuration file.

   ```Bash
   sudo vim /etc/docker/daemon.json
   ```
   

2. Press `i` to enter edit mode, and enter the mirror site you need in the `registry-mirrors` structure.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>https://registry-1.docker.io</code> and <code>https://registry-2.docker.io</code> with the mirror sites you need. Separate multiple sources with <code>,</code>.   </div>
   

   ```JSON
   {
     "registry-mirrors": [
       "https://registry-1.docker.io",
       "https://registry-2.docker.io"
     ]
   }
   ```
   

3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to restart the Docker service.

   ```Bash
   sudo systemctl daemon-reload && sudo systemctl restart docker
   ```
   


<span id=".566h55CG6ZWc5YOP"></span>
#### Manage images


* **Pull images**

   In the example provided in this topic, the Ubuntu image is used.

   ```Bash
   docker pull ubuntu
   ```
   

* **View the existing images**

   ```Bash
   docker images
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3d435130eb9090a7ff92b9aeb61316e.png) </span>

* **Forcibly delete an image**

   ```Bash
   docker rmi -f ubuntu
   ```
   

   After you delete an image, you can execute the `docker images` command to check whether the image is deleted.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe1ee02616a1b2f20fa44137369474fa.png) </span>


<span id=".566h55CG5a655Zmo"></span>
#### Manage containers


* **Enter a container**

   ```Bash
   docker run -it <ImageId> /bin/bash
   ```
   

   You can execute the `docker images` command to get `<ImageId>` in the preceding command.

* **Exit a container**

   Execute the `exit` command to exit the current container.

* **Run a container in the background**

   ```Bash
   docker run -d --name ubuntu ImageId
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <code>--name</code> option specifies <code>ubuntu</code> as the container name.   </div>
   

* **Enter a container running in the background**

   ```Bash
   docker exec -it <Container ID> /bin/bash
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><Container ID></code> with the actual container ID, which you can obtain by executing the <code>docker ps</code> command.   </div>
   

* **Create an image from a container**

   ```Bash
   docker commit <Container ID OR Container Name> [<Repository Name>[:<Tags>]]
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><Container ID OR Container Name></code> with the actual container ID or name, <code><Repository Name></code> with the actual repository name, and <code><Tags></code> with the actual repository tags. Example: <code>docker commit 097fdd5e**** dockertest/ubuntu:latest</code>.   </div>
   

<span id=".5Yi25L2c6ZWc5YOP"></span>
#### Create an image


1. Execute the following command to create and edit a Dockerfile.

   ```Bash
   vim Dockerfile
   ```
   

2. Press `i` to enter edit mode and add the following content.

   ```Dockerfile
   FROM nginx
   RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
   ```
   

   The following items describe simple instructions in the Dockerfile. For more information, visit [the official website](https://hub.docker.com/).

   * FROM statement: Indicates that the Nginx image is used as the base image. In a Dockerfile, the FROM instruction is required and must be the first instruction.

   * RUN statement: The format is `RUN <command>`. For example, if the command in the statement is `echo` "Hello, Docker!", `Hello, Docker!` is displayed after you execute the statement.

3. Press the `Esc` key, enter `:wq`, and then press Enter to save and exit the Dockerfile.

4. Execute the following command to create an image.

   ```Bash
   docker build -t nginx:v1 .            # .  specifies the path to the Dockerfile and cannot be omitted.
   docker images                         # Check whether the image is created.
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a6b8480cc7b8332fab780b13d2b7f2.png) </span>

5. Execute the following commands to run and view the containers.

   ```Bash
   docker run -d nginx:v1                # Run containers in the background.
   docker ps                             # View currently running containers.
   docker ps -a                          # View all containers, including containers that are not running.
   docker logs CONTAINER ID/NAMES        # If no running containers are displayed, use the container ID or name to check the startup logs for troubleshooting purposes.
   ```
   

6. Execute the following command to create an image.

   ```Bash
   docker commit bd0d3e7e**** nginxtest:v1     # Add the container ID, along with the name and version number of the new image, after the commit parameter.
   docker images                               # List local (downloaded and locally created) images.
   ```
   

7. Push the image to the remote repository.

   By default, the image is pushed to Docker Hub. You need to first log in to Docker, associate tags with the image, and name the image in the format of `[Docker User Name]/[Image Name]:[Tag]`. The push is complete.

   ```Bash
   docker login
   docker tag [ImageId] [Docker User Name]/[Image Name]:[Tag]
   docker push [Docker User Name]/[Image Name]:[Tag]
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>[Docker User Name]</code> with your actual Docker username, <code>[Image Name]</code> with the actual image name, and <code>[Tag]</code> with the actual image tag.   </div>
   

8. Log in to [Docker Hub](https://hub.docker.com/) to view the image.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/2d79ee63d2a14b4d942cce71b48fe5f0.png) </span>
