---
title: "Re-importing Content industry Live Mode data"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-re_importing_content_industry_live_mode_data"
---

If you encounter issues with your imported data, you can resolve them by deleting and reimporting it. The system will automatically import and remove duplicate data from dates that were not deleted.

<span id="86073608"></span>
# Re\-importing historical data

You can re\-import your historical data through the BytePlus Recommend console.

**To re\-import live historical data:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to re\-import data to.

   The Validate Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a3a21c7a01f409eb80cff9865a8df80~tplv-goo7wpa0wc-image.image) </span>

3. Click **Import data**.

   The Import data pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d61213ab8ed44649585e61271a171b2~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

4. Select the **Import Method**.

5. If GCS/S3, fill in the directory path. If API/SDK, follow the instructions.

6. Click **Select files**.

7. Select your files.

8. You can **Preview** your files if needed.

9. Click **Import data**.

   The trial data re\-import process begins.


<span id="5202d1d5"></span>
# Re\-importing incremental data

For API/SDK imports, if you reimport the data, user events will be organized based on their timestamps. To ensure accurate metric calculations, it's recommended to import the latest user or content data. These will be stored as if they were from the day of the initial deletion, even if they are shown in the import summary on the date of the original import block. For example, if data was blocked from August 1st to 5th, importing user and product data for the 5th is advised, and it will be treated as if it was imported on August 1st for metrics recalculation.

**To re\-import incremental data:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to re\-import data to.

   The Validate Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a3a21c7a01f409eb80cff9865a8df80~tplv-goo7wpa0wc-image.image) </span>

3. Click **Import data**.

   The Import data pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d61213ab8ed44649585e61271a171b2~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

4. Select the **Import Method**.

5. If GCS/S3, fill in the directory path. If API/SDK, follow the instructions.

6. Click **Select files**.

7. Select your files.

8. You can **Preview** your files if needed.

9. Click **Import data**.

   The data re\-import process begins.
