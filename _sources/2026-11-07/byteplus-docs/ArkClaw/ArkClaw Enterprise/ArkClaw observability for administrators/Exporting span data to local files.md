---
title: "Exporting span data to local files"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Exporting_span_data_to_local_files"
---

Span information can be exported and used in scenarios such as data evaluation, trace diagnosis algorithm verification, detection rule optimization, exception identification effectiveness assessment, and fault case accumulation and reproduction. This topic describes how to export span data.

<span id="OEl42IR4"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Click the **Trace analysis** tab. Filter the trace data to be analyzed based on your business requirements. Select the span list to be exported and click **Span export**.

4. Specify the Span export parameters based on your business requirements. Then, click **Preview** to view the export effect. Click **Export** to export the Span data based on the configuration.

   
   |Configuration item |Description |
   |---|---|
   |Export address |The export destination for span data. You can select **Local file** to export span data to a local CSV file. |
   |Export format |The export format for span data.<br><br><br>* **Select export field**: Manually select the Span fields and mapping relationships to be exported.<br><br>* **Export span details**: Export complete span data. |
   |Field mapping |The field mapping relationship during data import. You need to specify this parameter when the Export format parameter is set to Select export field. Select a Trace Span field and the evaluation set column to which the data will be imported. |
   |Sample Span |The sample span. It is used for reference only. |
   


<span id="M8BYl5Bo"></span>
## What to do next

Go to the local download manager, view the downloaded CSV files, and use them for subsequent data analysis.
