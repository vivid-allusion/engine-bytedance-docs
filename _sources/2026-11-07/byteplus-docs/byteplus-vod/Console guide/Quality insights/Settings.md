---
title: "Settings"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-settings"
---

On the **Settings** page, you can create, edit, delete, and manage custom dimensions for your data analysis, including **filters**, **CDN vendors**, and **business tags**.

Configurations you create here can be applied directly in the **Dashboard** (on the QoS, QoE, and Cost Metrics tabs) and the **Analysis and diagnosis** page. This is ideal for long\-term monitoring of specific data streams.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please note that any changes (adds, edits, or deletes) made on this page will take effect in approximately 30 minutes.</div>


<span id="7f9b4cae"></span>
## Managing filters

Filters allow you to define a set of rules across multiple dimensions to precisely segment your data during analysis. Once created, you can apply them by selecting **Filter mode** on the **Play QoS**, **Play QoE**, and **Cost metrics** tabs of the **Dashboard**.

<span id="37491bbe"></span>
### Adding a filter


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. In the left navigation pane, click **Quality insights** \> **Settings**.

3. Go to the **Filters** tab and select the **App name** and **Device type** for which you want to create the filter.

4. Click **Add filter**.

5. In the drawer that appears, configure the filter:

   * **Filter name**: (Required) Enter a descriptive name for your filter, up to 100 characters.

   * **Rule configuration**: Define the filter rules using "AND" and "OR" logic.

      * **Condition groups**: Different condition groups are linked by an **OR** logic (data must match any one group).

      * **Conditions**: Conditions within the same group are linked by an **AND** logic (data must match all conditions in the group).

6. Click **Confirm**.


<span id="53b41cdd"></span>
## Managing CDN vendors

If you use multiple CDN services, this feature allows you to group different CDN domains under a custom "CDN vendor" dimension. This enables you to compare the performance of different providers during data analysis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can add a maximum of 5 CDN vendors.</div>


* <div data-tips="true" data-tips-type="tip">After the configuration takes effect, historical data will be backfilled to the nearest hour.</div>



<span id="4a4c4733"></span>
### Adding a CDN vendor


1. On the **Settings** page, switch to the **CDN vendor management** tab.

2. Click **Add CDN vendor dimension**.

3. In the dialog box, configure the following:

   * **CDN vendor name**: (Required) A custom name for the vendor.

   * **CDN domain**: (Required) Select the corresponding CDN domains for this vendor from the drop\-down list. Multiple domains are supported, but wildcard domains are not.

4. Click **Confirm**.


<span id="1d611a22"></span>
### Using the CDN vendor dimension

Once configured, you can use this dimension in the following ways:


* **Dashboard**: In **Breakdown by dimension** mode, select "CDN vendor" as a **Global breakdown dimension** or as a criterion for a **dimension filter**.

* **Filters**: Use "CDN vendor" as a condition when creating a filter.


<span id="6f247e9d"></span>
## Managing business tags

A business tag is a custom label you can use to classify your video content based on your business logic, such as "immersive feed," "short\-form video," or "long\-form video." By reporting these tags from your client application, you can analyze data segmented by business scenario.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can create a maximum of 20 business tags.</div>


<span id="9c4272fe"></span>
### Step 1: Create the business tag in the console


1. On the **Settings** page, switch to the **Business tag** tab.

2. Select an app and click **Query**.

3. Click **Create business tag**. In the configuration panel, provide the following information:

   * **Business tag**: (Required) The identifier to be used in the client\-side SDK calls, up to 20 characters.

   * **Display name**: (Required) The name that will appear in the console for easy identification, up to 20 characters.

   * **Business subtag**: (Optional) A sub\-category for more granular classification, such as "encrypted video" or "audio." You can add up to 20 sub\-types per business tag.

4. Click **Confirm**.


<span id="6848d991"></span>
### Step 2: Set and report from the client

Creating a business tag in the console is only the first step. To make it effective, you **must** implement the corresponding SDK calls in your client application to set the `Tag` and `Subtag` for each video playback. This ensures that the data is correctly reported and categorized.


* **Set business tag**

   * Android: [Setting business tags](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-android#d01cc9b4)

   * iOS: [Setting business tags](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-ios#761cabed)

* **Set business subtag**

   * Android: [Setting business subtags](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-android#5660d314)

   * iOS: [Setting business subtags](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-ios#5717f6fa)


<span id="5b79d586"></span>
### Step 3: Use the business tag for analysis

Once the client\-side reporting is in place, you can use this dimension in the following ways:


* **Dashboard**: In **Breakdown by Dimension** mode, select "business tag" as a **Global breakdown dimension** or as a criterion for a **Dimension filter**.

* **Filters**: Use "business tag" as a condition when creating a filter.
