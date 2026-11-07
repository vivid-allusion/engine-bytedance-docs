---
title: "Configuring Process Running Control Policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/process-running-control"
---

Process running control allows you to intercept the startup of specific processes on the operating system. Use this to manage portable software, built\-in Windows processes (e.g., `mstsc`), and other unauthorized applications. Fine\-grained process management ensures efficient and secure allocation of computer system resources.

<span id="add-a-process-running-control-policy"></span>
## Add a process running control policy

<span id="create-a-policy-and-configure-basic-information"></span>
### Create a policy and configure basic information


1. Log in to the **Admin Console**.

2. In the left navigation bar, select **Endpoint** \> **Software** \> **Process Control**.

3. On the **Policy Management** tab, click  **+ Create Policy**.

4. Configure the **Basic Information**:

   * **Policy Name**: Enter a unique identifier for the policy.

   * **Priority**: Set the policy priority (0–100; higher values take precedence). If multiple policies apply, the system matches them in descending order of priority. The highest\-priority match takes effect immediately, and further matching stops. If two policies share the same priority, the one with the most recent modification time takes precedence.


<span id="configure-control-processes"></span>
### Configure control processes

Define the processes to be intercepted on the **Add Policy** page.


1. In the **Control Process** area, select a process source: **Built\-in Software Library**, **Software Statistics Reference**, or **Custom Software Process**.

> Clients on macOS require **Full Disk Access** once the interception policy is active. Unauthorized devices receive a mandatory authorization prompt. If the enterprise uses MDM and the device supports configuration profiles, the system enables this permission automatically.



