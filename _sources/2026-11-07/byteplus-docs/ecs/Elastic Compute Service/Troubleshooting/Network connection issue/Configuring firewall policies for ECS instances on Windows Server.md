---
title: "Configuring firewall policies for ECS instances on Windows Server"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuration_method_for_firewall_policies_on_ECS_instances_with_Windows_Server_system"
---

This topic describes how to configure the firewall in Windows Server. In this example, Windows Server 2022 Datacenter is used.

> This topic may contain information about third\-party products, which is provided for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id=".5YWB6K6456iL5bqP5oiW5Yqf6IO96YCa6L-HV2luZG93c-mYsueBq-WimQ=="></span>
## Allow an app or feature through Windows Defender Firewall


1. [Use VNC to log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Select "Start \> Control Panel \> System and Security \> Windows Defender Firewall".

3. In the left directory tree, select "Allow an app or feature through Windows Defender Firewall".

4. Click the "Allow another app..." button.

5. On the page for adding apps, select the target app and click the "Add" button to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the app you want to allow is not listed in the app module, click the "Browse" button to locate and select the target application file in the file system.   </div>
   

<span id=".5YWB6K645oiW56aB5q2i54m55a6a5pys5Zyw56uv5Y-j6K6_6Zeu"></span>
## Allow or block access to specific local ports


1. [Use VNC to log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Select "Start \> Control Panel \> System and Security \> Windows Defender Firewall".

3. In the left directory tree, select "Advanced settings".

4. In the left directory tree, select "Inbound Rules" and click the "New Rule" button in the right "Actions" pane.

5. Select "Port" and click the "Next" button.

6. Configure the protocol type and port range for the current inbound rule based on your needs, and then click the "Next" button.

7. Specify the type of action to be taken when an inbound request matches the rules you configured, and click the "Next" button.

   
   |Parameter​ |Description |
   |---|---|
   |Allow the connection |Allow connections that match the conditions of this rule. In other words, permit access to the ports you configured. The firewall will not perform any authentication or security checks on the connections. |
   |Allow the connection if it is secure |Allow only connections authenticated and encrypted via IPsec. You can customize the secure connection rules. |
   |Block the connection |Reject and block connections that match the conditions of this rule. In other words, prohibit access to the ports you configured. Connection attempts will be discarded directly. |
   

8. Select the scope for the current rule and click the "Next" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, all scope options are selected. Select the scope based on the actual network environment.   </div>
   

9. After you enter the rule name, click the "Finish" button.


<span id=".6ZmQ5Yi2SVDlnLDlnYDnmoTorr_pl67mnYPpmZA="></span>
## Allow or block access from specific IP addresses


1. [Use VNC to log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Select "Start \> Control Panel \> System and Security \> Windows Defender Firewall".

3. In the left directory tree, select "Advanced settings".

4. In the left directory tree, select "Inbound Rules" and click the "New Rule" button in the right "Actions" pane.

5. Select "Custom", and click the "Next" button.

6. Select the applicable program scope for the current rule based on your needs, and click the "Next" button.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"All programs" indicates all programs on the local machine.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"This program path:" indicates a specific program.   </div>
   

7. Configure the ports and protocols to which the rule applies based on your needs, and click the "Next" button.

8. Select the scope for the current rule.

   1. Based on the target IP address type, select "These IP addresses" in the corresponding module (for example, select IP addresses in the "Which remote IP addresses does this rule apply to?" module when restricting external IP address access), and click the "Add" button.

   2. Configure the target IP address or CIDR block in the pop\-up window, and click the "OK" button.

   3. To add multiple IP addresses or CIDR blocks to be restricted, click the "Add" button again to complete the configuration.

   4. Click the "Next" button.

9. Specify the type of action to be taken when an inbound request matches the rules you configured, and click the "Next" button.

   
   |Parameter​ |Description |
   |---|---|
   |Allow the connection |Allow connections that match the conditions of this rule. In other words, permit the IP addresses you configured to access the programs, services, or ports specified by the rule. The firewall will not perform any authentication or security checks on such connections. |
   |Allow the connection if it is secure |Allow only connections authenticated and encrypted via IPsec. You can customize the secure connection rules. |
   |Block the connection |Reject and block connections that match the conditions of this rule. In other words, prohibit the IP addresses you configured from accessing the programs, services, or ports specified by the rule. Connection attempts will be discarded directly. |
   

10. Select the scope for the current rule and click the "Next" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, all scope options are selected. Select the scope based on the actual network environment.   </div>
   

11. After you enter the rule name, click the "Finish" button.
