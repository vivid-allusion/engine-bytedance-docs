---
title: "Publish Resource and Subscription Resource"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132443"
---

<span id="publishing-resources"></span>
## Publishing Resources

You must create a publishing resource before starting publishing media streams.

Publishing resources are objects assigned by the WTN server for a specified stream name. You can create them by calling the [Create Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132482) API.

When initiating a publish task, the server generates a publish object that includes relevant status information, such as the stream's mute status.

<span id="lifecycle-of-publishing-resources"></span>
### Lifecycle of Publishing Resources

After a publishing resource is destroyed, clients can no longer connect to it, and any existing connections are disconnected.

You can actively destroy the publishing resource by:


* Invoking the API to destroy the publishing resource.

* Invoking the API to re\-publish. In this case, the original publishing resource will be destroyed.


Under the following circumstances, the publishing resource will be destroyed by WTN:


* The publishing resource is created, but a connection is not established within 30 seconds.

* After publishing has started, the publisher's connection to WTN is disconnected due to network issues and cannot be re\-established within 30 seconds.


<span id="correspondence-between-publish-and-subscription-resources"></span>
### Correspondence Between Publishing and Subscription Resources

The correspondence between publishing resources and subscription resources can be 1v0, 1v1, or 1vN.

When a publishing resource is destroyed, all corresponding subscription resources are also destroyed.

<span id="special-scenarios-for-subscribers"></span>
## Special Scenarios for Subscribers

The publisher's behavior affects the corresponding subscriber's behavior. The affected situations are as follows:


|Scenario |Publisher's Behavior |Subscriber's Behavior |
|---|---|---|
|1 |Not publishing. |Subscription returns `404`. |
|2 |During the publishing process, the publishing resource is destroyed. |The subscription connection is disconnected. When re\-subscribing, it returns `404`. |
|3 |During the publishing process, the connection to the WTN server is disconnected due to network issues and is restored within 30 seconds. |* Clients currently subscribing: The connection to the WTN server is not disconnected, and the subscriber's display holds the last received frame. After the publisher's connection is restored, the subscriber receives the media stream again.<br><br>* Clients that start subscribing while the publisher is disconnected: Successfully connect to the WTN server and receive a black frame. After the publisher's connection is restored, the subscriber receives the normal media stream. |
|4 |During the publishing process, the connection to the WTN server is abnormally disconnected due to network reasons, and it is not restored within 30 seconds. |Clients currently subscribing: The connection with the WTN server is not disconnected. After the publishing resource is destroyed, the subscription connection is disconnected.<br><br>Clients that start subscribing while the publisher is disconnected: Successfully connect to the WTN server. After the publishing resource is destroyed, the subscription connection is disconnected. |
|5 |The publishing resource is re\-established using the same parameters. |The subscribed media stream will switch to the new publishing resource. |