|**Process Source** |**Description** |
|---|---|
|**Built\-in Software Library** |Select common software pre\-integrated with SealSuite.<br><br>1. Click  **+ Select Software** to open the **Built\-in Software Library**.<br><br>2. Filter by **All**, **Windows**, or **macOS**, or search by software name.<br><br>3. Click **Add** in the **Action** column or select multiple items and click **Confirm**. |
|**Software Statistics Reference** |Reference software from data already reported by enterprise endpoints.<br><br>1. Click  **+ Select Software** to open **Software Statistics Reference**.<br><br>2. Filter by **All**, **Windows**, or **macOS**, or search by **Software Name** or **Bundle ID / Publisher**.<br><br>3. Click **Add** in the **Action** column or select multiple items and click **Confirm**. |
|**Custom Software Process** |Define processes using custom rules if the software is not in the library or statistics.<br><br>1. Click  **+ Select Process** to open the **Process Library**.<br><br>2. Click  **+ New Process**. To batch import data, click **Import** and choose:<br><br>**Local Import**: Download the template, edit the process data (up to 10,000 entries), and upload the file.<br><br>**Quote from Baseline**: Select process groups from **Endpoint Control** \> **Endpoint Baseline** \> **Detection Item Configuration** \> **Process Detection Item**. The system references each process in the group independently.<br><br>3. Complete the configuration on the **New Process** page and click **Confirm**.<br><br>For details on process information and the Windows parsing tool, see [Obtain Detailed Process Information](https://docs.byteplus.com/en/docs/31/120472#retrieve-detailed-process-information).<br><br>**Rule Name**: Enter a name to identify the rule.<br><br>**Operating System**: Select **Windows, macOS**, or **Linux**.<br><br>**Add Rule**: Define rules using **Process Name**, **File Digital Signature**, **Process Path**, or **Command Line Parameters**. Multiple rules use an **AND** relationship. Supported operators:<br><br>**Contains**: Fuzzy match (e.g., `demo.exe` matches `1-demo.exe`).<br><br>**Belongs to**: Exact match.<br><br>**Regex** (Command line parameters only): Match using regular expressions (e.g., `^setup\.exe\s+/silent.*$` matches `setup.exe /silent /force`).<br><br>Enter multiple values separated by commas.<br><br>4. Select the target process in the **Process Library** and click **Confirm**.<br><br>5. (Optional) Edit or delete newly created processes in the **Process Library**. Edits sync to all referencing policies. Processes bound to active policies (e.g., software control, terminal firewall) cannot be deleted. |



2. To remove a process, click **Remove** in the list or check multiple items and click **Batch Remove**.


<span id="configure-notifications-and-target-objects"></span>
### Configure notifications and target objects


1. In the **Notify** area, toggle the alert for blocked processes.

2. (Optional) Click **Edit Notification Template** to preview or edit the default notification content.

3. In the **Scope** area, define the scope by **Employee** or **Device**.

   * View selected objects on the right.

   * To bypass controls for specific entities, add them to the **Process Running Control** whitelist. See [Configuring global allowlist](https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-global-allowlist).

   * **Deployment Tip**: For initial rollout, target a small group (e.g., IT or Security) to verify policy behavior before expanding the scope.

4. (Optional) Configure **Excluded Objects** to refine the scope. The final effective range is **Target Object** minus **Excluded Objects**.


<span id="retrieve-detailed-process-information"></span>
## Retrieve detailed process information

Accurate metadata (e.g., **Process Name**, **File Digital Signature**, **Process Path**) is required when creating or importing processes.

<span id="windows"></span>
### Windows

<span id="retrieve-info-via-task-manager"></span>
#### Retrieve info via Task Manager

Retrieve the **Process Name**, **File Digital Signature**, **File Description**, **File Version**, **Product Name**, **Product Version**, **Original Filename**, and **Process Path**:


1. Open **Task Manager**.

2. Locate the path in the **Details** tab (**Process Path**).

3. Right\-click the process and select **Properties**:

   * **General**: Retrieve the **Process Name**.

   * **Digital Signatures**: Retrieve the **File Digital Signature**.

   * **Details**: Retrieve the **File Description**, **File Version**, **Product Name**, **Product Version**, and **Original Filename**.


<span id="retrieve-info-via-windows-parsing-tool"></span>
#### Retrieve info via Windows parsing tool

Download the parsing tool from the **New Process** page in the Admin Console to retrieve the **Company Name**, **Internal Name**, **Product Code**, **Product Name**, or **Product Version**.


|**Tool** |**Description** |
|---|---|
|**Resource hacker (.exe)**  |Retrieves metadata for `.exe` files, including **CompanyName**, **InternalName**, **OriginalFilename**, **ProductName**, and **ProductVersion**. |
|**InstEd (.msi)**  |Retrieves metadata for `.msi` files, including **ProductCode**, **ProductName**, and **ProductVersion**. |


<span id="macos"></span>
### macOS

<span id="retrieve-software-name-digital-signature-and-path"></span>
#### Retrieve software name, digital signature, and path

Adding software info to a policy disables all associated executable files once the policy is active.


1. Install the target software package.

2. Retrieve the path:

   1. In **Finder**, select **View** \> **Show Path Bar**.

   2. Locate the package, right\-click the path bar at the bottom, and copy the path.

   Example: Safari's path is `/Applications/Safari.app`; the name is `Safari.app`.

3. Retrieve the digital signature:

   1. Open **Terminal**.

   2. Run: `codesign -dvv <Software_Path> 2>&1 | grep "Authority=" | head -n 1 | cut -d = -f2`

      * Example: `codesign -dvv /Applications/Safari.app 2>&1 | grep "Authority=" | head -n 1 | cut -d = -f2`

      * Result: `Software Signing`.


<span id="retrieve-process-name-digital-signature-and-path"></span>
#### Retrieve process name, digital signature, and path

For running processes, use the PID to retrieve details:


1. Open **Activity Monitor** and locate the process **PID**.

2. Open **Terminal**.

3. Run: `ps -p <PID>`

   * Example: `ps -p 79494` returns the path `/System/Volumes/Preboot/Cryptexes/App/System/Applications/Safari.app/Contents/MacOS/Safari`; the process name is `Safari`.

4. Retrieve the digital signature:

   * Run: `codesign -dvv <Process_Path> 2>&1 | grep "Authority=" | head -n 1 | cut -d = -f2`

   * Example: `codesign -dvv /System/Volumes/Preboot/.../Safari 2>&1 | grep "Authority=" | head -n 1 | cut -d = -f2`

   * Result: `Software Signing`.


<span id="linux"></span>
### Linux

<span id="retrieve-process-name-path-and-startup-parameters"></span>
#### Retrieve process name, path, and startup parameters

For running processes, use the PID to retrieve details:


1. Open **Terminal**.

2. Identify the target process `PID`:

   ```shell
   ps -ef | grep <process_keyword>
   ```
   

   Example: `ps -ef | grep python`

3. Retrieve the process name:

   ```shell
   cat /proc/<PID>/comm
   ```
   

   If the command returns `python3`, enter `python3` as the **Process Name** in the policy.

4. Retrieve the process path:

   ```shell
   readlink -f /proc/<PID>/exe
   ```
   

   If the command returns `/usr/bin/python3`, enter `/usr/bin/python3` as the **Process Path** in the policy.

5. Retrieve startup parameters:

   ```shell
   tr '\0' ' ' < /proc/<PID>/cmdline
   ```
   

   Example output: `python3 /opt/demo/app.py --port 8080 --env prod`.

   Enter the full command or stable fragments (e.g., `--port 8080`) as **Startup Parameters** based on your requirements.


<span id="manage-process-control-policies"></span>
## Manage process control policies


1. Log in to the **Admin Console**.

2. Select **Endpoint** \> **Software** \> **Process Control** \> **Policy Management**.

3. Supported actions:

   * **Filter**: Search for policies by name, employee, or device.

   * **Adjust**: Directly update the **Priority** or **Status** (Enabled/Disabled) in the list.

   * **Actions**: **Copy**, **Edit**, or **Delete** policies.

      * **Caution**: Deleted policies cannot be recovered.


<span id="view-process-running-control-events"></span>
## View process running control events

SealSuite monitors processes in real\-time. Blocked or hit events are reported to the **Event List** tab under **Software** \> **Process Control**.


* Filter events by specific criteria.

* Export the event list to a local file.

* Inspect event details: **Report Time**, **User Info**, **Device Info**, **Policy Name**, and **Process Name**.


<span id="faq"></span>
## FAQ

<span id="what-are-the-priorities-between-process-control-endpoint-baseline-and-software-licenses"></span>
#### What are the priorities between process control, endpoint baseline, and software licenses?


* **Endpoint Baseline vs. Process Control**:

   * If a process is flagged for **Prohibited Process** detection in a baseline and also exists in a process control policy, the **Process Control Policy** takes precedence. The system intercepts the process and reports an interception log; the baseline does not report a violation.

   * If a process is flagged for **Required Process** detection in a baseline and is also blocked by a process control policy, the **Process Control Policy** takes precedence. The system intercepts the process and reports an interception log, while the baseline reports that the required process is not running.

* **Software License vs. Process Control**:

   If a process is both disabled via a software license and blocked by a process control policy, the **Process Control Policy** takes precedence.
