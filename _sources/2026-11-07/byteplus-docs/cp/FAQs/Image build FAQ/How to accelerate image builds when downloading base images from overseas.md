---
title: "How to accelerate image builds when downloading base images from overseas"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_accelerate_image_builds_when_downloading_base_images_from_overseas"
---

When downloading the base image from overseas, network issues may result in slow overall image build times. It is recommended to first store base images from overseas sources in the BytePlus image repository, and then download the base image from the repository when building the image using the Dockerfile to improve build speed. This article uses the base image `Nginx` as an example. The specific actions are as follows:


1. Pull the overseas base image to your local machine.


```shell
docker pull nginx
```



2. Push the local base image to the BytePlus image repository in the Chinese mainland region. For detailed steps, see [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


```shell
docker login --username=xxx@2100****** cr-cn-beijing.volces.com
docker tag nginx cr-cn-beijing.volces.com/yournamespace/nginx:lastest
docker push cr-cn-beijing.volces.com/yournamespace/nginx:lastest
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The image repository must be set to public; otherwise, the pipeline (using the public resource pool) will not be able to pull your base image.</div>



3. Modify the base image address in the Dockerfile and download the image from your own image repository.


```shell
FROM cr-cn-beijing.volces.com/yournamespace/nginx:lastest
```
