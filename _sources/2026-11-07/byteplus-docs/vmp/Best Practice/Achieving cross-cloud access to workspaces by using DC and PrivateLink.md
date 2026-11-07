---
title: "Achieving cross-cloud access to workspaces by using DC and PrivateLink"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Achieving_cross-cloud_access_to_workspaces_by_using_DC_and_PrivateLink"
---

The workspace of Vital Managed Service for Prometheus (VMP) can be accessed over the Internet through PrivateLink. This topic describes how to configure PrivateLink to read and write data in a VMP workspace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use a  root user to configure and use this feature. If you use an Identity and Access Management (IAM) user to create an endpoint, you may not be able to select an available endpoint service. For more details, see <a href="https://docs.byteplus.com/en/docs/privatelink/FAQs">Why can't I select an available endpoint service when creating an endpoint?</a>  </div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A VMP workspace offers a standard remote write URL and a standard query URL that can be accessed over internal networks. This allows you to collect service metrics and business metrics in the internal networks of the public cloud and deploy Grafana in a Vital Kubernetes Engine (VKE) cluster to create and view metric dashboards. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

In some scenarios, you may need to query or write data in a VMP workspace in other public network environments such as other cloud providers and Internet data centers (IDCs). In this case, you can achieve cross\-cloud access to the VMP workspace by using [Direct Connect (DC)](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect) and [PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about PrivateLink, see <a href="https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01">What is PrivateLink?</a></div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created, and basic authentication has been enabled. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* The network between other environments and the  cloud is connected through DC. For more details, refer to [What is Direct Connect](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic provides an example of how to configure the query URL of a VMP workspace by using PrivateLink. This configuration method applies to other addresses.</div>


<span id=".5q2l6aqk5LiA77ya6YWN572u57uI56uv6IqC54K5"></span>
### Step 1: Configure an endpoint


1. Log in to the [VPC console](https://console.byteplus.com/pl).  

2. In the left navigation bar, click **PrivateLink** \> **Endpoint**, and click the **Interface Endpoint** tab. Click **Create Endpoint**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_20548c3715c8d1325bb8a26da15d7247.png) </span>

3. Specify the information about the endpoint.

   * **Basic information**: Select the region where the VMP workspace is deployed, specify the endpoint name, and select **Interface** for the Type parameter.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1bc77b76a5670da710339d9cd5a1a0b5.png) </span>

   * **Endpoint Service**: Select **BytePlus service** for the **Add method** parameter, and select the service that corresponds to VMP for the **Endpoint Service** parameter.  

      * VMP read\-only service: used to query data of the VMP workspace.

      * VMP write\-only service: used to write data in the VMP workspace.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1e3cb9ace76b8a5dbc7d6069d6924271.png) </span>

   * **Network configuration**: Select the user VPC, availability zone, subnet, and security group.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4254e06dfb1ea15b24eb870b8eaba470.png) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more details about the configuration of the endpoint, see <a href="https://docs.byteplus.com/en/docs/privatelink/Endpoint-02">Creating interface endpoints</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Make sure that the security group allows traffic on port <code>8080</code>. Otherwise, the port may be inaccessible.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the read/write splitting scenarios, you need to separately create endpoints for reading and writing and use different domain names for the endpoints.      </div>
      

4. Click **Buy now** to complete the configuration.


<span id=".5q2l6aqk5LqM77ya56Gu6K6k57uI56uv6IqC54K56L-e5o6l54q25oCB"></span>
### Step 2: Check the endpoint connection status


1. After VMP automatically accepts the endpoint connection request, the network connection status of the endpoint changes to **Connected**, which indicates that the connection is successful. In this case, you can access VMP by using the **domain name of the endpoint**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d8eb7556f98f3074f8df4246a79f057.png) </span>

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

<span id=".5q2l6aqk5LiA77ya6YWN572u6YeH6ZuG5ZmoIFJlbW90ZVdyaXRlIOWcsOWdgA=="></span>
### Step 1: Configure the remote write URL of the collector

After the network is connected, modify the remote write URL of the collector in the same VPC as the endpoint. This allows you to store the metrics collected by the collector in the VPC in the VMP workspace.

This topic takes the [VM Agent collector](https://docs.byteplus.com/en/docs/vmp/Collection-solution-overview) as an example. You need to change the value of the `remoteWrite.url` field in the configuration file of the collector to the modified remote write URL of the workspace.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to modify the remote write URL of the workspace as follows:</div>



1. <div data-tips="true" data-tips-type="tip">Change the domain name to the domain name of the endpoint.</div>


2. <div data-tips="true" data-tips-type="tip">Add port <code>8080</code> next to the domain name.</div>


3. <div data-tips="true" data-tips-type="tip">The values of other parameters remain unchanged.</div>



<div data-tips="true" data-tips-type="tip">For example, change the remote write URL of the workspace to <code>http://ep-5gs***.epsvc-22j124***.cn-shanghai.privatelink.volces.com:8080/workspaces/b73***/api/v1/write</code>.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_daadcb69ba43dd80e09559a762297ff4.png) </span>

<span id=".5q2l6aqk5LqM77ya6YWN572uIEdyYWZhbmEg5o6l5YWl5bel5L2c5Yy6"></span>
### Step 2: Integrate Grafana with the workspace


1. Log in to Grafana in another environment.

2. Click **Connections \> Data sources** in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ded4dc33c39042fd34638b8d64e70621.png) </span>

3. Click **Add data source** to create a new data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e19addc9f3c41abf7ff61ed439c82eb0.png) </span>

4. On the **Add data source** page, click **Prometheus**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11943066b25290a5cced71f4e85d2006.png) </span>

5. In the HTTP section, paste the modified query URL of the workspace in the **Prometheus server URL** field.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to modify the original query URL of the workspace as follows:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Change the domain name to the domain name of the endpoint.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Add port <code>8080</code> next to the domain name.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The values of other parameters remain unchanged.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, change the query URL of the workspace to <code>http://ep-5gs***.epsvc-22j124***.cn-shanghai.privatelink.volces.com:8080/workspaces/b73***</code>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79a4331f2346af26bb69748b6b63ba77.png) </span>

6. Switch on **Basic auth** in the Auth section and configure the username and password used for workspace authentication in the **Basic Auth Details** section.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_71cdb7048685823d506df8dec399eddb.png) </span>

7. Click **Save & test** at the bottom of the page. When the message **Successfully queried the Prometheus API** is displayed, it indicates the data source is configured and the workspace is integrated with Grafana.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_694c3ab091976f68ac406eed6fc9b3b3.png) </span>


<span id=".55uR5o6n6L-Q57u0"></span>
## Monitoring and O&M

After you achieve cross\-cloud access through PrivateLink, you can view the details and monitoring information of the endpoint.


* [Viewing endpoint details](https://docs.byteplus.com/en/docs/privatelink/Viewing-endpoint-details)

* [Viewing Monitoring Data](https://docs.byteplus.com/en/docs/privatelink/Monitor-01)


For more configuration details, refer to the [official documentation of PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01).
