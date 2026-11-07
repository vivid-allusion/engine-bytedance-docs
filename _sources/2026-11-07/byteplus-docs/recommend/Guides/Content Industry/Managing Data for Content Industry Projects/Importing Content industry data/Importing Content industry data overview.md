---
title: "Importing Content industry data overview"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_content_industry_data_overview"
---

Once you have configured your data schema, scene, attribution, and metrics, you can start to import your Trial, Historical, and Incremental data. Through the BytePlus Recommend console, you can first access the Import dashboard in **Trial** mode.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a6eff161e9240dfbe6d84f190dac375~tplv-goo7wpa0wc-image.image) </span>

<span id="304d2244"></span>
# Import stages

There are several types of data and import stages: Trial Historical, Historical, and Incremental.


|**Data Type** |**Project Mode** |**Purpose** |**Data Period Required** |**Time Data was Retrieved** |**Import Methods** |
|---|---|---|---|---|---|
|Trial Historical |Trial Mode |The purpose of trial import is to provide users with the ability for fast import and error diagnosis and facilitate the speedy implementation process.<br><br>The data imported in Trial Mode is 1\-2 weeks worth of **historical data**. |Up to 2 weeks |Recent 100 days |* GCS<br><br>* S3<br><br>* API/SDK |
|Historical |Live Mode |Users can import historical data for the model. The full\-bulk upload requires a minimum of two months of historical data. |Minimum 60 days up to 100 days |Recent 100 days |* GCS<br><br>* S3<br><br>* API/SDK |
|Incremental |Live Mode |Users can import incremental data for real\-time data synchronization. |Most recent data |Today's data |* GCS<br><br>* S3<br><br>* API/SDK |


<span id="f36e7178"></span>
## Trial data import

After users have defined the data schema in the BytePlus Recommend console, they can start importing their trial data. The purpose of the trial import is to provide users with the ability for fast import and error diagnosis and facilitate the speedy implementation process. Trial import is only available in **Trial** **Mode**.

A user can import up to 2 weeks of Historical data. This allows you to better understand and evaluate the quality of your data before committing to the entire historical and incremental data import cycle, which can take up to several days. The imported trial data will not be used for model training, and instead provides an opportunity to identify any errors. Once the imported trial historical data is cleared of any errors, you can switch to **Live Mode** and all the historical data imported during **Trial Mode** will be deleted.

After importing the trial data, you can view the BytePlus Recommend console's data validation report that provides you with details on the quality and completeness of your imported data. Through this, you can still configure the data schema, scene, attribution, and metrics if needed.

For more information on managing your data schema, scene, attribution, and metrics, refer [here](https://docs.byteplus.com/recommend/docs/configuration_dashboard_overview).

<span id="53792173"></span>
## Historical data import

You can import historical data in **Live Mode**. The full\-bulk upload requires a minimum of two months of historical data. Recommendation systems work majorly on understanding patterns. Therefore, analysing customer data, including demographics, behavior, and historical interactions, to identify patterns and preferences that can drive personalized recommendations.

In **Live Mode**, you can import a minimum of 60 days to a maximum of 100 days of historical data. After importing the historical data, you can view the BytePlus Recommend console's data validation report that provides you with details on the quality and completeness of your imported data. Through this, you can still configure the data schema, scene, attribution, and metrics if needed.

<span id="5830af40"></span>
## Incremental data import

You can import incremental data for real\-time data synchronization. You can import incremental data only in **Live Mode**. Using the most recent user data, including their preferences, behaviour, and interests, the BytePlus Recommend model training process will definitely be more efficient. This produces more accurate and personalized product recommendations for your users.

In **Live Mode**, you can import the most recent data that you collated. The number of successful import records will be shown in real\-time. You can also check the import status for each file using the Validation screen.

<span id="4e4055ab"></span>
# Data import status

There are different types of data import statuses:


|**Data Import Status** |**Description** |
|---|---|
|Importing |Indicates that new data is flowing in and processed, as well as report generation. You cannot delete or re\-import data when the Importing status is on\-going. |
|Completed |When the import status is completed, it means all the data has been successfully imported to the BytePlus Recommend console. You can then proceed to validate the data and modify the content if necessary. |
