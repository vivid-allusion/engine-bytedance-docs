---
title: "Automated office capabilities of cloud PC"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Automated_office_capabilities_of_cloud_PC_"
---

Cloud PC has built\-in automated office capabilities. Simply enter natural language instructions or specific data in the dialog box, and ArkClaw will automatically generate, process, and format Excel spreadsheets or Word documents for you.

<span id="d2nkjdb2"></span>
## Usage notes

The office capabilities of the cloud PC are fully instruction\-driven. Please note the following characteristics during use:


* **Interface\-free instruction execution**: Tasks are processed automatically in the background. You can view the real\-time processing progress in the dialog box. No traditional graphical office software interface (such as Word or WPS) will be displayed, and file creation and editing are performed via natural language instructions.

* **File saving and retrieval**: Generated files are saved in `/root/.cua/runs/output` by default. You can explicitly specify in your instruction to save the file to your cloud PC desktop or send it to you. You may then download it to your local device for viewing or manual editing.

* **Visual document preview**: To directly double\-click and preview files on the cloud PC desktop, you need to manually download and install the relevant office software (such as WPS) in the **cloud PC**.

* **Continuous interaction and editing**: For generated files, you can send instructions to specify modification requirements. ArkClaw will help you complete advanced operations such as content modification, merging, supplementation, or formatting.


<span id="yBLeLh1E"></span>
## (Optional) Install office dependencies

If you are using an ArkClaw instance created **before April 16, 2026**, perform the following steps to manually install the office dependencies before you can use this feature.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14bf1170d6737ad509cbe2af73342712.png) </span> and the "View terminal" button to access the terminal.

4. Execute the following command to install office dependencies.

   ```Bash
   curl -fsSL https://cua-prd.tos-cn-beijing.volces.com/setup-cua.sh | bash
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9108060733662103eb16747fbeb7e536.png) </span>

   If the following information is displayed, the office dependency installation succeeds.

5. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8726595f9b3415ecb5ad24c1a79e2062.png) </span>or press Enter to refresh the ArkClaw page to enable and experience the office capabilities of the cloud PC.


<span id="QNiqqaAv"></span>
## Usage examples

This section provides sample prompts for common scenarios for your reference during actual use.

<span id="6Ddw4AQm"></span>
### Create an Excel report with specified formulas and style

You can ask ArkClaw to generate complex spreadsheets with specific data, automated formulas, and custom styles.


* **Sample prompt:** 

   Use CUA: Create an annual sales report in Excel format named `annual_sales.xlsx`, with the following requirements:

   [Sheet1 \- Sales data]

   1. Headers (A1:F1): "Zone", "Product", "Q1 sales", "Q2 sales", "Q3 sales", and "Total annual sales". Bold the headers and set a background color.

   2. Data rows (rows 2\-5): 2 zones (China (Shanghai), China (Beijing)). Each zone has 2 products (laptop, mobile phone), with 4 rows of data in total. Fill in reasonable values for the quarterly sales.

   3. Formula for column F: Calculate the total annual sales for each row using the SUM formula: =SUM(C:E).

   4. Summary row (row 7): Calculate quarterly and total annual sales using the SUM formula. Apply bold formatting and a light background color.

   [Final verification]

   Confirm that the file has been generated in the current directory, and check formulas and cells.


<span id="pLcoHUD2"></span>
### Create and format a Word document

Send instructions to ArkClaw to create content for you and save it as a standard Word document.


* **Sample prompt:** 

   1. Use CUA to randomly generate a short story file named `new.docx`.

   2. After successful execution, log in to the IM client (such as Lark), and send the `new.docx` file from the desktop to me.

      > Before using the IM client, make sure that you have [configured the message channel](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__) for ArkClaw.      
      

&nbsp;


&nbsp;
