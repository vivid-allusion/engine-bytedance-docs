---
title: "How to call inference services (new)"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Howtocallinferenceservices_new"
---

After the service is successfully deployed, the service can be invoked through the access address and sample code.

<span id="使用前提"></span>
# premise of use


1. There are \> = 1 services in [inference services].

2. The state of the service to be invoked is `running`.


<span id="操作步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click [Model Services] \- [Inference Services] in the left navigation bar to enter the list page.

2. On the list page, click a service name to enter the details page, and click [Call Guide] to view the access address and sample code of the service. For ease of understanding, the following parameters are specifically explained:



|**Parameter** |**Note** |
|---|---|
|API gateway call |* When selecting the API gateway, the domain name calling method is supported, and "token verification" is enabled. However, the token valid period is 7 days by default, please ensure timely update.<br><br>* After opening the API gateway and enabling token verification, refer to the service call method:<br><br><br>```Plain```<br>```curl 访问地址 -H "Authorization: Bearer + Token"```<br><br><br><br>* Supports four listening/access ports<br><br>   * HTTP 1.1<br><br>   * HTTP 2<br><br>   * GRPC<br><br>   * Metrics |
|CLB call |* When CLB is selected, the service can be accessed by requesting IP: Port.<br><br>   * When creating/upgrading a service, add an access configuration, and the service will be assigned to the corresponding private IP/public IP.<br><br>* If the service does not add an access configuration, you need to view the IP and Port of an instance in the instance list.<br><br>   * Services provided by a service instance can be accessed through IP: PORT in the Dev boxes.<br><br>* CLB supports three listening/access ports<br><br>   * HTTP<br><br>   * RPC<br><br>   * Metrics |
|VPC access address (single network interface card) |* If the service adds a private network and subnet, the VPC access address is displayed.<br><br>* On a machine connected to the private network, the service can be accessed by requesting this address. |
|VPC access address (dual network interface card) |* If the service adds a private network, subnet, and load balancer, the VPC access address is displayed.<br><br>* On a machine connected to the private network, the service can be accessed by requesting this address. |
|Public network access address |* If the service has public access enabled, the public access address is displayed.<br><br>* Request this address on the public network to access the service. |



3. For inference services using pre\-built mirrors, the platform provides HTTP and RPC access methods and sample code.

   1. Copy the sample code to a machine that keeps the network unobstructed with the access address, and modify the relevant paragraphs in the sample code based on the real input and output information of the model.

   2. Execute the sample code and feed the test data to get the inference result of the inference service.

4. For inference services that use non\-preconfigured mirrors, users need to construct their own requests based on the code in the mirror and invoke the service through the access address.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1e7f3c81d324b8fbea8f1fead0e5f41~tplv-goo7wpa0wc-image.image) </span>
