---
title: "Subscribe to events"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/subscribe-to-events"
---

To integrate SealSuite audit logs and security events with your internal platforms like SIEM, data lakes, or custom applications, you can create an event subscription. This guide provides step\-by\-step instructions for configuring event subscriptions via Webhook, Kafka, and Syslog, and explains how to manage them in the admin console.

<span id="dd1149a1"></span>
## **Subscription Type Overview**

SealSuite supports the following three event subscription types to meet different technical and business requirements:


|Subscription Type |How It Works |Use Case |
|---|---|---|
|**Webhook** |**HTTP Push**<br><br>When an event occurs, SealSuite proactively sends an HTTP `POST` request containing the event data to a URL you specify. |Simple and fast integration. Suitable for low\-volume event scenarios or for integrating with SaaS services and lightweight custom applications that support webhooks. |
|**Kafka** |**Publish\-Subscribe Model**<br><br>SealSuite acts as a Producer, publishing events to a Kafka Topic you specify. Your internal backend services then act as Consumers to subscribe to and pull messages from that Topic. |High\-throughput, high\-concurrency event processing. Suitable for ingesting a full stream of event logs into internal SIEM platforms, data lakes, or real\-time computing systems. |
|**Syslog** |**Syslog protocol push**<br><br>When an event occurs, SealSuite pushes the event data to your designated log server using the Syslog protocol. |Standardized log integration. Ideal for forwarding events to an enterprise SOC or security auditing platform. |


<span id="73abedba"></span>
## **Adding an Event Subscription**


1. Log in to the admin console.

2. In the left navigation bar, select **Settings** \> **Integration** \> **Event Hub**.

3. On the Event Hub page, click **Add Event Subscription** in the upper\-right corner.

4. Choose your desired subscription method and click **Confirm**.


<span id="6d26e0fe"></span>
### **Configuring a Webhook Subscription**

After selecting the **Webhook** type, complete the following settings on the configuration page:

<span id="89d526a1"></span>
#### **1. General**


* **Name**: (Required) A custom name to identify this event subscription.

* **Description**: (Optional) A custom description of the subscription's purpose.


<span id="b2ca29ea"></span>
#### **2. Webhook Configuration**

When a subscribed event occurs, SealSuite sends an HTTP `POST` request containing the event data to your specified Request URL.

Before configuring a webhook, you must prepare a server to receive the event data and ensure it meets the following conditions:


* **Network Accessibility**: Your server's URL must be accessible from the SealSuite admin console. For example, if your SealSuite instance is public, the server must also have a public IP and an accessible port.

* **Processing Capability**: Your server must be able to receive and process HTTP `POST` requests and parse JSON\-formatted data.

