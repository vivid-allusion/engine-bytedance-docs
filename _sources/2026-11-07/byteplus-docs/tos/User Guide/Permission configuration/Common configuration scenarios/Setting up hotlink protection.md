---
title: "Setting up hotlink protection"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-configuring-hotlinking-protection"
---

You can set a Referer allowlist to control requests to a bucket.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

When a browser sends a request to a web server, the request header will contain a Referer, which indicates the source page of the request. You can configure Referer conditions in Torch Object Storage (TOS) to allow or deny access.

<span id="74611ec1"></span>
## Scenario description


* Account: all users.

* Resource: all objects.

* Action: all actions.

* Condition: key is Referer, condition operator is equals, value is http://console.volcengine.com.


<span id="7a20d902"></span>
## Recommended configuration method

We recommend using the bucket policy for this scenario.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**, then on the **Buckets** page click on the target bucket name.

3. In the left navigation bar, select **Permissions \> Bucket Policies**.

4. Select the authorization method as needed.

* Visual view

   1. Click **Create Policy**.

   2. At the bottom of the **Create Bucket Authorization Policy** page, select **Custom Policy** and click **Next**.

   3. Set the following parameters.

      * **Policy name**: Click **Basic configuration** and set the policy name.

      * **Effect**: Allow means allowing accesses from sources that meet the conditions, and Deny means denying accesses from sources that meet the conditions. This text is set to **Allow**.

      * **Authorized Users**: Select **All users**.

      * **Resource Scope**: Select **Current bucket** and **Objects in bucket**, and select **All Objects**.

      * **Action**: Select  **\*** , which represents all actions.

      * **Condition**: Click the **Add Field** , set **Key** to **Referer**, **Condition operator** to **Equal To**, and **Value** to **http://console.volcengine.com**.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When using the 'like' operator, the wildcard \* is supported. For more information about operators, please see <a href="https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#nk9G2rUC">Conditions</a>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Supports input of regular domains, wildcard domains, and IP addresses.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Before the address, enter http:// or https://.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When entering multiple addresses, separate them with a comma (,).      </div>
      

   4. After setting up, click **Next**.

   5. After confirming the strategy is correct, click **Create**.

* JSON view

   Click **Edit**, copy the content below into the textbox, then click **Save**.

   ```Plain
   {
     "Statement": [
       {
         "Sid": "custom policy-c1db",
         "Effect": "Allow",
         "Principal": [
           "*"
         ],
         "Action": "tos:*",
         "Resource": [
           "trn:tos:::test3",
           "trn:tos:::test3/*"
         ],
         "Condition": {
           "StringEquals": {
             "tos:referer": [
               "http://console.volcengine.com"
             ]
           }
         }
       }
     ]
   }
   ```
