---
title: "Collecting the logs of the ingress-nginx add-on"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Collecting-ingress-nginx-logs"
---

Integrated with TLS, VKE clusters allow you to collect the logs of the ingress\-nginx add\-on. This topic describes how to configure and view add\-on logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only describes how to configure and view the logs of the <strong>system default ingress\-nginx</strong> add\-on. If you have deployed a <strong>custom ingress\-nginx</strong> add\-on in your cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers">Best practices for observability of custom NGINX Ingress Controllers</a> for instructions on configuring and viewing its logs.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TLS has been activated. If not, log in to the [TLS console](https://console.byteplus.com/tls) and activate the service based on the on\-screen prompts.

* A **log project** and **log topic** have been created in TLS. For detailed operations, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics)the .

* The log\-collector add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the add\-on is not installed, you will be prompted to install the add\-on on the <strong>Log management</strong> page. Follow the on\-screen prompts to complete the installation.   </div>
   

* The ingress\-nginx add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).


<span id=".6YWN572u5pel5b-X6YeH6ZuG"></span>
## Configuring log collection


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Log management**. On the page that appears, click the **Addon log** tab. Click **Enable ingress access log**.

5. In the pop\-up dialog box, select the **log project** and **log topic** where the add\-on logs will be stored.

6. Click **Confirm**.


<span id=".5p-l55yL5pel5b-X"></span>
## Viewing logs


1. In the left navigation bar of the cluster management page, click **Log management**.

2. On the **Addon log** tab of the **Log management** page, you can view the logs of the ingress\-nginx add\-on.


<span id=".5YWz6Zet5pel5b-X6YeH6ZuG"></span>
## Disabling log collection

You can disable log collection for the ingress\-nginx add\-on. This way, logs from the add\-on will no longer be collected into TLS.


1. On the **Addon log** tab of the **Log management** page, click **Disable ingress access log**.

2. After a secondary confirmation, you can disable log collection for the ingress\-nginx add\-on.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">After you disable add\-on log collection, existing log topics will not be deleted and may still incur fees. If you no longer need the log topics, go to the <a href="https://console.byteplus.com/tls">TLS console </a> to manually delete them. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yig6Zmk5pel5b-X5Li76aKY">Deleting log topics</a>the .</div>


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [Nginx Ingress best practices](https://docs.byteplus.com/en/docs/vke/Nginx-Ingress-best-practices)

* [Best practices for observability of custom NGINX Ingress controllers](https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers)
