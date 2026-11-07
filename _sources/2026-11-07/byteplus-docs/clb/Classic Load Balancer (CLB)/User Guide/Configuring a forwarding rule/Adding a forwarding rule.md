---
title: "Adding a forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Layer 7 listeners support forwarding or redirecting access requests based on the forwarding rules you configure.


* **Ordinary forwarding rule**: Support forwarding requests for different domain names and URLs to specified backend server groups for processing, thereby improving the flexibility of traffic distribution and facilitating rational resource management.

* **Redirect forwarding rule**: Support redirecting requests for a specific domain name and URL to a different protocol, domain name, port, or path. Main application scenarios:

   * When business security requirements are high, you can redirect HTTP requests to HTTPS.

      HTTPS is an encrypted data transmission protocol with higher security, ensuring secure connections for your business.

   * When changing your business domain name, you can redirect the original domain name to the new one to avoid any impact on your business.

   * By redirecting common misspellings of your business domain name to the correct one, you can expand the reach of your business.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Server Group has been created and backend server has been added. For details, see [Creating a server group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group).

* The listener has been created. For details, see [Creating a HTTP protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener) and [Creating a HTTPS protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).


<span id=".5pON5L2c6K-05piO"></span>
## Action notes


* In the same listener, you cannot configure two forwarding rules with exactly the same domain name and URL.

* If the protocol, domain name, port, and path in the redirect configuration are exactly the same as those in the client request, the redirect may become ineffective. Please proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5re75Yqg44CM5pmu6YCa6L2s5Y-R6KeE5YiZ44CN"></span>
### Add Ordinary Forwarding Rule


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Edit listener** to the right of the target CLB instance.

4. Click **Configure forwarding rule** to the right of the target Layer 7 listener.

5. Click **Add forwarding rule**.

6. Configure relevant parameters based on the table below.

   
   |Parameters |Notes |Value |
   |---|---|---|
   |**Trigger condition** |||
   |Domain name |Enter the domain name of the request to be forwarded. The domain name can be a wildcard domain. `*` must be at the beginning or end of the domain name. |www.test.com |
   |URL |The URL to be forwarded must be an absolute path. You can add multiple URLs for the same domain name. |/ |
   |**Forwarding action** |||
   |Forwarding action |Select the action to be performed by the forwarding rule. |Forward to |
   |Server group |The backend server group that receives and processes requests after they match the domain name and URL. IPv6 backend server groups are not currently supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Indicates that forwarding client requests for a specific domain name and URL to a specified backend server group for processing.</div><br> |group\-1 |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the add icon, enter the tag key and tag value, and add tags to the forwarding rule. |* Tag key: rule\-key<br><br>* Tag value: rule\-v1 |
   

7. Click **OK** to complete the action.


<span id=".5re75Yqg44CM6YeN5a6a5ZCR6L2s5Y-R6KeE5YiZ44CN"></span>
### Add Redirect Forwarding Rule


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Edit listener** to the right of the target CLB instance.

4. Click **Configure forwarding rule** to the right of the target Layer 7 listener.

5. Click **Add forwarding rule**.

6. Configure relevant parameters based on the table below.

   
   |Parameters |Notes |Value |
   |---|---|---|
   |**Trigger condition** |||
   |Domain name |Enter the domain name of the request to be forwarded. The domain name can be a wildcard domain. `*` must be at the beginning or end of the domain name. |test.com |
   |URL |Enter the URL to be forwarded. Only absolute paths are supported. You can add multiple URLs for the same domain name.<br><br>Regular expressions are supported, with the following specifications:<br><br><br>* Must start with `~`. Supports uppercase and lowercase letters, numbers, and special characters: . \-` _ / = ? ~ ^ * $ : ( ) [ ] + \|`.<br><br>* `~` can only appear at the beginning, and only once.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">URL support for regular expression is in Beta stage. If you need a trial, please contact your account manager.</div><br> |/ |
   |**Forwarding action** |||
   |Forwarding action |Select the action to be performed by the forwarding rule.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Redirect to</strong> means redirecting requests for the above domain name and URL to the protocol, domain name, port, and path specified below.</div><br> |Redirect to |
   |Agreement |Select the protocol type for redirection. Both HTTP and HTTPS protocols are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the protocol for redirection is the same as the listener protocol, at least one of the domain name, port, or path for redirection must be specified; none can be left empty.</div><br> |HTTPS |
   |Domain name |The domain name you enter for redirection must be an exact domain name that conforms to domain name specifications. |www.test.com |
   |Port |Enter the port to redirect to. |443 |
   |Path |Input the URL path to be redirected to, and it must start with `/`. |/123 |
   |Status code |Select the status code for redirection.<br><br><br>* **301**: Indicates that the requested resource has been permanently moved to a new URL. The client should use the new URL for subsequent requests.<br><br>* **302**: Indicates that the requested resource has been temporarily moved to a new URL but may change again. The client should use the new URL for subsequent requests.<br><br>* **307**: Similar to **302**, but requires the client to preserve the request method when redirecting. For example, if the original request is a GET request, it will remain a GET request after redirection.<br><br>* **308**: Similar to **301**, but requires the client to keep the request method unchanged when redirecting. |301 |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the add icon, enter the tag key and tag value, and add tags to the forwarding rule. |* Tag key: rule\-key<br><br>* Tag value: rule\-v1 |
   

7. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateRules](https://docs.byteplus.com/en/docs/clb/CreateRules)
