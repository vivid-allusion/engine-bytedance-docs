---
title: "Diagnostic tools"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools"
---

BytePlus CDN provides a suite of diagnostic tools to help you troubleshoot issues and analyze your service configuration. You can use these tools to verify if an IP address belongs to a CDN node, compare configuration differences between two domains, or analyze discrepancies between two acceleration policies. This helps you quickly identify and resolve potential access or configuration problems.


* [IP detection](https://docs.byteplus.com/en/docs/18/6629#ip-detection)

* [Domain comparison](https://docs.byteplus.com/en/docs/18/6629#domain-name-comparison)

* [Policy comparison](https://docs.byteplus.com/en/docs/18/6629#policy-comparison)


<span id="ip-detection"></span>
## IP detection

After adding your site to the CDN, if you experience slower than expected access speeds, use this tool to verify if a user's IP address belongs to a CDN node.

You can query up to 50 IPv4 and IPv6 addresses at a time. Separate multiple IP addresses with line breaks or semicolons (;).

If an IP address is a CDN node IP address, the check result will also show the location of the IP address. If the location is in China, the result also shows the IP address's network operator.

<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click **Tools Center** \> **Diagnostic Tools**.

3. On the **Diagnostic Tools** page, click **Getting Started** under **IP Detection**.

4. On the **IP Detection** page, enter the IP address to be queried, and then click **Query**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_82ff49abe75a2b0e52fe012afde1e9b7.png) </span>

<span id="domain-name-comparison"></span>
## Domain name comparison

Use this tool to compare the configurations of two domain names. This tool calls the DescribeCdnConfig API to retrieve the configuration of the specified domain names, and then highlights differences in the API parameters.

For definitions of the parameters in the comparison results, see the following API documentation: [DescribeCdnConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_en-us).

<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click **Tools Center** \> **Diagnostic Tools**.

3. On the **Diagnostic Tools** page, click **Getting Started** under **Domain Name Comparison**.

4. On the **Configuration Differences** page, specify the domain names to compare, and the tool will display the differences.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8283d0c00fd283bc88bfb00709d4e504.png) </span>

<span id="policy-comparison"></span>
## Policy comparison

This tool is used to compare the configuration differences between two policies. The comparison results are displayed in the following tabs:


* General Configurations: Shows the differences in basic information between the two policies.

* Feature Configurations: Shows the differences in CDN feature configurations between the two policies.

* Bound Domains: Shows the differences in the domain names bound to the two policies.


When using this tool, you need to specify the policy type and then select two policies to compare their configurations.


* If the policy type is delivery policy, this tool calls the DescribeServiceTemplate API to obtain the configuration of the two policies and then displays the configuration differences in these three tabs.

* If the policy type is encryption policy, this tool calls the DescribeCipherTemplate API.


In the **Feature Configurations** tab, this tool highlights the configuration differences of CDN features at the API level. For the definition of each parameter in the comparison results,


* If you are comparing two delivery policies, see [DescribeServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describeservicetemplate-00652).

* If you are comparing two encryption policies, see [DescribeCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describeciphertemplate-f8c12).


<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click **Tools Center** \> **Diagnostic Tools**.

3. On the **Diagnostic Tools** page, click **Getting Started** under **Policy Comparison**.

4. On the **Configuration Differences** page, select the policy type and the policies to compare.


**Example screenshot of a general configuration comparison**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b17c529a854cdbb9271229aef6777457.png) </span>

**Example screenshot of a feature configurations comparison**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f0f0a6d38b2ac29fef9a9b6de9709fa6.png) </span>

**Example screenshot of a bound domains comparison**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c0f6f95033fd78b86d844c331fad9cdb.png) </span>
