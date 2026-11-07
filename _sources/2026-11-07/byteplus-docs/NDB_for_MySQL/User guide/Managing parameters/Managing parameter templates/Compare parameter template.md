---
title: "Compare parameter template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Compare_parameter_template"
---

To facilitate the management and application of parameter templates, NDB for MySQL provides a comparison feature to quickly identify differences between templates and export the results as a CSV file to your local device.

## Precautions

* Only parameter templates of the same type can be compared. System parameter templates cannot be compared with custom parameter templates.

* Only parameter templates that apply to the same version can be compared.

## Procedure

1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the top menu bar, select the region where the parameter template is located.

3. Click **Parameter templates** in the left\-side navigation bar.

4. On the **Customized template** or **System template** tab, select the parameter templates to compare, and click **Parameter comparison**.

5. The **Parameter comparison** page displays the comparison results of two parameter templates. You can view only the **Comparison items with differences** or view **All comparison items**.

   > **tip**

   > Click the download icon in the upper\-right corner to export the comparison results of the parameter templates to your local device in CSV format.

6. Click **OK** to exit parameter comparison.

## Related APIs

|**API** |**Description** |
|---|---|
|[CompareParameterTemplates](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CompareParameterTemplates) |Call the CompareParameterTemplates API to compare parameter templates. |
