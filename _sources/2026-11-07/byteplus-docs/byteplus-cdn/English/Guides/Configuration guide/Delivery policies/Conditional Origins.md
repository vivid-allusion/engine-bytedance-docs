---
title: "Conditional Origins"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/conditional_origins_en"
---

In addition to the basic origin configuration, CDN provides the **Conditional Origins** feature. This feature lets CDN route the origin fetch to a specific origin based on the characteristics of the user request.

<span id="fb6fd6ea"></span>
## Origin Selection Logic

After CDN receives a user request:


* If the request matches a rule in Conditional Origins, CDN performs the origin fetch from the origin specified in that rule.

* Otherwise, CDN selects the origin based on the basic origin configuration.


<span id="c96ff9a4"></span>
## Origin Retry

See [Origin Retry Logic](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en).

<span id="e5b2968f"></span>
## Steps


1. Open the **Origins** tab. For instructions, see [Domain Name Configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. In the **Origins** module, click  **+ Conditional Origins**, and then enable **Conditional Origins**.

3. Click **Add Rule**. You can add up to 20 rules. Rules are prioritized. See [Rule Priority](https://docs.byteplus.com/en/docs/18/27431#rule-priority).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To increase the rule limit, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.   </div>
   

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604121216-1463094658902.png) </span>

4. Refer to the [Configuration Instructions](https://docs.byteplus.com/en/docs/18/27431#bac52cb6) to configure the rules.

5. After configuring all rules, click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604121116-1440691142039.png) </span>

<span id="bac52cb6"></span>
## Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Match Conditions |Defines one or more match conditions, up to 50, for matching user requests. Click **Add** to create a match condition.<br><br>You can specify the relationship between these match conditions, which is **Or** by default.<br><br>You can select from the following match objects:<br><br><br>* **URL Path**<br><br>* **URL Path Directory**<br><br>* **URL Path Extension**<br><br>* **Client IP**<br><br>* **Request Query Param**: A specific query parameter in the request URL.<br><br>* **URL Query String**: All query parameters in the request URL.<br><br>* **Request Header**: A header in the user request.<br><br><br>See [Appendix I](https://docs.byteplus.com/en/docs/18/27431#appendix-1) for the match types corresponding to each match object, as well as the input requirements and examples for match values. |
|Origin Role |Indicates the origin mode. The following options are available:<br><br><br>* **Primary**<br><br>* **Secondary**<br><br><br>The total number of primary and secondary origins cannot exceed 50. |
|Origin Type |Indicates the origin type. The following options are available:<br><br><br>* **IP Address**: The origin is an IP address.<br><br>* **Domain Name**: The origin is a domain name.<br><br>* **Object Storage**: The origin is an object storage bucket. |
|Origin Address |See the description in [Origin configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-configurations#origin-configuration-instructions-for-ip-address-and-domain-name-types). |
|HTTP Port ||
|HTTPS Port ||
|Origin Hostname ||


<span id="19400524"></span>
## Rule Priority

Each rule in the list has a priority, with 1 being the highest. When the CDN receives a user request, it matches the request against the rules in descending order of priority. If a request meets the conditions of a rule, the settings in that rule are applied, and the CDN stops matching the request against any remaining rules. You can drag rules to adjust their priority.

<span id="e748bdca"></span>
## More Information

<span id="172a248c"></span>
### Appendix I

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Regex matching is case\-insensitive.</div>



|**Matching Object** |**Available Match Types** |**Match Value Input Requirements** |**Match Value Example** |
|---|---|---|---|
|URL Path |* Equal To, Not Equal To<br><br>* Match Regex, Not Match Regex |* Must start with a slash (/).<br><br>* Can include the wildcard character `*`, but it cannot be just `*`.<br><br>* The total length cannot exceed 1,024 characters.<br><br>* Separate multiple paths with semicolons (;). The total length cannot exceed 1,024 characters.<br><br>* Cannot contain the following characters:<br><br>   * Double slashes (//), spaces, dollar signs ($), and question marks (?). |`/www/img/my*image.png;/docs/file` |
|URL Query String |* Match Regex, Not Match Regex |* The total length cannot exceed 1,024 characters.<br><br>* Separate multiple regular expressions with semicolons (;). |`^a{1,2}b(.*)g=val[1-3]` |
|URL Path Directory |* Equal To, Not Equal To |* Must start and end with a slash (/).<br><br>* The total length cannot exceed 1,024 characters.<br><br>* Separate multiple directories with semicolons (;).<br><br>* Cannot contain the following characters:<br><br>   * Double slashes (//), spaces, dollar signs ($), and question marks (?). |`/www/img/;/docs/folder/` |
|URL Path Extension |* Equal To, Not Equal To |* Can only contain letters and numbers.<br><br>* The total length cannot exceed 1,024 characters.<br><br>* Cannot start with a period (.).<br><br>* Separate multiple extensions with semicolons (;). |`png;jpg` |
|Client IP |* Equal To, Not Equal To<br><br>* Belong to, Not Belong To: indicates whether the client IP address belongs to your specified countries and regions. |For IP addresses:<br><br><br>* You can specify up to 5 IP addresses or CIDR blocks.<br><br>* Only IPv4 addresses and IPv4 CIDR are supported.<br><br>* Separate multiple IP addresses with semicolons (;). |xx.xx.xx.x;xxx.xxx.xxx.xx |
|Request Query Param |* Equal To, Not Equal To<br><br>* Match Regex, Not Match Regex<br><br>* Exist, Not Exist<br><br>* Empty, Not Empty |**Parameter Name**<br><br><br>* Each match condition can have only one parameter name.<br><br>* The length cannot exceed 256 characters.<br><br>* It can only contain numbers, letters, underscores (_), hyphens (\-), and periods (.).<br><br><br>**Parameter Value**<br><br><br>* Separate multiple parameter values with semicolons (;). The total length cannot exceed 1,024 characters. |**Parameter Name**<br><br>param<br><br>**Parameter Value**<br><br>p_value1;p_value2 |
|Request Header |* Match, Not Match<br><br>* Empty, Not Empty |**Header Name**<br><br><br>* Only one header name can be specified in each match condition.<br><br>* The length cannot exceed 1,024 characters.<br><br>* Cannot contain Chinese characters, underscores (_), spaces, double quotes ("), or colons (:).<br><br><br>**Header Value**<br><br><br>* You can specify up to 50 values, separated by vertical bars (\|).<br><br>* The total length cannot exceed 1,024 characters.<br><br>* Header values can start or end with a wildcard character `*`, but cannot be just `*`. |**Header Name**<br><br>header<br><br>**Header Value**<br><br>header_value1 |
