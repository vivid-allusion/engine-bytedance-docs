---
title: "Creating cloud sandbox instances using custom images"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_cloud_sandbox_instances_using_custom_images"
---

Cloud sandbox supports using images from your self\-built private image repositories outside BytePlus (such as Harbor, Nexus, and Generic Registry V2) directly as custom images for sandbox instances. This enables you to set up sandbox environments quickly without migrating images.

## Application scenarios

To meet security and compliance requirements, the image repositories deployed in your local data center or self\-owned server room are only accessible on the private network. The system cannot pull images via the public network. Through the custom CR capability, veFaaS can use your pre\-established dedicated line to warm up images from intranet image repositories to sandbox nodes and complete format conversion. This provides an instant cache hit when creating an instance, enabling startup in seconds and saving the time spent pulling large images remotely from the origin for each instance creation.

This topic describes the complete process for configuring a private CR and creating a sandbox instance. It uses an example in which images are pulled from a Harbor CR over a dedicated line and pre\-cached as custom sandbox images.

## Prerequisites

* **Network connectivity (private network access required)**

   * A dedicated line from the cloud private network to the local data center has been established. For details, see [Connecting an on-premises IDC to the cloud](https://docs.byteplus.com/en/docs/6407/1791170?lang=en).

   * Your self\-built image repository can be accessed via one or more private IPv4 addresses within your VPC.

   * (Optional) To access the CR by domain name, prepare a DNS resolver in the VPC. Make sure that the resolver can resolve the domain name and record its IP address. For details, see [Checking TrafficRoute resolution records](https://docs.byteplus.com/en/docs/cr/Viewing_TrafficRoute_resolution_records?lang=en#VPC).

   * (Optional) If you are working as an IAM user, you need to add the VeFaaSFullAccess system preset policy in advance. For details, see [Using global preset policies and authorizing](https://docs.byteplus.com/en/docs/6662/1355665?lang=en#.5Zy65pmv5LiA77ya5L2_55So5YWo5bGA6IyD5Zu055qE6aKE6K6-562W55Wl5bm25o6I5p2D).

* **Third\-party registry**

   The access credentials for the third\-party registry (Harbor in this example) have been obtained.

   * BasicAuth type: Obtain the username and password in advance for accessing the third\-party registry.

   * BearerToken type: Obtain the token in advance for accessing the third\-party registry.

## Procedure

To create a cloud sandbox application using a custom image, you need to complete six steps in sequence, from creating a CR to finally creating a sandbox instance. The following figure shows the complete procedure. Detailed descriptions of each step are as follows.

## ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed6db213fda94ab3b3eef0882ce3b3b9.png)

## Procedure

### Step 1: Create a custom CR

Call [CreateCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600006) to create a custom CR.

* Sample requests

   ```JSON
   {
     "Name": "harbor",
     "Server": "registry-cn-shanghai.harbor.com",
     "Namespace": "****",
     "AuthConfig": {
       "AuthType": "BasicAuth",
       "Username": "admin",
       "Password": "****"
     },
     "NetworkConfig": {
       "AccessType": "PrivateVpc",
       "VpcId": "vpc-****",
       "SubnetId": "subnet-****",
       "ServerIps": ["192.168.***.***"],
       "UserSecurityGroupIds": ["sg-****"],
       "DnsServerIps": ["10.0.***.***"]
     }
   }
   ```

   > **tip**

   > For detailed network configuration instructions, see [CustomImageRegistryNetworkConfig](https://docs.byteplus.com/en/docs/6662/2600006?lang=en#customimageregistrynetworkconfig).

   |**Field** |**Required** |**Description** |
   |---|---|---|
   |AuthConfig |No |Authentication type for the custom CR. It specifies the authentication method for the registry. Available values are as follows.<br><br><br>* BasicAuth: Username and password authentication.<br><br>* BearerToken: Token authentication.<br><br>* Anonymous: Anonymous access, no authentication required. |
   |VpcId |Yes |The ID of the private network where the custom CR resides. |
   |SubnetId |Yes |The subnet ID where the custom CR resides. |
   |ServerIps |Yes |The list of private IPv4 addresses of the custom CR within the VPC. |
   |UserSecurityGroupIds |Yes |The list of security group IDs used in the private network. |
   |DnsServerIps |No |The IP address of the DNS resolver within the private network. Fill this in only when accessing via the custom CR's domain name. |

* Sample responses

   After a successful call, the ID of the custom CR (RegistryId, in this example `regcfg-8xkq****`) is returned, and PrivateAccess.Status is `pending`, indicating the call was successful.

   ```JSON
   {
     "ResponseMetadata": {
       "RequestId": "20260709190000****",
       "Action": "CreateCustomImageRegistry",
       "Version": "2024-01-01",
       "Service": "vefaas",
       "Region": "cn-shanghai"
     },
     "Result": {
       "RegistryId": "regcfg-8xkq****",
       "Name": "harbor",
       "Server": "registry-cn-shanghai.harbor.com",
       "Namespace": "****",
       "AuthStatus": { 
          "AuthType": "BasicAuth",
          "Configured": true 
       },
       "NetworkConfig": {
         "AccessType": "PrivateVpc",
         "VpcId": "vpc-****",
         "SubnetId": "subnet-****",
         "ServerIps": ["192.168.***.***"],
         "UserSecurityGroupIds": ["sg-****"],
         "DnsServerIps": ["10.0.***.***"]
       },
       "PrivateAccess": {
         "Status": "pending",
         "Message": "",
         "EndpointIp": "",
         "LastCheckTime": ""
       }
     }
   }
   ```

### Step 2: Poll the private network access status

Use the CR ID returned from [Step 1](https://docs.byteplus.com/en/docs/6662/2599221?lang=en#xYVRWS8Q) (in this example `regcfg-8xkq****`) to call [GetCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600007?lang=en) until the private network access status PrivateAccess.Status becomes `ready`.

* Sample requests

   ```JSON
   {
       "RegistryId": "regcfg-8xkq****"
   }
   ```

* Sample responses

   ```JSON
   {
     "ResponseMetadata": {
       "RequestId": "20250829114726002227007142CD44EA",
       "Action": "GetCustomImageRegistry",
       "Version": "2024-06-06",
       "Service": "vefaas",
       "Region": "cn-shanghai"
     },
     "Result": {
       "Id": "regcfg-****",
       "Name": "harbor",
       "Server": "registry-cn-shanghai.harbor.com",
       "Namespace": "****",
       "AuthConfig": {
         "AuthType": "BasicAuth",
         "Configured": true
       },
       "NetworkConfig": {
         "AccessType": "PrivateVpc",
         "VpcId": "vpc-****",
         "SubnetId": "subnet-****",
         "ServerIps": ["172.16.***.***"],
         "UserSecurityGroupIds": ["sg-****"],
         "DnsServerIps": ["192.168.***.***"]
       },
       "PrivateAccess": {
         "Status": "ready",
         "Message": "Private network access is ready",
         "EndpointIp": "192.168.***.***",
         "LastCheckTime": "2025-04-25 11:11:29.376 +0000 UTC"
       }
     }
   }
   ```

   > **tip**

   > If it remains in the `enabling` or `failed` state for a long time, first verify the following configurations, and after correcting them, use [UpdateCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600009?lang=en) to trigger orchestration again.

   * > Whether VpcId, SubnetId, and security group belong to the same VPC.

   * > Whether the subnet has unused IPs.

### Step 3: Connect the custom CR and veFaaS

[Submit a ticket](https://console.byteplus.com/workorder/create?step=1) and provide the CR's private IP (ServerIps specified in [Step 1](https://docs.byteplus.com/en/docs/6662/2599221?lang=en#xYVRWS8Q)) to allow veFaaS to access the custom CR.

### Step 4: Submit image warm\-up

Call [PrecacheSandboxImages](https://docs.byteplus.com/en/docs/faas/PrecacheSandboxImages?lang=en) to submit an image warm\-up task.

* Sample requests

   ```JSON
   { 
       "ImageUrls": [ 
           "registry-cn-shanghai.harbor.com/****/native-****:v1" 
       ], 
       "RegistryId": "regcfg-8xkq****" 
   }
   ```

   |**Field** |**Required** |**Description** |
   |---|---|---|
   |ImageUrls |Yes |Fill in the complete address of the image to be warmed up, which is composed of the domain name, namespace, image name, and version of the target image registry. The format is `{Container Registry domain}/{namespace}/{image name}:{version}`. In this example, it is `registry-cn-shanghai.harbor.com/****/native-****:v1`. |
   |RegistryId |No |Fill in the image registry ID returned in [Step 1](https://docs.byteplus.com/en/docs/6662/2599221?lang=en#xYVRWS8Q). In this example, it is `regcfg-8xkq****`. |

* Sample responses

   The warm\-up is an asynchronous task. The API returns a query credential (TicketId), indicating that the warm\-up task was submitted successfully.

   ```JSON
   {
       "ResponseMetadata": {
           "RequestId": "20230604110420****100232280022D31",
           "Action": "PrecacheSandboxImages",
           "Version": "2024-06-06",
           "Service": "vefaas",
           "Region": "cn-shanghai"
       },
       "Result": {
           "TicketId": "948410ee80954******"
       }
   }
   ```

### Step 5: Query the warm\-up result

After the warm\-up task is submitted, poll [ListSandboxImages](https://docs.byteplus.com/en/docs/faas/ListSandboxImages?lang=en). When PrecacheStatus returns `success` ** ** , warm\-up is complete.

* Sample requests

   ```JSON
   { 
       "ImageType": "private", 
       "Filters": [ 
           { 
               "Key": "source_image_url", 
               "Values": [ 
                   "registry-cn-shanghai.harbor.com/****/native-****:v1" 
               ] 
           } 
       ], 
       "PageNumber": 1, 
       "PageSize": 10 
   }
   ```

   |**Field** |**Required** |**Description** |
   |---|---|---|
   |Filters.Key |No |Filter criterion Key. In this example, fill in `source_image_url` ** ** , i.e., filter by image address. |
   |Filters.Values |No |Fill in the ImageUrls from [Step 4](https://docs.byteplus.com/en/docs/6662/2599221?lang=en#LTWvGatW), which are the complete addresses of the images to be warmed up. In this example, it is `registry-cn-shanghai.harbor.com/****/native-****:v1`. |

* Sample responses

   When PrecacheStatus returns `success` ** ** , warm\-up is successful. The response also provides the warmed\-up image ID (ImageId), which is `9px3r6****` in this example.

   ```JSON
   { 
       "ResponseMetadata": { 
           "RequestId": "20230604110420****100232280022D31", 
           "Action": "ListSandboxImages", 
           "Version": "2024-06-06", 
           "Service": "vefaas", 
           "Region": "cn-shanghai" 
       }, 
       "Result": { 
           "Images": [ 
               { 
                   "ImageId": "9px3r6****", 
                   "ImageUrl": "registry-cn-shanghai.harbor.com/****/native-****:v1", 
                   "ImageGroup": "Code", 
                   "UpdateTime": "2025-04-25 11:11:29.376 +0000 UTC", 
                   "PrecacheStatus": "success", 
                   "PrecacheStatusReason": "", 
                   "RelatedSandboxApplications": [ 
                       "wxd2****" 
                   ] 
               } 
           ], 
           "TotalCount": 1 
       } 
   }
   ```

### Step 6: Create a sandbox instance

Call [CreateSandbox](https://docs.byteplus.com/en/docs/faas/CreateSandbox?lang=en) to create a sandbox instance. The returned SandboxId indicates successful creation.

* Sample requests

   ```JSON
   { 
       "FunctionId": "wrws****", 
       "Timeout": 60, 
       "Metadata": { 
           "app": "test" 
       }, 
       "InstanceTosMountConfig": { 
           "Enable": true, 
           "TosMountPoints": [ 
               { 
                   "BucketPath": "/sandbox", 
                   "LocalMountPath": "/mnt/tos" 
               } 
           ] 
       }, 
       "Envs": [ 
           { 
               "Key": "business_type", 
               "Value": "free" 
           } 
       ], 
       "InstanceImageInfo": { 
           "Id": "9px3r6****", 
           "Port": 8080, 
           "Image": "registry-cn-shanghai.harbor.com/****/native-****:v1", 
           "Command": "bash /root/sandbox/scripts/run.sh" 
       }, 
       "CpuMilli": 500, 
       "MemoryMB": 1024, 
       "MaxConcurrency": 20, 
       "RequestTimeout": 30 
   }
   ```

   |**Field** |**Required** |**Description** |
   |---|---|---|
   |InstanceImageInfo.Id |No |Fill in the ID of the sandbox image, which is the ImageId returned by [ListSandboxImages](https://docs.byteplus.com/en/docs/faas/ListSandboxImages?lang=en) in the previous step. In this example `9px3r6****`. |
   |InstanceImageInfo.Image |No |Fill in the complete address of the warmed\-up image, which is the ImageUrl returned by [ListSandboxImages](https://docs.byteplus.com/en/docs/faas/ListSandboxImages?lang=en) in the previous step. In this example, it is `registry-cn-shanghai.harbor.com/****/native-****:v1`. |

* Sample responses

   ```JSON
   { 
       "ResponseMetadata": { 
           "RequestId": "20230604110420****100232280022D31", 
           "Action": "CreateSandbox", 
           "Version": "2024-06-06", 
           "Service": "vefaas", 
           "Region": "cn-shanghai" 
       }, 
       "Result": { 
           "SandboxId": "vefaas-e8m6xarn-p2zamuv2fr-******" 
       } 
   }
   ```

##
