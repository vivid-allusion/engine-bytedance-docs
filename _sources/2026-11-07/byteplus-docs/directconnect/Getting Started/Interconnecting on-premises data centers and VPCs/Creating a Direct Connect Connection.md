---
title: "Creating a Direct Connect Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection"
---

This topic describes how to establish a dedicated Direct Connect (DC) connection.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin

Complete the access point selection, onsite survey and other preparations. For procedure, see [Preparations before access](https://docs.byteplus.com/en/docs/directconnect/Preparation-for-access).

<span id=".5q2l6aqk5LiA77ya55Sz6K-35o6l5YWl54mp55CG5LiT57q_"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya55Sz6K-35o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create DC Connection


1. Log in to the [DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select a target region and project.

3. Click **Create DC Connection**.

4. Configure the DC Connection port based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Access point mode |Select classic mode to create one access point in a single request. |Classic |
   |Region |Select the access point region of the DC Connection. |China (Beijing) |
   |Name |Enter a name for the DC Connection. |DAS123_port308_conn |
   |Access point |Select an access point for the DC Connection. |Beijing\-Chaoyang\-A |
   |Line operator |Select the type of Line Operator who constructs your DC connection. |China Mobile |
   |Port speed |Select a port specification. Different specifications charge different port fees. Apply based on actual needs. |1G |
   |Port type |Port Type supports the optical port. Port Spec determines the port rate. BytePlus access point devices support single\-mode optical ports with specifications of 1Gbps, 10Gbps, 40Gbps, and 100Gbps.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only Beijing\-Langfang\-C access point supports the 400Gbps optical port in DC connections with classic mode. If needed, please contact your account manager.</div><br> |1G optical port |
   |Affiliated project |The project to which the new DC connection belongs. |default |
   |Billing rules |View and confirm the DC Connection billing rules. |Check |
   

   This example demonstrates only sample values for required parameters. For more parameter details, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1). Sample values are for reference only and have no practical significance.

5. After configuration, click **Buy now** to submit the application.


<span id=".5q2l6aqk5LqM77ya55Sz6K-3TE9B"></span>
### Step 2: Apply for LOA

LOA is a letter of authorization for the DC Connection construction in the BytePlus access point data center. After the DC Connection application is approved, the status of DC Connection becomes **LOA pending**. Go to the BytePlus DC Connection console to apply for the LOA.


1. Log in to the [DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select China (Beijing).

3. In the DC Connection list, click **Apply for LOA** to the right of the DC connection (DAS123_port308_conn), and configure the LOA application based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Company name |Enter the name of the company who uses the DC Connection. |ByteDance |
   |Construction Company entering BytePlus Data Center |Enter the name of the construction company |BytePlus |
   |Line type |Select a type for the DC Connection. |MSTP |
   |Construction schedule |Select the expected construction schedule. |2023\-06\-30 |
   |IDC location |Enter the detailed address of the data center. |Room XX, XX Building, No. XX, XX Road, Chaoyang District, Beijing, China |
   |Bandwidth |Enter the bandwidth of the DC Connection purchased from the Line Operator. |1,000 Mbps |
   |Field Engineer |Enter names, contact information, and ID numbers of engineers for DC connection construction. |Wang \*\*, 151\*\*\*\*0086, Mainland China ID, 22222219990101\*\*\*\* |
   

4. Click **Submit** to complete the application submission and wait for LOA review.


<span id=".5q2l6aqk5LiJ77ya54mp55CG5LiT57q_5pa95bel"></span>
### Step 3: Construction by Line Operator


1. After the LOA application is approved, the DC Connection status becomes **Line operator construction**. Click **Download LOA** in the **Actions ** column to the right of the target DC Connection to obtain the LOA for on\-site construction.

2. You should take the LOA with you, and contact the Line Operator to construct the DC connection in the BytePlus access point data center.


<span id=".5q2l6aqk5Zub77ya5a6M5bel5oql56uj"></span>
### Step 4: Report completion

After the Line Operator completes the construction and you finalize the completion by testing the DC Connection link connectivity, you need to access the BytePlus DC Connection console to report the completion.


1. Log in to the [DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select China (Beijing).

3. In the DC Connection list, click **Completion report** in the **Actions** column to the right of DAS123_port308_conn.

4. After confirming the information about the DC Connection to report, enter the Building Cable ID of the DC access point's data center.

5. Click **Submit**.


To this point, the status of DAS123_port308_conn changes to **BytePlus construction**.

<span id="ttZK24XM"></span>
### Step 5: Construction by BytePlus

After the completion report is submitted, BytePlus engineers will perform patch cord installation and check optical attenuation for your DC Connection. You will receive a notification via onsite message and SMS once the construction is complete. Wait patiently.

<span id=".5q2l6aqk5LqU77ya5pSv5LuY56uv5Y-j5Y2g55So6LS5"></span>
### Step 6: Pay port occupancy fee


1. Log in to the [DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select China (Beijing).

3. In the DC Connection list, click **Pay now** in the **Actions** column to the right of DAS123_port308_conn.

4. Follow the guidance to complete the payment. After payment, the status of DAS123_port308_conn becomes **Opened**.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create DC Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway)

* [Create Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface)

* [Attach network instance](https://docs.byteplus.com/en/docs/directconnect/Loading-a-network-instance)

* [Configure on-premise routing and test connectivity](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity)
