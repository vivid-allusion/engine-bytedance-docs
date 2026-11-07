---
title: "Obtaining client IPs by using Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Getting-real-client-IP-addresses-through-Ingress"
---

This topic mainly describes how back\-end pods of a workload obtain the IP address of external requests when those requests access the workload by using Ingresses.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".Zmxhbm5lbC3nvZHnu5zpm4bnvqQ="></span>
## Flannel network cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. Set the external traffic forwarding policy `Spec.externalTrafficPolicy` of the service that corresponds to ingress\-nginx\-controller to `Local`.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The ingress\-nginx\-controller is the service that corresponds to the Ingress controller generated after the ingress\-nginx add\-on is installed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In clusters that use the Flannel network model, to enable back\-end pods to obtain client IP addresses, you need to set <code>externalTrafficPolicy</code> of the LoadBalancer service to <code>Local</code>. In this way, the IPVS of nodes can forward traffic only to the Nginx Ingress pods on the same nodes.   </div>
   

   1. Select **Services and Ingresses** \> **Service** in the left navigation bar.

   2. Find **ingress\-nginx\-controller** under the **kube\-system** namespace and in the **Actions** column, click `...` \> **Edit Yaml**.

   3. Change the value of `Spec.externalTrafficPolicy` to `Local`.

   4. Click **Confirm** to save the configuration.

4. Configure the ConfigMap that corresponds to ingress\-nginx\-controller, and add the required fields for obtaining the client IP address.

   1. In the left navigation bar of the cluster management page, click **Configurations** \> **ConfigMap**.

   2. Find **ingress\-nginx\-controller** under the **kube\-system** namespace and in the **Actions** column, click `...` \> **Edit Yaml**.

   3. Add the following fields in the `data` block of the ConfigMap.

      ```YAML
      data:
        use-forwarded-headers: "true"
        compute-full-forwarded-for: "true"
        forwarded-for-header: X-Forwarded-For
        ...
      ```
      

   4. Click **Confirm** to save the configurations.

5. After you complete the configuration, find ingress\-nginx\-controller in the **Deployment** list and redeploy it to make the new configurations take effect.


<span id=".dnBjLWNuaS3nvZHnu5zpm4bnvqQ="></span>
## VPC\-CNI network cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. Configure the ConfigMap that corresponds to ingress\-nginx\-controller, and add the required fields for obtaining the client IP address.

   1. In the left navigation bar of the cluster management page, click **Configurations** \> **ConfigMap**.

   2. Find **ingress\-nginx\-controller** under the **kube\-system** namespace and in the **Actions** column, click `...` \> **Edit Yaml**.

   3. Add the following fields in the `data` block of the ConfigMap.

      ```YAML
      data:
        use-forwarded-headers: "true"
        compute-full-forwarded-for: "true"
        forwarded-for-header: X-Forwarded-For
        ...
      ```
      

   4. Click **Confirm** to save the configurations.

4. After you complete the configuration, find ingress\-nginx\-controller in the **Deployment** list and redeploy it to make the new configurations take effect.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

In this topic, a client is simulated through an Nginx image. Therefore, before you verify the result, you also need to perform the following preparations:


* Install the ingress\-nginx add\-on on the cluster. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* Upload an open source Nginx image to CR to simulate the back\-end service when the operation results are being verified. For details, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* Prepare a host that can access the public network to simulate an external client. This client must be deployed outside the cluster where the Ingress is located.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can create an ECS instance that can access the public network as the execution machine. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances">Purchasing instances by using the wizard</a>.   </div>
   

<span id=".5q2l6aqk5LiA77ya6YOo572y5bqU55So5ZKM5pyN5Yqh"></span>
### Step 1: Deploy an application and service

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a cluster using the Flannel container network model, when the <code>externalTrafficPolicy</code> of a LoadBalancer Service is set to <code>Local</code>, the LoadBalancer IP becomes inaccessible if there are no Nginx Ingress Pods on the node. The IP address is mistakenly treated as an extended IP of the Service and is intercepted and forwarded by IPVS, leading to network connectivity failures. For more information about related issues, see <a href="https://github.com/kubernetes/kubernetes/issues/66607?spm=a2c4g.11186623.0.0.765e158bXIQRiB">Community documentation</a>.</div>


<div data-tips="true" data-tips-type="tip">Therefore, the following content uses a Deployment to simulate the Nginx Ingress pod of the back\-end service.</div>



1. Use an Nginx image to create a Deployment for simulating the back\-end service. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

2. Create a service of the LoadBalancer type and associate it with the Deployment created in Step 1.


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LWluZ3Jlc3M="></span>
### Step 2: Create an Ingress

Create an Ingress and associate it with the service of the LoadBalancer type created in Step 2. For detailed operations, see [Creating Nginx Ingresses in the console](https://docs.byteplus.com/en/docs/vke/Creating-an-Nginx-Ingress-in-the-console).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The namespace to which the Ingress belongs must be consistent with the namespace of the Deployment.</div>


<span id=".5q2l6aqk5LiJ77ya6K6_6Zeu6aqM6K-B"></span>
### Step 3: Verify access


1. Log in to the public network host.

2. Run the following command to access the domain name configured in the Ingress. `14.**.**.**` is the public IP address of the Ingress.

   ```Bash
   curl -H "Host: example.com" http://14.**.**.**
   ```
   

   The expected response result is as follows, in which the back\-end service can be accessed as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_996941ab3fcf157fd855f2c8ba4ce40f.png) </span>

3. Go to the details page of the back\-end Deployment (nginx) created in Step 1. Click the **Log** tab, and view the pod logs of the back\-end service. You can see that the X\-Forwarded\-For IP in the logs is the client IP address.
