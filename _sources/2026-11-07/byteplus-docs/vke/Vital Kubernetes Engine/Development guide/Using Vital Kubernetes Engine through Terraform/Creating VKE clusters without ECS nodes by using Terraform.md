---
title: "Creating VKE clusters without ECS nodes by using Terraform"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Terraform-to-create-a-VKE-cluster-without-ECS-nodes"
---

This topic describes how to use Terraform to create a VKE cluster that does not contain ECS nodes.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Before using Terraform to create a cluster without ECS nodes, follow the steps to install Terraform.


1. Download and install the desired version from the official Terraform website. For details, see the [Terraform documentation](https://www.terraform.io/downloads).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the Terraform version is not earlier than v0.13. You can run the <code>terraform version</code> command to query the version.   </div>
   

2. Provide Byteplus root user information in Terraform.

   1. Create environment variables to store authentication credentials.

      ```bash
      export BYTEPLUS_ACCESS_KEY="AK************"
      export BYTEPLUS_SECRET_KEY="************"
      export BYTEPLUS_REGION="ap-southeast-1"
      ```
      

      The following table describes the parameters.

      
      |Parameter |Description |
      |---|---|
      |BYTEPLUS_ACCESS_KEY |The AccessKey ID (AK) of your BytePlus account. For more information on how to obtain the key, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |BYTEPLUS_SECRET_KEY |The AccessKey secret (SK) of your BytePlus account. For more information on how to obtain the key, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |BYTEPLUS_REGION |The Region where your VKE application is located. For more information on Region and RegionID supported by VKE, refer to [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |
      

   2. Specify the provider section of the configuration file to provide authentication information.

      ```bash
      provider "byteplus" {
        access_key = "AK************"
        secret_key = "************"
        session_token = "sts token"
        region = "ap-southeast-1"
      }
      ```
      

      The following table describes the parameters.

      
      |Parameter |Description |
      |---|---|
      |access_key |The AccessKey ID (AK) of your BytePlus account. For more information on how to obtain the key, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |secret_key |The AccessKey secret (SK) of your BytePlus account. For more information on how to obtain the key, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
      |session_token |Optional. The role\-playing security token. Call the [AssumeRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole) API to obtain the token. |
      |region |The Region where your VKE application is located. Keep the parameter value the same as that of **BYTEPLUS_REGION** in the previous step. |
      


<span id=".5Yib5bu65pegLWVjcy3oioLngrnnmoTpm4bnvqQ="></span>
## Creating a cluster without ECS nodes


1. Create a folder and place a configuration file named `main.tf` in it.

   ```bash
   terraform {
     required_providers {
       byteplus = {
         source = "byteplus-sdk/byteplus"
         version = "0.0.12" # Get the version information from the official website of Terraform (https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest).
       }
     }
   }
   
   provider "byteplus" {
     access_key = "**********" # The AccessKey ID of the BytePlus account.
     secret_key = "**********" # The AccessKey secret of the BytePlus account.
     region = "ap-southeast-1" # The Region where the VKE application is located.
   }
   
   #Create a Virtual Private Cloud (VPC)
   resource "byteplus_vpc" "vke-tf-vpc" {
     vpc_name    = "vke-tf-vpc" # The name of the VPC.
     cidr_block  = "172.16.0.0/16" # The Classless Inter-Domain Routing (CIDR) block of the VPC.
   }
   
   #Create a Virtual Switch (VSW)
   resource "byteplus_subnet" "vke-tf-vsw" {
     subnet_name = "vke-tf-vsw-1" # The subnet name of the VSW.
     cidr_block  = "172.16.0.0/24" # The CIDR block of the VSW.
     zone_id     = "ap-southeast-1a" # The Availability Zone of the VSW.
     vpc_id      = byteplus_vpc.vke-tf-vpc.id # The ID of the VPC to which the VSW belongs.
   }
   
   #Create a VKE cluster
   resource "byteplus_vke_cluster" "vke-tf-test" {
     name                = "tf-created-vke-serverless" # The name of the cluster.
     kubernetes_version  = "1.26" # The Kubernetes version of the cluster. The version number only supports the x.y format rather than x.y.z.
     # For more information on Kubernetes versions that VKE supports, refer to https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes.
     description         = "vke-serverless created by tf" # The description of the cluster.
     delete_protection_enabled = true # Whether to enable Delete Protection. true: enable; false: disable.
     cluster_config {
       subnet_ids = [byteplus_subnet.vke-tf-vsw.id] # The subnet ID of the cluster.
       api_server_public_access_enabled = true # Whether to enable Public access to API Server. true: enable; false: disable.
       #Configure the Elastic IP Address (EIP) billing method and bandwidth for the API Server
       api_server_public_access_config {
         public_access_network_config {
           billing_type    = "PostPaidByTraffic" # The EIP billing method. PostPaidByTraffic: the pay-as-you-go billing method based on the actual traffic; PostPaidByBandwidth: the pay-as-you-go billing method based on the maximum bandwidth.
           bandwidth       = 10 # The maximum EIP bandwidth. The range of valid values for PostPaidByTraffic is 1 to 200. The range of valid values for PostPaidByBandwidth is 1 to 500.
         }
       }
       resource_public_access_default_enabled = true # Whether to enable internet-facing access. true: enable; false: disable.
     }
     pods_config {
       pod_network_mode = "VpcCniShared"  # The container network mode. VpcCniShared: the VPC-CNI network model; Flannel: the Flannel network model.
       #When the network model is Flannel, flannel_config takes effect.
       flannel_config {
         pod_cidrs = ["192.168.0.0/20"]  # The Pod CIDR of the Flannel container network.
         max_pods_per_node = 64  # The maximum number of single-node pod instances in the Flannel container network. Valid values: 64, 16, 32, 128, and 256.
       }
       #When the network model is VpcCniShared, vpc_cni_config takes effect.
       vpc_cni_config {
         subnet_ids = [byteplus_subnet.vke-tf-vsw.id]  # The pod subnet ID of the VPC-CNI container network.
       }
     }
     #Configure a CIDR for Services in the cluster
     services_config {
       service_cidrsv4 = ["192.168.16.0/24"]  # The CIDR that Services in the cluster use.
     }
   }
   
   resource "byteplus_vke_addon" "fo1" {
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install vci-virtual-kubelet. This add-on is a must-install.
     name = "vci-virtual-kubelet"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo2" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install core-dns. This add-on is a must-install.
     name = "core-dns"
     deploy_node_type = "VirtualNode"
   
   }
   
   resource "byteplus_vke_addon" "fo3" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install metrics-server. This add-on is a must-install.
     name = "metrics-server"
     deploy_node_type = "VirtualNode"
   
   }
   
   resource "byteplus_vke_addon" "fo4" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install csi-ebs.
     name = "csi-ebs"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo5" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install csi-nas.
     name = "csi-nas"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo6" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install snapshot-controller.
     name = "snapshot-controller"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo7" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install apig-controller.
     name = "apig-controller"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo8" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install application-inspector.
     name = "application-inspector"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo9" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install application-inspector.
     name = "application-inspector"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo10" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install cronhpa.
     name = "cronhpa"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo11" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install image-accelerator.
     name = "image-accelerator"
     deploy_node_type = "VirtualNode"
   }
   
   resource "byteplus_vke_addon" "fo12" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install prometheus-agent.
     name = "prometheus-agent"
     deploy_node_type = "VirtualNode"
     config = "{\"NodeExporterDisabled\":false,\"AutoScalingEnabled\":false,\"VmAgent\":{\"InitShards\":1,\"Requests\":{\"Cpu\":\"2\",\"Memory\":\"2Gi\"},\"Limits\":{\"Cpu\":\"4\",\"Memory\":\"4Gi\"}},\"KubeStateMetrics\":{\"InitShards\":1,\"Requests\":{\"Cpu\":\"0.2\",\"Memory\":\"512Mi\"},\"Limits\":{\"Cpu\":\"0.8\",\"Memory\":\"2Gi\"}}}"
   }
   
   resource "byteplus_vke_addon" "fo13" {
     depends_on = [byteplus_vke_addon.fo1]
     cluster_id = byteplus_vke_cluster.vke-tf-test.id
     # Install cr-credential-controller.
     name = "cr-credential-controller"
     deploy_node_type = "VirtualNode"
     deploy_mode = "Unmanaged"
     config = "{\"CrConfigmapData\":{\"Namespace\":\"*\",\"ServiceAccount\":\"*\",\"Registries\":[{\"Instance\":\"helm-cr\",\"Region\":\"ap-southeast-1\"}]}}"
   }
   
   resource "byteplus_vke_addon" "fo14" {
     depends_on       = [byteplus_vke_addon.fo1]
     cluster_id       = byteplus_vke_cluster.vke-tf-test.id
     # Install event-collector.
     name             = "event-collector"
     deploy_node_type = "VirtualNode"
     config           = "{\"TopicId\":\"f48b51d8-a6f7-4c26-b2ae-c1de96******\",\"ProjectId\":\"145749e8-b46d-424e-8c8a-a7d401******\",\"AccessKeyId\":\"AKLTNzc4MG******MWFiNDNlZGFmNTg5YT******\",\"AccessKeySecret\":\"WVRGaVlUT******EwWXpNd05ESmlaRGxpWkRCa******elpqUQ==\"}"
     deploy_mode      = "Unmanaged"
   }
   
   resource "byteplus_vke_addon" "fo15" {
     depends_on       = [byteplus_vke_addon.fo1]
     cluster_id       = byteplus_vke_cluster.vke-tf-test.id
     # Install ingress-nginx.
     name             = "ingress-nginx"
     deploy_node_type = "VirtualNode"
     config =  "{\"Replicas\":2,\"Resources\":{\"Requests\":{\"Cpu\":\"0.1\",\"Memory\":\"250Mi\"},\"Limits\":{\"Cpu\":\"0.5\",\"Memory\":\"1024Mi\"}},\"PrivateNetwork\":{\"SubnetId\":\"subnet-rrfr1oopsg00v0x57******\",\"IpFamily\":\"ipv4\"}}"
     deploy_mode      = "Unmanaged"
   }
   
   resource "byteplus_vke_addon" "fo16" {
     depends_on       = [byteplus_vke_addon.fo1]
     cluster_id       = byteplus_vke_cluster.vke-tf-test.id
     # Install load-balancer-controller.
     name             = "load-balancer-controller"
     deploy_node_type = "VirtualNode"
     config = "{\"IsSharedMode\":false,\"Resources\":{\"Requests\":{\"Cpu\":\"0.25\",\"Memory\":\"128Mi\"},\"Limits\":{\"Cpu\":\"1\",\"Memory\":\"512Mi\"}},\"PlbConfig\":{\"Enabled\":true,\"AccessKeyId\":\"AKLTNzc4MG******MWFiNDNlZGFmNTg5YT******\",\"AccessKeySecret\":\"WVRGaVlUT******EwWXpNd05ESmlaRGxpWkRCa******elpqUQ==\",\"ServiceId\":\"syssrv-111\"},\"ClbConfig\":{\"Enabled\":false}}"
     deploy_mode      = "Unmanaged"
   }
   
   resource "byteplus_vke_addon" "fo17" {
     depends_on       = [byteplus_vke_addon.fo1, byteplus_vke_addon.fo5]
     cluster_id       = byteplus_vke_cluster.vke-tf-test.id
     # Install p2p-accelerator. Ensure that P2P acceleration is enabled for the associated Container Registry instance.
     name             = "p2p-accelerator"
     deploy_node_type = "VirtualNode"
     config =       "{\"Region\":\"ap-southeast-1\",\"VpcId\":\"vpc-min4y8zya8sg5smt1a******\",\"Registry\":\"helm-cr\",\"NydusEnabled\":false,\"DaemonProxyReplicas\":3,\"AccessKeyId\":\"AKLTNzc4MG******MWFiNDNlZGFmNTg5YT******\",\"AccessKeySecret\":\"WVRGaVlUT******EwWXpNd05ESmlaRGxpWkRCa******elpqUQ==\",\"DeployNodeType\":\"VirtualNode\"}"
     deploy_mode      = "Unmanaged"
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Except the <strong>required</strong> add\-ons indicated by the comments, other add\-ons can be installed as needed. For details of add\-on parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on">Installing an add\-on</a> and <a href="https://docs.byteplus.com/en/docs/vke/CreateAddon">CreateAddon</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If an add\-on fails to be installed or is abnormal, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to obtain technical support.   </div>
   

2. Initialize the Terraform environment.

   ```bash
   terraform init
   ```
   

3. Perform resource planning.

   ```bash
   terraform plan
   ```
   

4. Creates a cluster.

   ```bash
   terraform apply
   ```
