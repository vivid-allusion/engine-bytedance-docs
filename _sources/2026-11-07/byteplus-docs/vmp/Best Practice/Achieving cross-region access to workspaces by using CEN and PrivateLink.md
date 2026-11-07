---
title: "Achieving cross-region access to workspaces by using CEN and PrivateLink"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Achieving_cross-region_access_to_workspaces_by_using_CEN_and_PrivateLink"
---

The workspace of Vital Managed Service for Prometheus (VMP) can be accessed over the Internet through PrivateLink. This topic describes how to configure PrivateLink to read and write data in a VMP workspace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use a  root user to configure and use this feature. If you use an Identity and Access Management (IAM) user to create an endpoint, you may not be able to select an available endpoint service. For more details, see <a href="https://docs.byteplus.com/en/docs/privatelink/FAQs">Why can't I select an available endpoint service when creating an endpoint?</a>  </div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A VMP workspace offers a standard remote write URL and a standard query URL that can be accessed over internal networks. This allows you to collect service metrics and business metrics in the internal networks of the public cloud and deploy Grafana in a Vital Kubernetes Engine (VKE) cluster to create and view metric dashboards. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

In some scenarios, you may need to establish connections between different regions of  to write or query data from the same Prometheus workspace in different regions. In this case, you can achieve cross\-region access to VMP workspaces by using [Cloud Enterprise Network (CEN)](https://docs.byteplus.com/en/docs/cen/Product-Overview-01) and [PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information about PrivateLink, refer to <a href="https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01">What is PrivateLink?</a></div>


* <div data-tips="true" data-tips-type="tip">For more information about CEN, refer to <a href="https://docs.byteplus.com/en/docs/cen/Product-Overview-01">What is Cloud Enterprise Network?</a></div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created, and basic authentication has been enabled. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A virtual private cloud (VPC) is created in each region.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic provides an example of how to configure the query URL of a VMP workspace by using PrivateLink. This configuration method applies to other addresses.</div>


<span id=".5q2l6aqk5LiA77ya6YWN572u5LqR5LyB5Lia572R"></span>
### Step 1: Configure CEN


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork). 

2. In the left navigation pane, click **CEN Instances**. On the page that appears, click **Create CEN** to create a CEN instance.

3. Click the name of the created CEN instance to go to the instance details page.

4. Click the **Network Instances** tab and click **Install Network Instances** to add two VPC instances in different regions.

&nbsp;

5. Click the **Inter\-region bandwidth** tab and click **Associate BWP** to create and bind a bandwidth package between two regions. Then, click **Allocate Inter\-region bandwidth** to allocate cross\-region bandwidth, thereby connecting networks across different regions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more detailed configuration and considerations of CEN, see <a href="https://docs.byteplus.com/en/docs/cen/Getting-Started-Overview">Considerations</a>.   </div>
   

<span id=".5q2l6aqk5LqM77ya6YWN572u57uI56uv6IqC54K5"></span>
### Step 2: Configure an endpoint

Create an endpoint in the region where the VMP workspace is located. This topic takes the China (Shanghai) region as an example. Procedure:


