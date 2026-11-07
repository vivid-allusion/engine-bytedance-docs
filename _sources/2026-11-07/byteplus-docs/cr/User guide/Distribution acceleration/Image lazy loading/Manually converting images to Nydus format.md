---
title: "Manually converting images to Nydus format"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Manually_convert_an_image_to_Nydus_format"
---

Image lazy loading conversion only supports images up to a certain capacity limit. If your image capacity is 60 GiB or larger, manually convert the image to the Nydus format.

After manual conversion, you can push the converted image to CR. Your workloads can then use the accelerated image to reduce container startup time and improve development efficiency.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".56ys5LiA5q2l77ya5LiL6L295bm25a6J6KOFIE55ZHVz"></span>
### Step 1: Download and install Nydus


1. Download the corresponding tool from [Release Nydus Image Service v2.1.6 · dragonflyoss/nydus](https://github.com/dragonflyoss/image-service/releases/tag/v2.1.6).

2. Extract and add to PATH. The sample code is as follows.

   ```plain
   tar -zxvf nydus-static-v2.1.6-linux-amd64.tgz  -C /usr/local/bin
   export PATH=$PATH:/usr/local/bin/nydus-static
   ```
   


<span id=".56ys5LqM5q2l77ya6L2s5YyW5Li6IE55ZHVzIOagvOW8jw=="></span>
### Step 2: Convert the image to Nydus format


1. Log in to the CR.

   ```sh
   docker login --username=<Account-Username>@<UserID> <Standard-Instance-Name>-<Region>.cr.volces.com
   ```
   

   Example

   ```sh
   docker login --username=v**@1007*** test1-ap-southeast-1.cr.bytepluses.com
   ```
   

2. Manually execute the Nydus conversion command.

   ```sh
   nydusify convert --source <srcImage> --target <srcImage>-nydus
   ```
   

   Example

   ```sh
   nydusify convert --source nginx:stable-alpine3.20-perl --target nginx:stable-alpine3.20-perl-nydus
   ```
