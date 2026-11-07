---
title: "Denying access to buckets based on IP addresses"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-implementing-ip-address-based-access-control-on-buckets"
---

This document explains how to restrict bucket access by setting source IP addresses.

<span id="50610747"></span>
## Scenario description


* Authorized account: a `user` account under another account (using `210000****` as an example).

* Authorized resource: all objects under the `bucketname` bucket.

* Restricted IP: deny access to the authorized resource from `192.168.1.0` and `1080:0:0:0:8:800:200C:417A`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to allow only specified IP addresses to access the bucket, change the <strong>condition operator</strong> in this example to <strong>Not equal</strong> (in JSON view, change <code>IpAddress</code> to <code>NotIpAddress</code>).</div>


<span id="f3c3b392"></span>
## Recommended configuration method

You need to use a bucket policy for authorization in this scenario. For detailed information on bucket policies, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_5).

<span id="6230b10f"></span>
## Precautions

If a configured permission does not take effect, we recommend that you retry later, as there is a delay.

<span id="439e81f7"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**, then on the **Buckets** page, click on the target bucket name.

3. In the left navigation bar, select **Permissions \> Bucket policies**.

4. Choose the authorization method as needed.

* Visual view

   1. Click **Create policy**.

   2. On the **Create Storage Bucket Authorization Policy** page, select the **Folder Read\-Only** template, then click **Next**.

   3. Set the following parameters.

      * **Effect**: Select **Deny**.

      * **Authorization user**: Select **Specified account**.

      * **Other accounts**: Select **Other main account**, enter the other main account ID, click **Add Field**, enter **Sub account name**, using user as an example.

      * **Resource**: Select All objects, using **All objects** as an example.

      * **Condition**: Click **Add Field**, set IP parameters.

         * **Key**: SourceIP

         * **Conditional operator**: Equal To

         * **Value**: 192.168.1.0.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Supports adding IPv4 and IPv6 addresses. For detailed instructions, please see <a href="https://docs.byteplus.com/docs/tos/docs-templates-and-parameters">Bucket policy templates and parameters</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">This document's IP address is for reference only; you need to set the IP address according to actual needs. You can click <strong>Add Field</strong> to set multiple IP addresses.      </div>
      

   4. After setup is complete, click **Next**.

   5. After confirming the policy is correct, click **Create**.

* JSON View

   Click **Edit**, copy the following content into the text box, and click ** Save**.

   ```JSON
   {
     "Statement": [
       {
         "Sid": "fold read-only-10c1",
         "Effect": "Deny",
         "Principal": [
           "210000****/user"
         ],
         "Action": [
           "tos:ListBucket",
           "tos:HeadBucket",
           "tos:ListBucketVersions",
           "tos:GetObject",
           "tos:GetObjectAcl",
           "tos:GetObjectVersion"
         ],
         "Resource": [
           "trn:tos:::bucketname",
           "trn:tos:::bucketname/*"
         ],
         "Condition": {
           "IpAddress": {
             "tos:sourceip": [
               "192.168.1.0",
               "1080:0:0:0:8:800:200C:417A"
             ]
           }
         }
       }
     ]
   }
   ```
