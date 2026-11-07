---
title: "Creating/Deleting a security policy"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Creating-Deleting-security-policy"
---

<span id="Bl1K8Mrj"></span>
## Create custom security policy

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The TLS listener is currently in Beta. For trial requests, contact your account manager.</div>


When system default policies cannot meet your requirements, you can customize security policies as needed.


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation tree, select **TLS Security Policy**.

3. In the top menu bar, select the target project and region.

4. In the **Custom policy** tab, click **Create custom policy**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sampling Example |
   |---|---|---|
   |Name |Input the name of the custom security policy. |TLS_v1.3_GCM |
   |TLS protocol |Select one or more TLS protocol versions.<br><br><br>* TLSv1.0<br><br>* TLSv1.1<br><br>* TLSv1.2<br><br>* TLSv1.3 |TLSv1.3 |
   |Cipher suite |Select Cipher suite. For details, please refer to Overview. |* TLS_AES_256_GCM_SHA384<br><br>* TLS_AES_128_GCM_SHA256 |
   |Project |The project to which the custom security policy belongs. |default |
   |Tags |Input the tag |tlsv1.3 : GCM |
   

6. Click **OK** to complete the action.


<span id="lF24SD6u"></span>
## Delete custom security policy

System default policies do not support deletion. When you no longer need the target custom security policy, you can delete it.


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation tree, select **TLS Security Policy**.

3. In the top menu bar, select the target project and region.

4. On the **Custom policy** tab, click **Delete** to the right of the target policy.

5. Click **Delete** to complete the action.


<span id="yBKVez9V"></span>
## Related documents


* [CreateNLBSecurityPolicy](https://docs.byteplus.com/en/docs/clb/CreateNLBSecurityPolicy)

* [DeleteNLBSecurityPolicy](https://docs.byteplus.com/en/docs/clb/DeleteNLBSecurityPolicy)
