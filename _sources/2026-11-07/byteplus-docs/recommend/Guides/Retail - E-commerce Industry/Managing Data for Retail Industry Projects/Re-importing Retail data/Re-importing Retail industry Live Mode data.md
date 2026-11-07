---
title: "Re-importing Retail industry Live Mode data"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-reimporting_retail_industry_live_mode_data"
---

If you encounter issues with your imported data, you can resolve them by deleting and reimporting it. The system will automatically import and remove duplicate data from dates that were not deleted.

<span id="a8aaabf1"></span>
# Re\-importing historical data

You can re\-import your historical data through the BytePlus Recommend console.

**To re\-import live historical data:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to re\-import data to.

   The Configure screen appears.

3. Click **Next**.

   The Import screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a30c75d6c4e44d0eab43fb5d1423ea15~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

4. Click **Import data**.

   The Import data pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d61213ab8ed44649585e61271a171b2~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Select the **Import Method**.

6. If GCS/S3, fill in the directory path. If API/SDK, follow the instructions.

7. Click **Select files**.

8. Select your files.

9. You can **Preview** your files if needed.

10. Click **Import data**.

   The data re\-import process begins.


<span id="380219bd"></span>
# Re\-importing incremental data

For API/SDK imports, if you reimport the data, user events will be organized based on their timestamps. To ensure accurate metric calculations, it's recommended to import the latest user or product data. These will be stored as if they were from the day of the initial deletion, even if they are shown in the import summary on the date of the original import block. For example, if data was blocked from August 1st to 5th, importing user and product data for the 5th is advised, and it will be treated as if it was imported on August 1st for metrics recalculation.

**To re\-import incremental data:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to re\-import data to.

   The Configure screen appears.

3. Click **Next**.

   The Import screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a30c75d6c4e44d0eab43fb5d1423ea15~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

4. Click **Import data**.

   The Import data pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d61213ab8ed44649585e61271a171b2~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Select the **Import Method**.

6. If GCS/S3, fill in the directory path. If API/SDK, follow the instructions.

7. Click **Select files**.

8. Select your files.

9. You can **Preview** your files if needed.

10. Click **Import data**.

   The data re\-import process begins.
