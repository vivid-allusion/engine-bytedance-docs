---
title: "Access an instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/accessing"
---

The instance enables private network access by default, allowing direct access from ECS within the same VPC environment. Public network access can also be enabled to access the instance directly using a public address. This topic describes how to access the instance.

<span id="3d8577e5"></span>
## Prerequisites


* If you want to access the instance via a public address, you need to enable the instance's public network access and obtain the instance's public network access address first. For detailed steps, see [Configure instance public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access).

* Instance private network access is enabled by default, allowing direct access from ECS within the same VPC environment. To learn how to create an ECS, see [Purchase an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id="f0af5744"></span>
## Access the instance using a public address

After enabling the instance's public network access, you can directly access the instance using its public network access address.


1. Enter the instance's public network access address in the browser address bar, then press **Enter**.

2. Enter the username and password to log in to the instance.

3. Check whether the logon is successful.

   Returning the following similar information indicates a successful logon:

   ```Shell
   {
       "name": "es-coordinator-***kamn6-1",
       "cluster_name": "***kamn6",
       "cluster_uuid": "svy8esf**l128sjYtQ",
       "version": {
           "number": "7.10.2",
           "build_flavor": "default",
           "build_type": "tar",
           "build_hash": "747e1cc71def*****3c1f785afa92b9",
           "build_date": "2021-01-13T00:42:12.435326Z",
           "build_snapshot": false,
           "lucene_version": "8.7.0",
           "minimum_wire_compatibility_version": "6.8.0",
           "minimum_index_compatibility_version": "6.0.0-beta1"
       },
       "tagline": "You Know, for Search"
   }
   ```
   


<span id="12eda1d8"></span>
## Access the instance using the private network address


1. Connect to the ECS instance. For connection methods, refer to [Connect to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to access the instance.

   ```Shell
   # 默认开启用户登录认证，请注意输入用户名密码。
   curl -XGET  -u user:password http://elasticsearch-o-00c****vmn6.escloud.ivolces.com:9200
   
   # user：登录实例的访问用名。 
   # password：登录实例用户名的密码。
   # host：实例的私网访问地址，可在实例信息页面获取。
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance uses HTTPS protocol, add the <code>--insecure</code> parameter to the <code>curl</code> command to temporarily disable certificate verification for quick access.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Cloud Search service instance supports a global domain name, and the private network address enables cross\-region access. To use this feature, <a href="https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255">submit a ticket</a> to apply.   </div>
   

3. Check if accessing the instance is successful.

   Returning similar information below indicates normal instance access. The specific parameter values vary according to the instance version.

   ```Shell
   {
     "name" : "es-data-00***0o6-0",
     "cluster_name" : "00***0o6-0",
     "cluster_uuid" : "kCPx1u***avs-_XvkZA",
     "version" : {
       "number" : "7.10.2",
       "build_flavor" : "default",
       "build_type" : "tar",
       "build_hash" : "747e1cc71def0***a59143c1f785afa92b9",
       "build_date" : "2021-01-13T00:42:12.435326Z",
       "build_snapshot" : false,
       "lucene_version" : "8.7.0",
       "minimum_wire_compatibility_version" : "6.8.0",
       "minimum_index_compatibility_version" : "6.0.0-beta1"
     },
     "tagline" : "You Know, for Search"
   }
   ```
