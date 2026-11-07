---
title: "Add a CNAME record"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Adding_CNAME_record"
---

After you bind a custom domain name to the service, you need to add a CNAME record at your DNS provider to point your custom domain name to the default domain name of the current service in API Gateway. You can copy the default domain name information on the service's domain name management page. If you do not add a CNAME record, client requests sent via a custom domain name cannot be correctly resolved to the API Gateway. This article introduces common ways to configure CNAME records with DNS service providers.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the CNAME record has been added, please wait patiently for the configuration to take effect. The time it takes for a CNAME record to take effect depends on the TTL value you configure.</div>


* <div data-tips="true" data-tips-type="tip">You can go to the API Gateway console to check whether the domain name has taken effect. After the configuration takes effect, the domain name status will change from <strong>CNAME not effective</strong> to <strong>In progress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The update time for the domain name status in the console may be slightly slower than the actual effective time. You can refresh it using the <strong>Refresh</strong> button.</div>



<span id=".5Zyo54Gr5bGx5byV5pOO5re75YqgIENOQU1FIOiusOW9lQ=="></span>
## Add a CNAME record in BytePlus

If your DNS service provider is BytePlus, configure the CNAME record as follows. 


1. Log in to the [Cloud DNS console](https://console.byteplus.com/auth/login?redirectURI=%2FTrafficRoute%2Fdns%2Fpublic-zone).

2. On the public network domain name management page, find the domain name bound to the API Gateway and click it.

3. On the Record Management tab, click **Add Record**.

4. In the add record panel, configure the following information as required, and leave other parameters at their default values.

   
   |**Configuration Item** |**Descriptions** |
   |---|---|
   |Domain name |Enter the host record (the domain name prefix) to complete the subdomain for resolution.<br><br><br>* If you want to configure the resolution for www.example.com, set the host record to www.<br><br>* If you are configuring DNS for example.com, set the host record to '@'. |
   |Record types |Select a CNAME record here to point your domain name to another domain name. |
   |Recorded value |Enter the domain name that the CNAME should point to. Directly copy the default domain name of the current Service in the API Gateway. |
   

5. Click **Submit** to complete the configuration.


<span id=".5Zyo6Zi_6YeM5LqR77yI5LiH572R77yJL-iFvuiur-S6kS_mlrDnvZHmt7vliqAgQ05BTUUg6K6w5b2V"></span>
## Add a CNAME record in other DNS service provider

If you use other DNS service provider , please configure the CNAME record in the following way. Detailed procedure can be consulted in the corresponding official documentation.


1. Log in to the console of the relevant domain name service provider, locate the domain name that is bound to the API Gateway, and add a DNS record.

2. Configure the following information as required; keep other parameters at their default values.

   
   |**Configuration Item** |**Descriptions** |
   |---|---|
   |Record types |Select the CNAME record here to point your domain name to another domain name. |
   |Host record |Enter the host record, that is, the domain name prefix.<br><br><br>* To configure the DNS record for www.example.com, set the host record to www.<br><br>* When configuring DNS for example.com, set the host record to '@'. |
   |Recorded value |Enter the domain name that the CNAME should point to. Directly copy the default domain name of the current service in the API Gateway. |
   

3. Click **Submit** to complete the configuration.
