---
title: "Use cases for QoS policies"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Qos-policy-use-cases"
---

This topic outlines how to use QoS policies for various business needs.

<span id="29d39320"></span>
## Use cases

The following use cases cover different scenarios. Choose the one that best fits your needs.


|**Use case** |**Description** |
|---|---|
|[Setting different throttling limits for various services accessing the same TOS resources](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases#f08bd1a6) |Where multiple services (e.g., vePFS and EMR) access the same TOS resources, use QoS policies to throttle the bandwidth for the IAM roles corresponding to each service. This ensures that the traffic behaviour of one service does not affect the others, as each service operates independently with dedicated traffic quotas. |
|[Applying throttling at the workload level](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases?lang=en#pyqUzCb3) |Where multiple workloads (e.g., from vePFS or an IAM user) access different TOS resources, use QoS policies to throttle the bandwidth for each workload. This ensures that the traffic behaviour of one workload does not affect the others, as each workload operates independently with dedicated traffic quotas. |
|[Throttling bandwidth for a specific bucket](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases#f5a1f3e6) |Use a QoS policy to limit the upload bandwidth for a specific bucket, thereby preventing traffic spikes for that bucket from affecting other buckets. |
|[Throttling bandwidth for a specific user](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases#82a17b1d) |Use a QoS policy to limit the bandwidth of a user accessing TOS, thereby preventing them from consuming excessive bandwidth. |
|[Prioritizing bandwidth for a specific bucket](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases#66d99285) |Use a QoS policy to prioritize bandwidth for one bucket while limiting bandwidth for other buckets. |
|[Prioritizing bandwidth for a specific user](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases#8e24cd73) |Use a QoS policy to prioritize bandwidth for one user while limiting bandwidth for other users. |
|[Implementing priority‑based throttling for various services accessing the same TOS resources](https://docs.byteplus.com/en/docs/tos/Qos-policy-use-cases?lang=en#eErA0lLq) |Where multiple services (e.g., vePFS and EMR) access the same TOS resources, use QoS policies to allocate guaranteed bandwidth and priorities to the corresponding IAM roles for each service. This maximizes resource utilization and achieves business stability. |
|[Implementing priority‑based throttling across multiple buckets](https://docs.byteplus.com/en/docs/tos/Qos-policy-use-cases#M3pP9dXm) |For multi\-bucket scenarios, use QoS policies to set the guaranteed bandwidth and priorities for each bucket and the IAM roles associated with your services accessing that bucket. This maximizes resource utilization and achieves business stability. |


<span id="f08bd1a6"></span>
## Setting different throttling limits for various services accessing the same TOS resources

In this section, we will set the write bandwidth limits for the 'bucketevent' bucket to 3,000 and 2,000 Mbps for vePFS and EMR, respectively.

<span id="e9d9d619"></span>
### Step 1: Throttle the bandwidth for vePFS


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="fGVkRcVw5E" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 3,000.
   
         * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Role name** section, click **Add row** to apply **ServiceRoleForVEPFS**.
   
         * User Policy: Select **Include the above users**.
   
         * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent and **Scope of application** to **All objects**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="RTbBrlek5F" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
         "Sid": "test",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "3000",
           "ReadsRate": ""
         },
         "Principal": [
           "trn:iam::214748****:role/ServiceRoleForVEPFS"
         ],
         "Resource": "trn:tos:::bucketevent/*"
       }
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

&nbsp;


<span id="5e380693"></span>
### Step 2: Throttle the bandwidth for EMR


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="kHJSFf0iIe" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test2.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 2,000.
   
         * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Role name** section, click **Add row** to apply **ServiceRoleForEMROLAP**.
   
         * User Policy: Select **Include the above users**.
   
         * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent and **Scope of application** to **All objects**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="swUXmtgCQj" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   <div data-tips="true" data-tips-type="warning">In JSON, elements are separated by commas (,). Before copying new content into the <code>Statement</code>, add a comma (,) after the QoS rules for vePFS.</div>
   
   
   ```JSON
   {
         "Sid": "test2",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "2000",
           "ReadsRate": ""
         },
         "Principal": [
           "trn:iam::214748****:role/ServiceRoleForEMROLAP"
         ],
         "Resource": "trn:tos:::bucketevent/*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="pyqUzCb3"></span>
## Applying throttling at the workload level

In this section, we will use vePFS and the IAM user "aaa" as examples. We will set the write bandwidth limit to 5,000 Mbps for vePFS when accessing the "bucketevent1" bucket, and the write bandwidth limit to 3,000 Mbps for aaa when accessing the "bucketevent2" bucket.

<span id="24d70a4e"></span>
### Step 1: Throttle the bandwidth for vePFS


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="qTftMix9bm" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 5,000.
   
         * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Role name** section, click **Add row** to apply **ServiceRoleForVEPFS**.
   
         * User Policy: Select **Include the above users**.
   
         * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent1 and **Scope of application** to **All objects**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="F7sjnnZ9TU" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
         "Sid": "test",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "5000",
           "ReadsRate": ""
         },
         "Principal": [
           "trn:iam::214748****:role/ServiceRoleForVEPFS"
         ],
         "Resource": "trn:tos:::bucketevent1/*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="151f8b87"></span>
### Step 2: Throttle the bandwidth for the specified user


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="O5mWgQggYP" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test2.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 2,000.
   
         * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Sub account name** section, click **Add row** and select **aaa** from the list.
   
         * User Policy: Select **Include the above users**.
   
         * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent2 and **Scope of application** to **All objects**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="dT4J2T6to4" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   <div data-tips="true" data-tips-type="warning">In JSON, elements are separated by commas (,). Before copying new content into the <code>Statement</code>, add a comma (,) after the QoS rules for vePFS.</div>
   
   
   ```JSON
   {
         "Sid": "test2",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "2000",
           "ReadsRate": ""
         },
         "Principal": [
           "trn:iam::214748****:user/aaa"
         ],
         "Resource": "trn:tos:::bucketevent2/*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="f5a1f3e6"></span>
## Throttling bandwidth for a specific bucket

In this section, we will use the 'bucketevent' bucket in China (Beijing) as an example. The default write bandwidth limit for this region is 10,000 Mbps, but we will limit this bucket's write bandwidth to 3,000 Mbps.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="2YlARXNf" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test3.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 3,000.
   
         * Authorized user: Select **All users**.
   
         * User Policy: Select **Include the above users**.
   
         * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent and **Scope of application** to **All objects**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="WdSAKBod" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
         "Sid": "test3",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "3000",
           "ReadsRate": ""
         },
         "Principal": [
           "*"
         ],
         "Resource": "trn:tos:::bucketevent/*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="82a17b1d"></span>
## Throttling bandwidth for a specific user

In this section, we will set a write bandwidth limit of 3,000 Mbps for the IAM user "aaa" in China (Beijing).


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="ULMM4Orm" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test4.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 3,000.
   
         * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Sub account name** section, click **Add row** and select **aaa** from the list.
   
         * User Policy: Select **Include the above users**.
   
         * Resource: Select **All buckets**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="yFDyq5ir" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
         "Sid": "test4",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "3000",
           "ReadsRate": ""
         },
         "Principal": [
           "trn:iam::214748****:user/aaa"
         ],
         "Resource": "*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="66d99285"></span>
## Prioritizing bandwidth for a specific bucket

In this section, we will use the 'bucketevent' bucket in China (Beijing) as an example. The default write bandwidth limit for this region is 10,000 Mbps. To ensure 'bucketevent' has a write bandwidth limit of 7,000 Mbps while the other buckets in this region collectively have a limit of 3,000 Mbps, we will set the limit for the other buckets to 3,000 Mbps.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="LT3R6xYz" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test3.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 3,000.
   
         * Authorized user: Select **All users**.
   
         * User Policy: Select **Include the above users**.
   
         * Resource scope: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent and **Scope of application** to **All objects**.
   
         * Resource strategy: Select **Exclude the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="Wov1tNDo" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
         "Sid": "test3",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "3000",
           "ReadsRate": ""
         },
         "Principal": [
           "*"
         ],
         "NotResource": "trn:tos:::bucketevent/*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="8e24cd73"></span>
## Prioritizing bandwidth for a specific user

In this section, we will use the IAM user "aaa" and the China (Beijing) region as an example. The default write bandwidth limit for this region is 10,000 Mbps. To ensure aaa has a write bandwidth limit of 7,000 Mbps while the other users collectively have a limit of 3,000 Mbps in this region, we will set the limit for the other users to 3,000 Mbps.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="LBxQVBQr" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter test4.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 3,000.
   
         * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Sub account name** section, click **Add row** and select **aaa** from the list.
   
         * User Policy: Select **Exclude the above users**.
   
         * Resource: Select **All buckets**.
   
         * Resource strategy: Select **Include the above resources**.
   
         * Condition: No conditions are required for this scenario.
   
      3. After completing the settings, click **Next step**.
   
      4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="qSAwGjZb" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
         "Sid": "test4",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "3000",
           "ReadsRate": ""
         },
         "NotPrincipal": [
           "trn:iam::214748****:user/aaa"
         ],
         "Resource": "*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="eErA0lLq"></span>
## Implementing priority‑based throttling for various services accessing the same TOS resources

In this section, we will set the guaranteed write bandwidth quotas to 1,000 Mbps for vePFS and 2,000 Mbps for EMR when accessing the "bucketevent" bucket. The total write bandwidth quota is 3,000 Mbps.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="Dx59UcVBcE" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter "test\-priority1".
   
         * Policy type: Select **Priority traffic control**.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 3,000 Mbps.
   
         * Priority configuration: Click **Add priority** to set the guaranteed bandwidth quota and priority level for vePFS.
   
            * Guaranteed flow control value: Set **Category** to **WritesRate**, and **Value** to 1,000 Mbps.
   
            * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Role name** section, click **Add row** to apply **ServiceRoleForVEPFS**.
   
            * User Policy: Select **Include the above users**.
   
            * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent and **Scope of application** to **All objects**.
   
            * Resource strategy: Select **Include the above resources**.
   
            * Condition: No conditions are required for this scenario.
   
            * After verifying the details, click **Confirm**.
   
         * Priority configuration: Click **Add priority** to set the guaranteed bandwidth quota and priority level for EMR.
   
            * Guaranteed flow control value: Set **Category** to **WritesRate**, and **Value** to 2,000 Mbps.
   
            * Authorized user: Set **Authorized user** to **Specified account** and select **Current main account**. In the **Role name** section, click **Add row** to apply **ServiceRoleForEMROLAP**.
   
            * User Policy: Select **Include the above users**.
   
            * Resource: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent and **Scope of application** to **All objects**.
   
            * Resource strategy: Select **Include the above resources**.
   
            * Condition: No conditions are required for this scenario.
   
            * After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="XJoRLKWOGG" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
     "Sid": "test-priority1",
     "Quota": {
       "WritesRate": "3000"
     },
     "Priority": [
       {
         "PriorityLevel": 1,
         "GuaranteedQuota": {
           "WritesRate": "1000"
         },
         "Principal": [
           "trn:iam::2147489060:role/ServiceRoleForVePFS"
         ],
         "Resource": "trn:tos:::bucketevent/*"
       },
       {
         "PriorityLevel": 2,
         "GuaranteedQuota": {
           "WritesRate": "2000"
         },
         "Principal": [
           "trn:iam::2147489060:role/ServiceRoleForEMROLAP"
         ],
         "Resource": "trn:tos:::bucketevent/*"
       }
     ],
     "Condition": {}
   }
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. After completing the settings, click **Next step**.

6. After verifying the details, click **Confirm**.


<span id="M3pP9dXm"></span>
## Implementing priority‑based throttling across multiple buckets

In this section, we will use the "bucketevent1" and "bucketevent2" buckets in China (Beijing) as examples. The default write bandwidth limit for this region is 10,000 Mbps. We will set guaranteed write bandwidth quotas of 3,000 Mbps for both "bucketevent1" and "bucketevent2".


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. On the **QoS policy management** page, set **Region** to **China (Beijing)**  in the upper\-left corner.

4. Configure the policy using your preferred view.

   
   <Tabs>
   <Tab zoneid="oMNcZEFXVA" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
      1. Click **Create policy**.
   
      2. On the **Create QoS policy** page, set the following parameters.
   
         * Policy configuration method: Select **Visual view**.
   
         * Policy name: Enter a name for the policy. In this example, enter "test\-priority2".
   
         * Policy type: Select **Priority traffic control**.
   
         * QoS value: Set **Category** to **WritesRate**, and **Value** to 10,000 Mbps.
   
         * Priority configuration: Click **Add priority** to set the guaranteed bandwidth quota and priority level for bucketevent1.
   
            * Guaranteed flow control value: Set **Category** to **WritesRate**, and **Value** to 3,000 Mbps.
   
            * Authorized user: Select **All users**.
   
            * User Policy: Select **Include the above users**.
   
            * Resource scope: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent1 and **Scope of application** to **All objects**.
   
            * Resource strategy: Select **Include the above resources**.
   
            * Condition: No conditions are required for this scenario.
   
            * After verifying the details, click **Confirm**.
   
         * Priority configuration: Click **Add priority** to set the guaranteed bandwidth quota and priority level for bucketevent2.
   
            * Guaranteed flow control value: Set **Category** to **WritesRate**, and **Value** to 3,000 Mbps.
   
            * Authorized user: Select **All users**.
   
            * User Policy: Select **Include the above users**.
   
            * Resource scope: Check the **Objects in bucket** checkbox. Set **Bucket** name to bucketevent2 and **Scope of application** to **All objects**.
   
            * Resource strategy: Select **Include the above resources**.
   
            * Condition: No conditions are required for this scenario.
   
            * After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="eV9CbuvPXT" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   On the **JSON view** tab, click **Edit**. Then, copy the following content into the `Statement`, and click **Save**.
   
   ```JSON
   {
     "Sid": "test-priority2",
     "Quota": {
       "WritesRate": "10000"
     },
     "Priority": [
       {
         "PriorityLevel": 1,
         "GuaranteedQuota": {
           "WritesRate": "3000"
         },
         "Principal": [
           "*"
         ],
         "Resource": "trn:tos:::bucketevent1/*"
       },
       {
         "PriorityLevel": 2,
         "GuaranteedQuota": {
           "WritesRate": "3000"
         },
         "Principal": [
           "*"
         ],
         "Resource": "trn:tos:::bucketevent2/*"
       }
     ],
     "Condition": {}
   }
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. After completing the settings, click **Next step**.

6. After verifying the details, click **Confirm**.
