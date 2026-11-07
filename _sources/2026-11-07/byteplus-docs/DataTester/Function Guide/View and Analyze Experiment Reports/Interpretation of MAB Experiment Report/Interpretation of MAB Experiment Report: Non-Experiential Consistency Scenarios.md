---
title: "Interpretation of MAB Experiment Report: Non-Experiential Consistency Scenarios"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Interpretation-of-MAB-Experiment-Report-Non-Experiential-Consistency-Scenarios"
---

<span id="c20ea04a"></span>
# Core concept

Consistency of experience: refers to entering groups but not leaving groups, ensuring that users participating in tuning enter the same experimental version every time.

Non\-experiential consistency: After entering the group, it is allowed to leave the group, and users participating in the tuning may enter different experimental versions during the process.

Non\-Experience Consistency Scenarios: Scenarios in which the Experience Consistency feature is turned off during the experiment.

<span id="9a9bbdb2"></span>
# Operation and report page similarities and differences

**Comparing non\-experience consistency with experience consistency**


|**Module** |**Point of difference** |**Similarity** |**Example diagram in a non\-experience consistency scenario** |
|---|---|---|---|
|Overall revenue improvement of MAB experiment |Add a prompt for editing the time point in the experiment. After clicking, you can display the version and traffic changes before and after editing at the corresponding time point. |The data presented has the same meaning and function |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aeed9ca4f808467caffbf3648c34fe98~tplv-goo7wpa0wc-image.image) </span> |
|List of core metrics |Details of core metrics, from experimental version information to tuning parameter information;<br><br>Since the parameters can be adjusted during the experiment, the current online parameters and all parameters will be displayed in TAB |The online parameters also show the value of the metric, the number of users entering the group, and the probability of becoming the optimal group |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5619abb74ab24f96ba474283fd92249b~tplv-goo7wpa0wc-image.image) </span> |
|Core metric trend |Index trend chart, from experimental version information to tuning parameter information;<br><br>Clearly describe the node that edits the experimental information in the experiment, and click to display the flow of each parameter before and after adjustment<br><br>Click Hide offline parameters to observe the data trend of current online parameters |Show cumulative metric data for each round of tuning |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e7e4f7363784f0495d98101f44073f0~tplv-goo7wpa0wc-image.image) </span> |
|Experimental traffic allocation |The experimental traffic distribution trend is changed from experimental version information to tuning parameter information.<br><br>Clearly describe the node that edits the experimental information in the experiment, and click to display the flow of each parameter before and after adjustment |Show the cumulative and flow allocation of each round of tuning |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/936f6ef00dd746ccb4adb99cf97e582b~tplv-goo7wpa0wc-image.image) </span> |