1. Log in to the [VPC console](https://console.byteplus.com/pl).  

2. In the left navigation pane, click **PrivateLink** \> **Endpoint**, and click the **Interface Endpoint** tab. Click **Create Endpoint**.

3. Specify the information about the endpoint.

   * **Basic information**: Select the region where the VMP workspace is deployed, specify the endpoint name, and select **Interface** for the Type parameter.

   * **Endpoint Service**: Select **BytePlus service** for the **Add method** parameter, and select the service that corresponds to VMP for the **Endpoint Service** parameter. You can select one of the following services:

      * VMP read\-only service: This service is used to query data of the VMP workspace.

      * VMP write\-only service: This service is used to write data in the VMP workspace.

   * **Network configuration**: Select the user VPC, availability zone, subnet, and security group.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more details about the configuration of the endpoint, see <a href="https://docs.byteplus.com/en/docs/privatelink/Endpoint-02">Creating interface endpoints</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Make sure that the security group allows traffic on port <code>8080</code>. Otherwise, the port may be inaccessible.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the read/write splitting scenarios, you need to separately create endpoints for reading and writing and use different domain names for the endpoints.      </div>
      

4. Click **Buy now** and check again to complete the configuration.


<span id=".5q2l6aqk5LiJ77ya56Gu6K6k57uI56uv6IqC54K56L-e5o6l54q25oCB"></span>
### Step 3: Check the endpoint connection status


1. After VMP automatically accepts the endpoint connection request, the network connection status of the endpoint changes to **Connected**, which indicates that the connection is successful. In this case, you can access VMP by using the **domain name of the endpoint**.

2. (Optional) In an Elastic Compute Service (ECS) instance or a pod in the VPC bound to the endpoint, run the following command to access the endpoint domain name and check whether the endpoint, domain name, and network are working as expected.

   ```bash
   curl http://ep-5g***.epsvc-22j124***.cn-shanghai.privatelink.volces.com:8080
   ```
   

   The following section shows the expected result: If a response is returned when you access the endpoint domain name, the connection is normal and the network is connected.

   ```bash
   Not Found
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b44eaebb3bb4e68e1b533d562b2f686.png) </span>


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

After the network is connected, you can access the VMP workspace across regions to read data from and write data to the workspace. The following section provides an example of how to deploy Grafana in a cluster in the China (Beijing) region to access the VMP workspace in the China (Shanghai) region.


1. Deploy Grafana in a VKE cluster in China (Beijing). For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

2. Run the following command to configure Grafana port forwarding:

   ```bash
   kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
   ```
   

3. Open a browser in your local environment (Linux/Mac), paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

4. Click **Connections \> Data sources** in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ded4dc33c39042fd34638b8d64e70621.png) </span>

5. Click **Add data source** to create a new data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e19addc9f3c41abf7ff61ed439c82eb0.png) </span>

6. On the **Add data source** page, click **Prometheus**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11943066b25290a5cced71f4e85d2006.png) </span>

7. In the HTTP section, paste the modified query URL of the workspace in the **Prometheus server URL** field.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to modify the original query URL of the workspace as follows:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Change the domain name to the domain name of the endpoint.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Add port <code>8080</code> next to the domain name.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The values of other parameters remain unchanged.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, change the query URL of the workspace to <code>http://ep-5gs***.epsvc-22j124***.cn-shanghai.privatelink.volces.com:8080/workspaces/b73***</code>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79a4331f2346af26bb69748b6b63ba77.png) </span>

8. Switch on **Basic auth** in the Auth section and configure the username and password used for workspace authentication in the **Basic Auth Details** section.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_71cdb7048685823d506df8dec399eddb.png) </span>

9. Click **Save & test** at the bottom of the page. When the message **Successfully queried the Prometheus API** is displayed, it indicates the data source is configured and the workspace is integrated with Grafana.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_694c3ab091976f68ac406eed6fc9b3b3.png) </span>

10. Click Explore in the left navigation pane of the Grafana platform. Then, you can query the data in the workspace as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8f54df4f8226bce832c00e1f6b90b00.png) </span>


<span id=".55uR5o6n6L-Q57u0"></span>
## Monitoring and O&M

After you achieve cross\-region access to the workspace by using CEN and PrivateLink, you can view the details and monitoring information of the CEN instance and the endpoint.


* [Viewing Monitoring Data](https://docs.byteplus.com/en/docs/cen/Monitoring-01)

* [View endpoint details](https://docs.byteplus.com/en/docs/privatelink/Viewing-endpoint-details)

* [Viewing Monitoring Data](https://docs.byteplus.com/en/docs/privatelink/Monitor-01)


For more configuration details, refer to the [official documentation of CEN](https://docs.byteplus.com/en/docs/cen/Product-Overview-01) and the [official documentation of PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01).
