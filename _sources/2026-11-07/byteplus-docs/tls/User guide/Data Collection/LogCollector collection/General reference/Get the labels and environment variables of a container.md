---
title: "Get the labels and environment variables of a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/the_labels_and_environment_variables_of_a_container"
---

When you create a collection rule for self\-managed Kubernetes containers in the console, you are required to set the container labels and environment variables to specify the containers of which the logs are to be collected. This topic describes how to obtain the labels and environment variables of a container after you log on to its host machine.


* Container label: obtained using the docker inspect command.

* Environment variable: configured when a container is started.


<span id="docker-runtime-场景"></span>
## Docker runtime scenario


1. Log on to the host machine of the container.

2. Run the following command to get the container ID.

   where:

   * hbase is the container name. Replace it with the actual container name in your scenario.

   * The first string in the response is the container ID. For example, `7cbb0bca4d09` in the following figure is a container ID.

   ```shell
   docker ps | grep hbase
   ```
   

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d6b5f7aefbe84bd7eca071b7c14ea828) </span>

3. Run the following command to get the environment variables of the container.

   where:

   * `7cbb0bca4d09` is the container ID. Replace it with the actual container ID in your scenario.

   * The response includes the environment variables of the container.

   ```shell
   docker exec 7cbb0bca4d09 env
   ```
   

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_aacd7e1140fe5b3ab2a06d066322e19e) </span>

4. Run the following command to get the labels of the container.

   where:

   * `7cbb0bca4d09` is the container ID. Replace it with the actual container ID in your scenario.

   * The `Labels` field in the response displays the container labels.

   ```shell
   docker inspect 7cbb0bca4d09
   ```
   

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e6673bbb4f73feef43c4ffa6acd92c2d) </span>


<span id="containerd-runtime-场景"></span>
## Containerd runtime scenario


1. Log on to the host machine of the container.

2. Run the following command to get the container ID.

   where:

   * `ntp` is the container name. Replace it with the actual container name in your scenario.

   * The first string in the response is the container ID. For example,`95f7dbb305ade` in the following figure is a container ID.

   ```shell
   crictl ps | grep ntp
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfde91facba648089e87a2c87a85f08b~tplv-goo7wpa0wc-image.image) </span>

3. Run the following command to get the environment variables of the container.

   where:

   * `95f7dbb305ade` is the container ID. Replace it with the actual container ID in your scenario.

   * The response includes the environment variables of the container.

   ```shell
   crictl exec 95f7dbb305ade env
   ```
   

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e85b4c11b4964efa2d033f94cd036757) </span>

4. Run the following command to get the labels of the container.

   where:

   * `95f7dbb305ade` is the container ID. Replace it with the actual container ID in your scenario.

   * The `Labels` field in the response displays the container labels.

   ```shell
   crictl inspect 95f7dbb305ade
   ```
   

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b75e02a920b340e442b782a2ff530d8f) </span>
