---
title: "Flink Access to PrivateLink Domain Name Resolution (Services like EMR)"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_Access_to_PrivateLink_Domain_Name_Resolution"
---

In specific scenarios, Flink needs to access external services via Private Link. For example, Flink accesses services like EMR via Priavte Link domain names. This article introduces how to enable Flink to access specified services via Private Link.

Serverless Flink does not resolve domain names in Private Link by default; two custom Flink parameters are needed to inject the domain names into the Flink runtime environment.

```YAML
containerized.master.env.ENV_SEARCH_DOMAIN: Private domain name suffix that needs to be resolved
containerized.taskmanager.env.ENV_SEARCH_DOMAIN: Private domain name suffix that needs to be resolved
```


<span id="4afaefab"></span>
## Practice Case

<span id="73d52a53"></span>
### Accessing EMR Services


1. Without special configurations in Flink tasks, accessing EMR services fails with errors unable to resolve the domain name address of EMR nodes.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c5e660dfcaf4a5fbb8bd4fb1b63a40f~tplv-goo7wpa0wc-image.image" width="2098px" /></div>



2. Review the DNS domain name of nodes in EMR, extract `"cn-beijing.xxx.xxx.byteplus.com"` from the figure, and note that domain names vary across different clusters.

3. Add related settings in Flink's custom parameter configuration.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92c6ddef75e14af2b78e29d63c1bc71d~tplv-goo7wpa0wc-image.image" width="732px" /></div>



4. After the launch, tasks can now be correctly resolved to the service address corresponding to EMR's domain name.


<span id="31bae29a"></span>
### Access other PrivateLink services

If other services have provided a PrivateLink domain or set up their own PrivateLink domain, similar to accessing EMR services, the corresponding domain suffix needs to be added to Flink's custom parameters.
