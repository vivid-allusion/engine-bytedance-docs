---
title: "FAQs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/faq"
---

This article describes issues you may encounter when using Cloud Search.

<span id=".5LqR5pCc57Si5pyN5Yqh5pSv5oyB5YyF5bm05YyF5pyI5ZCX77yf"></span>
### Does Cloud Search support Subscription?

Yes. For an overview of Cloud Search billing, refer to [Billing instruction](https://docs.byteplus.com/docs/cloudsearch/billing-overview).

<span id=".5pSv5oyB5oyJ6YeP6K6h6LS56L2s5YyF5bm05YyF5pyI5LmI77yf"></span>
### Is it possible to switch from Pay\-as\-you\-go to Subscription?

Yes. For detailed steps, refer to [Convert from Pay-as-you-go to Subscription](https://docs.byteplus.com/docs/cloudsearch/changing-billing-method).

<span id=".5YyF5bm05YyF5pyI5a6e5L6L5Y-v5Lul5Y-W5raI5LmI77yf"></span>
### Can a Subscription instance be canceled?

Yes. Subscription instances support a 7\-day unconditional unsubscription.

<span id="cd51f7b4"></span>
### The error "class file has wrong version" is reported when connecting to an instance by using the OpenSearch 2.9 Java SDK.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9c5a9f29a07424c96f2cb29b19521f5~tplv-goo7wpa0wc-image.image) </span>

Connecting to an OpenSearch instance by using Java requires at least JDK 11, whereas connecting to an ES instance requires at least JDK 1.8.

An error occurs if your JDK version is too low. You need to upgrade the JDK version to connect to the OpenSearch instance.

<span id="1fe18156"></span>
### Within minutes, the instance experiences a request backlog, CPU usage reaches 100%, and all requests become almost completely unavailable.

When requests surge, this issue occurs within minutes primarily due to the instance's **internal queue backlog** and **excessive threads**.

The solution is: for requests dequeued from the instance's internal queue, search\-related requests will be aborted if their queuing time exceeds the threshold (default: 10s) instead of being executed.

You can dynamically update the timeout in the search queue. The command is as follows:

```Java
PUT _cluster/settings
{
    "persistent": {
        "thread_pool.search.queue_wait_timeout":"30s"
    }
}
```


For more information about controllable delay queues, refer to [Controllable delay queues](https://docs.byteplus.com/docs/6465/1276617).

<span id="976a0ff8"></span>
### Why is public network access unavailable after it has been enabled?

Public network access has been enabled for the instance and Kibana/Dashboards, but an `ERR_CONNECTION_TIMED_OUT` error occurs during access. This issue most likely occurs because **the associated public EIP has been disassociated**.

Follow these steps to troubleshoot the issue:


1. Get the inaccessible public domain name, such as `visual-o-00gr**.escloud.volces.com`.

2. Get the IP address for the domain name.

   * Use the `ping` command in a command\-line tool to check for accessibility and get the IP address for the domain name.

      If a `timeout` or `request timed out` error is returned, the public domain is inaccessible. Get the public IP address for the domain name and search for it in the EIP console.

      ```JSON
      ping visual-o-00gr**.escloud.volces.com
      PING visual-o-00gr**.escloud.volces.com (180.184.*.*): 56 data bytes
      Request timeout for icmp_seq 0
      Request timeout for icmp_seq 1
      Request timeout for icmp_seq 2
      ```
      

   * Alternatively, use a domain name resolution tool, such as DNSChecker or an IP finder. Enter the domain name on the tool's webpage to get its corresponding IP address.

3. [Log in to the EIP console](https://console.byteplus.com/eip) and search by public IP on the **Public IP** page.

   * The target EIP status is **not associated**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6ca577cd14e43108cc724cea1c452dc~tplv-goo7wpa0wc-image.image) </span>

   * If an EIP is associated with a cloud resource, its status is **associated**, and the associated resource is displayed. For example, `public-kibana-00g0**` and `public-es-00g0**` are suffixed with instance or Kibana/Dashboards.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c44f576cf5824257bf8c0a30403d40c6~tplv-goo7wpa0wc-image.image) </span>

4. After you confirm that the associated EIP is disassociated, disable public access for the instance and Kibana/Dashboards, and then re\-enable public access and associate a new EIP.

   * [Configure public access for an instance](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access)

   * [Configure public access for Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access-tool)
