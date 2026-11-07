---
title: "Viewing historical diagnosis reports"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View_historical_diagnosis_reports"
---

You can view historical diagnosis reports to learn the development process of the target instance, as well as analyze and assess its historical issues.

> You can view historical diagnosis reports of all instances, but only reports from the past 60 days are available.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Instance Diagnosis", or select "Instances & Images \> Instances".

3. In the top navigation bar, select the project and region of the target instance. 

4. Click the "History of diagnosis" tab, or click the target instance name, and then select the "Diagnosis" tab.

5. On the History of diagnosis page, you can search for the target report by instance ID or report ID.

6. In the "Actions" column of the target instance, click the "View report" button to view the results and details of the instance diagnosis.

7. (**Optional**) If there are items recommended for repair, follow the repair suggestions or refer to the [diagnosis item repair suggestions](https://docs.byteplus.com/en/docs/ecs/Diagnosis_summary) to complete the fix. Then, click the "Re\-diagnosis" button in the "Actions" column of the target instance to verify whether the issues have been resolved.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the report involves the diagnosis of "Detecting ICMP connectivity of instances under the same VPC", the "Re\-diagnosis" button is grayed out. This means that you can not diagnose the selected instance again.   </div>
   

<div style="text-align: right">
</div>
