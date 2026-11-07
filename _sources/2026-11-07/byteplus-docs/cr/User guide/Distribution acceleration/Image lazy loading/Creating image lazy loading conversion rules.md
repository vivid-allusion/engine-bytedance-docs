---
title: "Creating image lazy loading conversion rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/create-image-lazy-loading-conversion-rules"
---

Image lazy loading converts images to the Nydus format, allowing containers to start without downloading the entire image and only loading the actual data as needed. This can reduce container startup time to seconds. By creating conversion rules, the system can automatically convert images to the Nydus format after they are pushed. This topic describes how to create an image conversion rule in CR for image lazy loading.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This operation is only applicable to Standard Edition instances.</div>


* <div data-tips="true" data-tips-type="warning">Images larger than or equal to 60 GiB cannot be automatically converted via conversion rules. Manually convert such images offline, and then push them to CR for use.</div>


   * <div data-tips="true" data-tips-type="warning">For the manual conversion method, see <a href="https://docs.byteplus.com/en/docs/cr/Manually_convert_an_image_to_Nydus_format">Manually converting images to Nydus format</a>.</div>


   * <div data-tips="true" data-tips-type="warning">For instructions on pushing images, see <a href="https://docs.byteplus.com/en/docs/cr/getting-started">Getting Started</a>.</div>


* <div data-tips="true" data-tips-type="warning">Using this feature incurs additional image storage costs.</div>


* <div data-tips="true" data-tips-type="warning">Converting images for lazy loading takes time. We recommend configuring the conversion policy in advance and allowing sufficient time for the conversion to avoid affecting the service release date. For example, converting a 40 GiB image takes approximately 30 minutes.</div>



<span id="nw7Mhjs7"></span>
## Prerequisites

Instance has been created. For operation methods, see [Create standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

<span id="NhE5qiRS"></span>
## Procedure

This article describes how to create image lazy loading conversion rules in CR. For other related operations for implementing the lazy loading feature, see [procedure for lazy loading](https://docs.byteplus.com/en/docs/cr/Image_lazy_loading_overview?TagIDs=2,300&lang=en#YJ0OGOfB).


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. On the Standard Edition instance details page, select **Distribution acceleration** \> **Image lazy loading** in the left navigation bar.

3. On the **Image lazy loading** page, click **Create image lazy loading conversion rule**.

4. Configure the parameters of the image lazy loading conversion rule.

   * Basic information

      
      |Parameter |Description |
      |---|---|
      |Name |A custom name of the image lazy loading conversion rule. |
      |Description |A custom description of the image lazy loading conversion rule. |
      

   * Acceleration rule

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">OCI artifact types that do not support conversion will not be converted even if they match a conversion rule. For example, Helm Chart is of the Nydus type, so conversion is not supported.      </div>
      

      
      |Parameter |Description |
      |---|---|
      |Instance |The name of the selected instance, which cannot be modified. |
      |Rule dimension |Supports filtering target images by namespace and OCI artifact repository.<br><br><br>* **Namespace**: Filters images by namespace, including all OCI artifact repositories within the selected namespace.<br><br>* **OCI artifact repository**: Filters images by OCI artifact repository. |
      |Namespace |Select the namespace where the target images reside. |
      |OCI artifact repository |Select the OCI artifact repository where the target image is located. This is supported only when the ** Rule dimension** is **OCI artifact repository**. |
      |Tag rule |Configure the rule for filtering image tags.<br><br><br>* **All**: Selects all images that match the filter rule.<br><br>* **Regex matching**: Selects images that match the regular expression. For common regex matching usage examples, see [Regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
      |Rule state |Whether to enable the conversion rule. **If this feature is enabled**, the system automatically generates a Nydus image replica when an image matching the rule is pushed to CR. |
      

5. Click **Confirm** to complete creation.


<span id=".5pON5L2c57uT5p6c"></span>
## Results


* After creation is complete, you can view the generated conversion rule records on the **Image lazy loading** page.

* After a conversion task is complete, you can view the converted Nydus image in the OCI artifact repository.
