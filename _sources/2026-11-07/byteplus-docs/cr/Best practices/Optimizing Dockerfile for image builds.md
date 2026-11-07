---
title: "Optimizing Dockerfile for image builds"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Optimize_the_Dockerfile"
---

This topic describes how to optimize image build strategies to shorten build time and improve image push and pull efficiency.

## Use Docker 1.10 or later

Docker images are built from multiple intermediate layers. Each instruction in a Dockerfile creates an image layer. In Docker 1.10 and later, Docker pushes as many image layers **concurrently** as possible by default to CR when you push an image.

## Minimize the base image

Reducing image size can shorten image pull time and improve image runtime efficiency. Images stored on Docker Hub may contain dependencies that are unnecessary for the application. You can use smaller community images or build your own minimal usable base image based on Docker's minimal architecture.

For more information about building images, see [Base images](https://docs.docker.com/build/building/base-images/) in the Docker documentation.

## Specify a tag for the base image

When a base image is referenced without a tag, the image tagged `latest` is used by default. Over time, the image associated with the `latest` tag may change. This may cause the entire image to be rebuilt during subsequent image pushes and pulls, increasing image build time.

* Before optimization

   ```Plain Text
   FROM nginx
   
   ADD . /app  
   RUN cd /app && booking install
   
   CMD booking start
   
   ```

* After optimization

   ```Plain Text
   FROM nginx:1.1.0
   
   ADD . /app  
   RUN cd /app && booking install
   
   CMD booking start
   
   ```

## Place frequently changing instructions later

To minimize the time required to rebuild an image and upload its layers, keep the most stable dependencies in the Dockerfile. Place frequently changing dependencies, such as your application's source code, later in the Dockerfile.

Docker caches image layers to accelerate image builds. If the image being built has not changed since the previous build, Docker does not rebuild it. Instead, Docker uses the cached image tag, reducing the build time. However, each image layer depends on the preceding layer. If the preceding layer changes, the current layer is rebuilt even if it remains unchanged. Placing frequently changing dependencies later reduces the number of image layers that must be rebuilt.

In this example, the booking module changes more frequently than Node.js. Therefore, the instructions for booking should be placed later.

* Before optimization

   ```Plain Text
   FROM nginx
   
   ADD . /app
   RUN cd /app && booking install  
   RUN apt-get update && apt-get install -y nodejs
   
   CMD booking start
   
   ```

* After optimization

   ```Plain Text
   FROM nginx
   
   RUN apt-get update && apt-get install -y nodejs  
   ADD . /app
   RUN cd /app && booking install
   
   CMD booking start
   
   ```

## Use combined instructions

Combining instructions can remove unnecessary intermediate files and reduce the image size.

Files created by one instruction remain part of the image even if a later instruction deletes them. They still occupy space in the image but are not visible in Docker containers.

* **Before optimization**

   ```Plain Text
   WORKDIR /tmp
   RUN wget http://booking.com/booking.tar.gz 
   RUN wget tar -xvf booking.tar.gz 
   RUN mv booking/binary /opt/bin/myapp
   RUN rm booking.tar.gz
   ```

* **After optimization**

   ```Plain Text
   WORKDIR /tmp
   RUN wget http://booking.com/booking.tar.gz &&\
       wget tar -xvf booking.tar.gz &&\
       mv booking/binary /opt/bin/myapp &&\
       rm booking.tar.gz
   ```

## Select the nearest region

Select the BytePlus CR region closest to you to reduce latency when pushing or pulling images. For regions supported by CR, see [Available regions](https://docs.byteplus.com/en/docs/cr/Region).

For cross\-border image pushes or pulls, use the Asia Pacific (Johor) region as a transit point. Then, use registry replication to quickly replicate the images. For details, see

[Pushing images across borders to BytePlus CR](https://docs.byteplus.com/en/docs/cr/Push_images_across_borders_to_the_Volcano_Engine_Container_Registry).