* **Request URL**

   * **Description**: The URL of your receiving server. It must begin with `http://` or `https://`.

   * **URL Validation**: When you save the configuration, SealSuite will immediately send a one\-time validation request to this URL to confirm its validity. Your server must respond correctly to this request, or the configuration will fail to save. The validation process is as follows:

      1. SealSuite sends a `POST` request with a JSON object in the body.

      2. The JSON object contains a field named `challenge`.

      3. Your server must parse the value of the `challenge` field and return it directly as the response body within **1 second**.

         **Validation Request Example:** 

      ```JSON
      {
        "challenge": "abc1234-xxxx-xxxx-xxxx-abc1234567",
        "token": "tokendemo",
        "type": "url_verification"
      }
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If an Encrypt Key is configured in the <strong>Encryption Policy</strong> below, this validation request will also be encrypted. Your server must first decrypt the request before performing the challenge\-response validation.      </div>
      

* **Subscribe to Events**


Select one or more event types you wish to subscribe to from the list.

<span id="b6b3e240"></span>
#### **3. Encryption Policy**

You can configure an encryption policy to encrypt event data in transit, ensuring that sensitive corporate information is not exposed and that the request originates from the SealSuite system.


* **Verification Token**: (Required) A token used to verify that requests originate from SealSuite. This value will be included in the event data pushed by SealSuite. You can define a custom value or click the **Reset** icon to generate one automatically.

* **Encrypt Key**: (Optional but Recommended) When configured, SealSuite will encrypt the event data pushed to the Request URL. It is recommended to configure this parameter to enhance data security. You can define a custom value or click the **Reset** icon to generate one automatically.


<span id="be118035"></span>
### **Configuring a Kafka Subscription**

After selecting the **Kafka** type, complete the following settings on the configuration page:

<span id="33e50bb5"></span>
#### **1. Basic Information**


* **Subscription Name**: (Required) A custom name to identify this event subscription.

* **Description**: (Optional) A custom description of the subscription's purpose.


<span id="6666fab8"></span>
#### **2. Kafka Connection Parameters**


* **Broker Addresses**: (Required) The address(es) of your Kafka cluster. You can configure a single broker or multiple brokers for high availability, separated by commas (`,`).

* **Topic**: (Required) The name of the Kafka topic where SealSuite events will be sent. Ensure this topic already exists in your Kafka cluster.

* **Security Protocol**: The authentication method used to connect to the Kafka cluster.

   * `PLAINTEXT`: Unencrypted, unauthenticated communication. Typically used in trusted internal networks.

   * `SASL_PLAINTEXT`: Uses SASL (Simple Authentication and Security Layer) for client authentication, but data is not encrypted in transit.

   * `SSL`: Uses SSL (Secure Sockets Layer) to establish an encrypted communication channel between the client and brokers, but does not authenticate the client's identity.

   * `SASL_SSL`: The highest security level, using SASL for authentication and SSL for encryption.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When a protocol including <code>SASL</code> is selected (<code>SASL_PLAINTEXT</code>, <code>SASL_SSL</code>), you must configure the following authentication details:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>SASL Mechanism</strong>: Choose the mechanism that matches your Kafka cluster's configuration:   </div>
   

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>PLAIN</strong>: A simple cleartext authentication mechanism. For security, it is recommended to use this only with the <code>SASL_SSL</code> protocol.   </div>
   

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>SCRAM\-SHA\-256 / SCRAM\-SHA\-512</strong>: Recommended secure mechanisms that use a challenge\-response flow, ensuring passwords are not sent in cleartext.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Kafka Username</strong>: The username for SASL authentication.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Kafka Password</strong>: The password corresponding to the username.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When a protocol including <code>SSL</code> is selected (<code>SSL</code>, <code>SASL_SSL</code>), you must configure the following certificate information:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>CA Certificate</strong>: The root certificate used to verify the identity of your Kafka brokers.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>SSL Mutual Authentication</strong>: (Optional) Enable this toggle if your Kafka broker requires clients to present a certificate for authentication (mTLS). When enabled, you must provide:   </div>
   

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Client Certificate</strong>: The certificate file that identifies the SealSuite client to the Kafka broker.   </div>
   

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Client Private Key</strong>: The private key file corresponding to the client certificate.   </div>
   

* **Subscribe to Events**: Select one or more event types you wish to subscribe to from the list.


<span id="61ec1037"></span>
#### **3. Encryption Policy**

You can configure an encryption policy to encrypt the content of the event messages.


* **Verification Token**: (Required) A token included in the event message to verify its origin.

* **Encrypt Key**: (Optional but Recommended) An encryption key used to encrypt the event data payload.


<span id="33d4dc07"></span>
### Configuring a Syslog Subscription

After you select the **Syslog** type, complete the following settings on the configuration page:

<span id="e6c0deae"></span>
#### 1. General

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/413f2d526f614a6fa75a43bac46427ed~tplv-goo7wpa0wc-image.image) </span>


* **Name**: (Required) Enter a custom name to identify this event subscription. Supports multilingual input.

* **Description**: (Optional) Enter a description for this event subscription. Supports multilingual input.


<span id="874e1437"></span>
#### 2. Syslog configuration


* **Protocol type**: Select the transport protocol. Options: **TCP**, **UDP**, and **TCP + TLS**. The default is **TCP**.

   * If you select **TCP + TLS**, TLS encryption is enabled for transmission, and you must upload a **CA certificate** file to verify the identity of the receiving server.

      * If your log server uses a public certificate issued by a trusted CA authority, you typically do not need to upload it (SealSuite trusts it by default).

      * If your log server uses a privately signed certificate issued by your enterprise, you **must upload** your enterprise root certificate. Otherwise, the TLS handshake will fail.

* **Request URL**: Enter the domain name or IP address and port of the server that will receive Syslog messages.

* **Events added**: Select one or more event types you want to subscribe to from the list.


<span id="655a3181"></span>
#### 3. Encryption strategy

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b007474852eb4c0d9d80b7d60676b138~tplv-goo7wpa0wc-image.image) </span>

You can optionally configure an encryption policy to encrypt event data in transit, preventing sensitive enterprise information from being exposed. It also allows you to verify that requests originate from the SealSuite system.


* **Verification Token**: (Required) A token used to verify that requests originate from SealSuite. This value will be included in the event data pushed by SealSuite. You can define a custom value or click the **Reset** icon to generate one automatically.

* **Encrypt Key**: (Optional but Recommended) When configured, SealSuite will encrypt the event data pushed to the Request URL. It is recommended to configure this parameter to enhance data security. You can define a custom value or click the **Reset** icon to generate one automatically.


<span id="455ff867"></span>
## **Managing Event Subscriptions**

After adding an event subscription, it will appear on the **Event Subscription** page, where you can manage all existing subscriptions.

The list provides the following actions:


* **Toggle Switch**: Quickly enable or disable a subscription without deleting it. Only active subscriptions will push events.

* **Details**: Click to open the subscription's detail page.

   * You can view or modify the subscription's configuration.

   * On the **Audit Log** tab, you can view the history of events triggered for this subscription.

* **Delete**: Click to permanently remove the subscription after a confirmation prompt. This action is irreversible.
