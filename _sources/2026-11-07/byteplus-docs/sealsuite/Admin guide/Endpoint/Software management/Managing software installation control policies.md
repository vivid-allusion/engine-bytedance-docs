---
title: "Managing software installation control policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-software-installation-control-policies"
---

Software installation control policies enforce compliance, security, and resource efficiency by specifying which software is permitted or prohibited on enterprise endpoints. If an employee attempts to install prohibited software, SealSuite blocks the action and generates an audit log.

<span id="1a0a34c3"></span>
# Notes


* Supported installation packages: MSI, EXE, DMG, and PKG.

* **macOS Full Disk Access**: Enforcing installation controls on macOS requires **Full Disk Access**. Devices lacking this permission receive a mandatory authorization prompt. Evaluate the impact scope before activation. Permissions are granted silently if the enterprise uses MDM with pre\-installed configuration profiles.


<span id="69901784"></span>
# Add a software installation control policy


1. Log in to the **Admin Console**.

2. In the left navigation bar, select **Endpoint** \> **Software** \> **Installation Control**.

3. On the **Installation Control** page, click **Policy Management**.

   \*If using this feature for the first time, click \****Getting Started*** *and then* ***Configure*** *in the dialog.* 

4. Click  **+ New Strategy** and configure the following:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy Name** |A unique identifier for the policy. Supports alphanumeric characters, spaces, and symbols (max 64 characters). |
   |**Priority** |Defines the evaluation order (0–100; higher values take precedence).<br><br>Multiple policies can be active simultaneously. SealSuite matches policies in descending order of priority and stops once a match is found. If no match is found after checking all policies, the detection cycle ends.<br><br>If two policies share the same priority, the one with the latest modification time takes precedence. |
   |**Control Action** |Defines the enforcement behavior for the specified software:<br><br><br>* **Forbid**: Blocks installation and automatically reports audit logs.<br><br>* **Allow**: Permits installation. You can toggle **Whether to keep audit logs** to capture software metadata for future "Add from Audit" operations. |
   |**ControlSoftware** |Choose to control **All** or **Part** software.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To identify specific software, see <a href="https://docs.byteplus.com/docs/sealsuite/managing-software-installation-control-policies#85975aff">Obtain software information</a>.</div><br><br><br>For **Part** control, select **Windows** or **macOS** and click  **+ Add Software** using one of these methods:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d005f82ec46e42409aeba0f1c7f99bd0~tplv-goo7wpa0wc-image.image) </span><br><br><br>* **Add manually**: Manually enter software attributes.<br><br>* **Add from audit**: Quickly add software detected in previous installation logs.<br><br>* **Import from local**: Download the template, populate software data, and upload the file.<br><br><br>**Advanced Rule Matching**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1d866744abe4f63890bf978b3a94a5b~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. Enable **Advanced settings**.<br><br>2. Click  **+ Add Condition** and select the OS.<br><br>3. Click  **+ Add Rule** to define criteria using operators and values (regex supported).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Combine multiple rules using <strong>AND</strong> or <strong>OR</strong> logic. Supported operators:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Contains/Does not contain</strong>: Fuzzy matching (e.g., <code>Contains Adobe</code> matches Adobe Photoshop and Adobe Illustrator).</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Matches/Does not match</strong>: Exact or regex matching (e.g., <code>Matches Adobe *</code>).</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Belongs to/Does not belong to</strong>: Set\-based matching (e.g., <code>Belongs to Adobe Photoshop, Adobe Illustrator</code>).</div><br> |
   |**Notification** |Toggle desktop alerts. When active, the SealSuite client displays a pop\-up if a prohibited installation is blocked. Click **Modify Configuration** to preview or edit the notification.<br><br><br>* **Chinese**: Title (max 40 chars), Content (max 200 chars).<br><br>* **English**: Title (max 100 chars), Content (max 500 chars).<br><br><br>**Note**: Update all language variants simultaneously to ensure consistency. |
   |**Scope** |Defines the policy scope by **Employee** or **Device**:<br><br><br>* **Employee**: Scope by **Department** or **Role**.<br><br>* **Device**: Scope by **Device**, **Operating System**, or **Group**.<br><br><br>Use **Exclude Object** to refine the scope. The final effective range is **Target Object \- Exclude Object**.<br><br>To bypass controls for specific entities, click **Go to Configure** to manage the **Global Whitelist** for the **Software Installation Control** module. See [Configuring global allowlist](https://docs.byteplus.com/docs/sealsuite/docs-configuring-global-allowlist). |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Default Policy</strong>: SealSuite includes a built\-in policy allowing all software installations.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Library/Distribution Overrides</strong>: Software explicitly added to the <strong>Software Library</strong> or <strong>Software Distribution</strong> is always allowed, overriding any installation control policies.   </div>
   


<span id="85975aff"></span>
# Obtain software information

Accurate software metadata is required when configuring installation controls. Use the following methods to retrieve this data:


1. In the **Control Software** section of the policy page, click **Configuration Instructions**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c192708cc3641eebfba068ae7b5d9d0~tplv-goo7wpa0wc-image.image) </span>

2. Choose a retrieval method:

   * **Method 1: Import directly from the audit log**

      Configure the system to audit target installation packages. Once detected, select the software directly from the audit logs.

   * **Method 2: Get it through a client side widget**

      Download the `installer_parser_windows.exe` or `installer_parser_mac` utility from the Admin Console.

3. Run the parsing tool locally to extract package details:

   * **Windows**

      1. Download `installer_parser_windows.exe`.

      2. Open a command prompt (`cmd.exe`) and navigate to the tool's directory.

      3. Run: `installer_parser_windows.exe <package_path>`

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Supports absolute or relative paths.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Avoid Chinese characters in paths/filenames.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Wrap paths containing spaces in double quotes.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Supports EXE and MSI formats.      </div>
      

   * **macOS**

      1. Download `installer_parser_mac`.

      2. Open Terminal and navigate to the tool's directory.

      3. Run: `xattr -d com.apple.quarantine ./installer_parser_mac && chmod +x ./installer_parser_mac`

      4. Run: `./installer_parser_mac <package_path>`

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Wrap paths containing spaces in double quotes.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Supports PKG and DMG formats.      </div>
      


<span id="3ed05a56"></span>
# Manage installation control policies


1. Log in to the **Admin Console**.

2. Select **Endpoint** \> **Software** \> **Installation Control** \> **Policy Management**.

3. Perform the following management tasks:

   * **Filter and Sort**: Search for policies or sort them by priority or edit time.

   * **Enable/Disable**: Toggle the switch to activate or deactivate enforcement for the specified scope.

   * **Copy/Edit/Delete**: Use the actions on the right to manage existing policies.

      * **Caution**: Deleted policies cannot be recovered. SealSuite stops enforcement for all software defined in the deleted policy.


<span id="4de4a427"></span>
# View installation package audit logs


1. Log in to the **Admin Console**.

2. Select **Endpoint** \> **Software** \> **Installation Control** \> **Installation Package To Perform Audit**.

3. Select the **Windows** or **macOS** tab to view execution logs.

4. Use the following log management features:

   * **Search**: Filter logs by user, department, device status, or OS. Use **Custom Filter** for advanced criteria.

   * **Export**: Click **Export List** to download logs as a `.csv` file.

   * **Inspect Details**:

      * Hover over **Employee** or **Device Info** for granular entity details.

      * Click the **Hit Policy** to view the specific control configuration.

      * Review the **Blocking Result** (e.g., Blocked/Allowed).

      * Inspect software metadata, including filename, MD5 hash, and directory path.
