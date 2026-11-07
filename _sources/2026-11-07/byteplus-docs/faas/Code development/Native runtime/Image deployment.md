---
title: "Image deployment"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_runtime_Image_Deployment"
---

Native functions support two methods of deployment: package deployment and Image Deployment. Before carrying out Image Deployment, you need to write a Dockerfile yourself, build the completed code package into an image, and upload it to the Container Registry in the same region as BytePlus. This topic introduces how to build an image.

<span id="background-information"></span>
## Background information

Image deployment includes the following processes:


1. Building the image: Users independently write Dockerfile, build the completed code package into an image, and upload it to the Container Registry in the same region as BytePlus.

2. Create a function: The function service will play the service role for that function, accessing the BytePlus Container Registry to pull the image. Once pulled successfully, the image will be synchronized to the Function Service.

3. Release function: After releasing a specified image tag, the current service will take over all requests.


<span id="prerequisites"></span>
## Prerequisites

The Container Registry has been activated. Container Registry instance has been created with a set access password, and both namespace and OCI artifact repository have been created. For more details, refer to [Getting Started with Container Registry](https://docs.byteplus.com/en/docs/cr/getting-started).

<span id="limits"></span>
## Limits


* HTTP Service Requirements

   * The service requires a startup script run.sh, which must be copied to the following container directory: /opt/application/run.sh.

   * The service must start within 120 seconds; otherwise, the following errors will occur.

      ```shell
      {
          Status: "failed"
          StatusMessage: "Function cold start timeout, please check your log/code and then retry, or contact oncall"
      }
      ```
      

* File Read and Write Permissions in Container

   The container's run\-as\-user UID is set to root. The Function Service will run your container image as root. If you have specified a specific user in the Dockerfile, the container image will not run as that user currently.

* Container Image Size Limit

   The maximum size of a container image must not exceed 10 GiB.


<span id="procedure"></span>
## Procedure


1. Write a Dockerfile in the current directory of your project. The following is an example Dockerfile for a Golang HTTP service.


```dockerfile
FROM golang:latest

Copy files from the current (host) directory to the /opt/application directory on Docker.
COPY ./output/main /opt/application/main
COPY run.sh /opt/application/run.sh

Set up the working directory
WORKDIR /opt/application
USER root

File to be executed to start docker
CMD /opt/application/run.sh
```



2. Execute the following command to specify the Container Registry, `IMAGE_NAM`E should be replaced with your image name. Assuming the region of the Function Service is `Johor`, your image name would be: `xxx-ap-southeast-1.cr.bytepluses.com/faas/native-image-go:latest`.

   ```shell
   # export IMAGE_NAME=[Container Registry Instance domain name]/[namespace]/[OCI artifact repository]:[image tag]
   export IMAGE_NAME="xxx-ap-southeast-1.cr.bytepluses.com/faas/native-image-go:latest"
   ```
   

3. Execute the following command to build the image.

   ```shell
   docker build -t $IMAGE_NAME .
   ```
   

4. Execute the following command to push the image to the Container Registry.

   ```shell
   export UserName="xxx" # UserName can be obtained from the Container Registry console
   export PassWord="xxx" # PassWord is the access password for the Container Registry Instance set in the prerequisites
   docker login --username=$UserName --password=$PassWord xxx-ap-southeast-1.cr.bytepluses.com
   docker push $IMAGE_NAME
   ```
   


<span id="what-to-do-next"></span>
## What to do next


1. In the [Function Service console](https://console.byteplus.com/vefaas), create a function, and select **Web Application**, and for the deployment method, select **Container image**. For specific actions, refer to [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications).

2. Release your function image and configuration to the cloud. For specific actions, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).
