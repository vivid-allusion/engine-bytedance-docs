---
title: "Data identification overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/data-identification-overview"
---

Data identification is the foundation of the SealSuite Data Loss Prevention (DLP) system. By automatically scanning file attributes—including names, content, types, and origins—the system accurately assesses the sensitivity of corporate assets and assigns them appropriate data classification levels.

Defining these identification parameters is a prerequisite for effective security management. Once configured, these classifications allow the **Strategy Center** to precisely trigger audit or blocking actions against target files.

 &nbsp;

<span id="high-level-workflow"></span>
## High\-Level Workflow

SealSuite follows a structured "Prepare → Define → Enforce" approach to data security:

 &nbsp;

<span id="step-1:-establish-the-resource-library-(atomic-identifiers)"></span>
### Step 1: Establish the Resource Library (Atomic Identifiers)

Before creating complex rules, you must define the basic criteria, or atomic identifiers, that the system will look for. These resources serve as the building blocks for all identification logic.


* **Sensitive Thesaurus**: Contains keywords, phrases, and regular expressions (regex) tailored to your business.

* **File Fingerprint Library**: Uses unique digital signatures extracted from your most sensitive documents (e.g., source code, design blueprints). SealSuite scans sample files to create these fingerprints, allowing it to detect even partially modified versions of the original data.

* **File Type Library**: Identifies files based on their extensions and physical attributes. This includes hundreds of pre\-defined industry\-standard formats, as well as custom extensions unique to your organization.

* **File Source Library**: Tracks the origin of data, such as specific business URLs, code repository paths, or local application identifiers.

* **File Transfer Action Library**: Displays the file operations that SealSuite can track on different operating systems, such as **Save As, compression, and decompression**, as well as **the supported software scope**. It is for display only and serves as a reference for administrators to evaluate auditing granularity and configure control policies.


 &nbsp;

<span id="hNEoVG0GO"></span>
### Step 2: Configure Data Sensitivity Levels

Before defining specific data classification and grading rules, you need first establish a data sensitivity level framework in the system that aligns with the enterprise's security management policies.

**Sensitive Level Settings**: Customize the labels and visual system for enterprise data sensitivity levels (L1 to L9). Administrators can flexibly enable the required levels and customize the name, description, and color of each level.

<span id="step-2:-define-classification-and-grading-rules"></span>
### Step 3: Define Classification and Grading Rules

In this stage, you combine the atomic identifiers from Step 1 using logical operators (AND/OR). The goal is to translate business context into technical rules.

**Classification and Grading Rules**: Define identification standards that reflect enterprise business semantics by combining multiple dimensions with logical operators. For example, combine “File source (code repository)” and “File type (source code extension)” to define a “Core R&D Code” rule, and assign it a custom sensitivity label (such as L9).

 &nbsp;

<span id="step-3:-deploy-control-policies"></span>
### Step 4: Deploy Control Policies

The final step is to link your classification results to actual security behaviors in the **Strategy Center**.

When configuring file outbound control or channel blocking policies, you reference your classification rules. Depending on the data's sensitivity label, the system will execute specific responses, such as logging the activity, capturing screenshots for evidence, or blocking the transmission in real\-time.

 &nbsp;

<span id="functional-modules-at-a-glance"></span>
## Functional Modules at a Glance

Use the table below to determine which module best fits your specific data detection needs:

&nbsp;


|**Module** |**Primary Use Case** |**Detection Target** |**Reference** |
|---|---|---|---|
|**Sensitive Thesaurus** |Detecting specific text patterns or sensitive terminology. |Keywords, Regex |[Managing sensitive thesaurus](https://docs.byteplus.com/docs/sealsuite/managing-sensitive-thesaurus) |
|**File Fingerprint Library** |Protecting core assets where content is unique and highly sensitive. |Blueprints, contracts, proprietary models |[Managing the File Fingerprint Library](https://docs.byteplus.com/docs/sealsuite/managing-the-file-fingerprint-library) |
|**File Type Library** |Categorizing files based on their format and physical properties. |Extensions (e.g., .pdf, .docx, .cad) |[Managing the File Type Library](https://docs.byteplus.com/docs/sealsuite/managing-the-file-type-library) |
|**File Source Library** |Identifying data based on where it was downloaded or created. |Business URLs, Repo paths, App processes |[Managing the File Source Library](https://docs.byteplus.com/docs/sealsuite/managing-the-file-source-library) |
|**Sensitive Level Settings** |Customizing the labels and visual system for enterprise data sensitivity levels (L1 to L9) and control the enabled status of each level. |Sensitivity level name, color, enabled status |[Managing the Sensitive Level Settings](https://docs.byteplus.com/en/docs/sealsuite/management-grading-settings) |
|**Classification and Grading Rules** |Aggregates all factors above to assign a final sensitivity level, acting as the logic layer. |Logical combinations and data labeling |[Managing classification and grading rules](https://docs.byteplus.com/docs/sealsuite/managing-classification-and-grading-rules) |
