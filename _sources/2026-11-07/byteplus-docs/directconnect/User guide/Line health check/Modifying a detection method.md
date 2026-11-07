---
title: "Modifying a detection method"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Modifying_a_detection_method"
---

<span id=".5pON5L2c6IOM5pmv"></span>
## Background

You can configure a detection method for the Direct Connect (DC) Virtual Interface, such as Bidirectional Forwarding Detection (BFD) or Network Quality Analyzer (NQA), and adjust the Detect Interval and Detect Multiplier for BFD and NQA at any time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select the region where the target Virtual Interface is deployed.

3. In the Virtual Interface list, click the name of the target Virtual Interface.

4. Click **Modify** at the end of **Detection method**.

5. In the pop\-up dialog box, configure the detection method based on the table below.

   
   |Parameter |Description |
   |---|---|
   |Detection method |* Disable: Do not enable line detection.<br><br>* BFD: Enable BFD as the detection method.<br><br>* NQA: Enable NQA as the detection method.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager. For details of BFD and NQA, see <a href="https://docs.byteplus.com/en/docs/directconnect/Detection_methods">Detection methods</a>.</div><br> |
   |BFD mode |Configure this parameter only when selecting BFD as the detection method.<br><br><br>* BFD control packet: Send BFD control packets to detect bidirectional path reachability between network devices. The data center must establish a BFD session and exchange packets.<br><br>* BFD echo packet: BytePlus sends BFD echo packets, and the data center returns them to quickly detect reachability between network devices. The data center only forwards echo packets.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The BFD echo packet feature is in the beta stage. If you need a trial, please contact your account manager.   </div><br>    |
   |Detect interval |Set the detect interval, including the sending and receiving intervals of probe packets. |
   |Detect multiplier |Set a number for detection attempts. If a session fails to receive the defined number of consecutive packets, the system declares a route failure. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When using static routing, you can enable either BFD or NQA for detection, but not both simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If active routes exist, enabling BFD may cause flash disruption and packet loss in seconds.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Switching between BFD and NQA may cause brief traffic interruptions. Carefully assess the impact on services before proceeding.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When modifying the detection method to BFD control packet, confirm that the gateway device of the on\-premises data center supports BFD. Modify the detection method for the data center's gateway to BFD simultaneously, and configure the detect interval and detect multiplier identically.   </div>
   

6. Click **Save** to complete the action.

   After modifying the detection method for the Virtual Interface to BFD control packet, update the data center's configuration accordingly. For specific configurations, see [Connecting an on-premises data center to a VPC via dual Direct Connects with BGP routes (load redundancy)](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-5#.5q2l6aqk5YWt77ya6YWN572u5pys5Zyw6Lev55Sx5ZKMQkZE).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you modify the NQA configuration on a Virtual Interface where NQA is already enabled, the following may occur during the transition period before the new configuration takes effect:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Healthy link</strong>: During this period, the routes associated with NQA temporarily lose NQA protection.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Faulty link</strong>: During this period, the invalidated routes associated with NQA may briefly become effective again, directing outbound traffic from the cloud to the faulty link. Therefore, we do not recommend modifying NQA parameters during link faults.   </div>
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectVirtualInterfaceAttributes): Modify the name, description, NQA, and other configurations of a specified Virtual Interface.
