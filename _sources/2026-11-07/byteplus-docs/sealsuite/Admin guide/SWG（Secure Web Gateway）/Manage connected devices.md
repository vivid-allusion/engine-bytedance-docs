---
title: "Manage connected devices"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/manage-connected-devices"
---

For day\-to\-day troubleshooting and handling special access needs in SealSuite's always\-on SWG environment, you need effective device management tools. This guide provides step\-by\-step instructions on how to use the Admin Console to monitor device connection status, forcibly disconnect a device, grant temporary bypass permissions, and trace connection issues using detailed logs.


|Control method |How it works |Typical use cases |Recovery mechanism |
|---|---|---|---|
|**Temporary bypass** |An administrator generates a temporary authorization code. The user enters the code on the client to gain time\-limited bypass permissions. |Emergency business access, client\-side network troubleshooting. |When the validity period ends, the system automatically restores control and re\-establishes the tunnel. |
|**Forced disconnect** |An administrator forcibly terminates the SWG tunnel connection for a specific endpoint from the Admin Console. |Severe network disruption on the user's device, SWG policy anomalies causing business interruption. |The administrator must manually perform "Restore online" from the Admin Console. |


<span id="f814b0e4"></span>
# Manage connected devices

<span id="392769ef"></span>
## View connected devices

Administrators can monitor the SWG runtime and connection status of endpoints in real time — including devices within the traffic routing policy scope and devices where employees have logged in.


1. Log in to the SealSuite Admin Console and go to **SWG** \> **Access Devices**.

2. In the connected devices list, you can view basic information for each device, including the associated employee, device name, connection node, and public/internal IP addresses. You can also use the filters above the list for combined queries. The following three key fields help you quickly assess an endpoint's secure access status:

   * **Connection status**: Indicates whether the SealSuite client has successfully established a network connection with an SWG node (Connected / Not connected).

   * **Certificate status**: Indicates whether the endpoint has successfully installed the corporate self\-signed root certificate (Installed / Not installed).

   * **Runtime status**: Provides an overall view of whether control is functioning properly on the endpoint. When a device is within the traffic routing scope but has not installed the corporate root certificate, the status shows **Abnormal** (in this state, the endpoint may fail to resolve HTTPS websites or experience false blocks). When the certificate is installed and traffic routing is in effect, the status shows **Normal**.


<span id="c35fb151"></span>
## Force disconnect and restore

When a user experiences severe network disruption or an SWG node has policy anomalies, administrators can forcibly terminate the tunnel connection. Note: Devices that are forcibly disconnected will not automatically reconnect.

<span id="681ddf6c"></span>
### Force disconnect


1. In the connected devices list, locate the target device.

2. Click **Force disconnect** in the Actions column, or select multiple devices and click **Batch offline** at the bottom left.

3. In the confirmation dialog, click **Take offline**.

4. Effects:

   * The SWG tunnel for the device is immediately disconnected, and all associated security policies stop working.

   * **User experience**: A popup appears on the client, notifying the user that "The secure internet channel has been paused by the administrator."

   * **Reconnection restriction**: A forcibly disconnected device **will not** trigger automatic reconnection until the administrator manually restores it.


<span id="8cf844b4"></span>
### Restore a device online

A forcibly disconnected device must be manually restored by an administrator before it can re\-establish the SWG connection.


1. Click **Forced Disconnect Logs** in the upper\-right corner of the connected devices page.

2. In the popup window, filter target records by employee, forced offline time, or device information.

3. Click **Restore online** in the Action column, or select multiple records and click **Batch restore** at the bottom left.

4. Effects: The device immediately receives the command and re\-establishes the SWG tunnel connection.


<span id="a458815b"></span>
## Temporary bypass management

When a user needs to briefly bypass SWG control (for example, to troubleshoot network issues or handle an urgent special task), an administrator can generate an authorization code that allows the user to temporarily disconnect from SWG. When the validity period ends, the system automatically restores control and re\-establishes the tunnel.

<span id="d403348d"></span>
### Get a bypass code


1. In the connected devices list, click **Temporary bypass** in the Actions column for the target device.

2. The system displays a **Code** popup showing an 8\-character temporary authorization code.

   * **Note**: The code is automatically refreshed every 60 minutes. Provide it to the user promptly.

3. The administrator shares the code with the user and instructs them to click **Remove protection** on the client SWG page and enter the code.

4. Effects:

   * After entering the code on the SealSuite client, the user can **manually disconnect, reconnect, or re\-establish** the SWG tunnel within the validity period.

   * **Automatic recovery**: When the bypass validity period ends, the code permissions expire automatically, and the system re\-establishes the SWG tunnel and restores security control.


<span id="262f4c92"></span>
### Manage bypassed devices

Administrators can centrally view devices currently in a "bypass" state, configure the validity period, or revoke access early.


1. Click **Bypass** in the upper\-right corner of the connected devices list page.

2. Click **Configure Temporary Access Validity** in the upper\-right corner of the popup, and enter the number of hours (1–48) the user is allowed to bypass control. When the validity period ends, the client automatically restores SWG control.

3. **Revoke bypass**: To end the bypass state early, locate the device in the popup list and click **Revoke bypass** in the Actions column. Revocation immediately withdraws the user's temporary permissions and forces the SWG tunnel to re\-establish.


<span id="54a2a291"></span>
# View employee SWG connection logs

To improve troubleshooting efficiency, SealSuite records complete SWG connection sessions for each employee. When an endpoint experiences issues such as web pages failing to load or policies not taking effect, administrators can trace the disconnection reason through connection logs.


1. On the **Access Devices** page, switch to the **Connection Log** tab.

2. The log list shows each complete connection session. Use the filter bar at the top for combined queries by employee name, service node, connect/disconnect time range, client version, operating system, and disconnection reason.

3. Click **View details** in the Actions column of a target log entry to view the session details in the right\-side drawer.

4. When a connection is disconnected, the log details display the specific **Disconnection reason**. The trigger scenarios for each disconnection event are described below:

   
   |Display label |Trigger scenario |Initiated by |
   |---|---|---|
   |**Portal authentication policy triggered** |A periodic Portal authentication policy was triggered, forcing the user to re\-authenticate and causing the disconnection. |System |
   |**Device not in traffic routing policy** |The administrator modified the policy, and the current device/user no longer matches any SWG traffic routing policy. The client actively or passively disconnects. |System |
   |**Client network unreachable** |The network connection between the client and the SWG node was lost, causing a heartbeat timeout (for example, the employee's computer went to sleep, lost its network connection, or switched Wi\-Fi). |Network environment |
   |**SWG node unavailable** |The connected SWG node experienced a crash, maintenance, or network jitter, causing the connection to drop. |SWG node |
   |**Forced disconnect from Admin Console** |The administrator performed a forced offline operation on the device from the Admin Console. |Administrator |
   |**Client temporary bypass** |The employee entered a temporary authorization code on the client to temporarily bypass SWG traffic routing, actively disconnecting for a period of time. |User / Employee |
   |**Client normal exit** |The employee's computer shut down or the SWG client process was forcibly terminated. |User / Employee |
