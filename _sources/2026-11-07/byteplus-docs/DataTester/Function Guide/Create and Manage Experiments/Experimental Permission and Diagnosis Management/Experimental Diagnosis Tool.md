---
title: "Experimental Diagnosis Tool"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experimental-Diagnosis-Tool"
---

After the experiment is created, the experimental collaborators can use the experimental diagnostic tools provided by DataTester to monitor and analyze whether the shunting and whitelisting services of the current experiment are normal from the experimental perspective, that is, to see if the target experimental user hits the corresponding experimental version normally. This article introduces the precautions and operation instructions for using experimental diagnostic tools.

<span id="1c2551fa"></span>
# Precautions


* **Time limit:**  When diagnosing an experiment, the maximum time period for backtracking is 3 months, that is, you can diagnose hits in the experiment for up to three months.

* **Experiment type:**  Currently only "**debugging**", "**running**", "**frozen**" and "**suspended**" state of the **client side** experiment, you can use the experimental diagnostic tool.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>The"Frozen"</strong> and "<strong>Pause</strong>" state of the <strong>client side</strong> experiment can use the experimental diagnostic tool to see the hit during the experiment run.   </div>
   

* **Permission related:**  Users with the "Analyst" permission of the experiment can perform diagnostic analysis from the experimental perspective to see whether some users hit the experiment for a certain experimental version (or not selected experimental version) within a certain time period, and the reason for the missed analysis.


<span id="f8383d92"></span>
# Application scenario

If you have the following problems in your AB test, you can use hit diagnostics to troubleshoot the detailed reason why the experiment failed to hit.


* Why is my testing device whitelisted, but it doesn't work?

* The experiment has started. I have adjusted the traffic weight of the experimental version to 90%. Why hasn't the testing device hit the experimental version yet?

* The experiment has been going on for a while, but the number of users entering the group is not as expected. Is there a problem with the diversion?


<span id="三-实验命中诊断"></span>
# Operation guidance

<span id="78bd47e6"></span>
## Experimental Diagnostic Entrance

On the Experiment List page, click the name of the experiment, and then click the "Diagnosis" action button, as shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f70902326cf74cf8a6b35b840538c972~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-3-实验报告页"></span>
### Experimental Diagnostic Configuration

After entering the diagnostic tool page of the current experiment, you can configure the shunt user, time window, and experimental version information that need to be diagnosed, and query the user's request shunt and hit experiment within the target time window.


|Pparameter |Configuration instructions |
|---|---|
|**Offload users** |You can select the added user test whitelist from the drop\-down box, or manually enter the target user's ssid. |
|**Time window** |Select the time window for which diagnosis is required. The current maximum supported backtracking period is nearly 3 months. |
|**Experimental version** |Select the experimental version that requires diagnosis. |


Once configured, click **Start Diagnostics** to view the diagnosis results at the bottom of the page.

<span id="b5186883"></span>
## Experimental diagnosis

The experimental diagnostic results show you the list of all experimental offloads and the detailed request log of each offload request in the time window, and show you the reasons for the missed analysis results. You can click on the top right of the experimental diagnosis results to switch the way the results are displayed, and support **list mode** or **timeline mode**.


|List mode |Timeline mode |
|---|---|
|<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2780b34b7a1b43629ae0b1e1ecdb94a1~tplv-em5hxbkur4-noop.image?width=1663&height=607) </span> |<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/73b7d3521ced400ba9d3608252e44433~tplv-em5hxbkur4-noop.image?width=1653&height=593) </span> |


You can view the log JSON details of each shunt request, and you can further view the corresponding request parameters in the log in combination with the reasons for the misses given, to further clarify the solution of the misses.

<span id="7c12bb7d"></span>
## Reference: Detailed description of the cause of the miss


|Serial number |Cause of miss |Explain in detail |
|---|---|---|
|1 |The experimental status is closed. |The experiment has been closed, and no user can access it. |
|2 |Mutual exclusion layer hit rule |Whitelist users, hit other experiments on the same level. |
|3 |Does not belong to the traffic range |The user shunting result does not belong to the traffic interval of the experiment. The current experimental allocation total traffic is < experimental assigned traffic percentage \>, and the user belongs to the remaining traffic space. |
|4 |The experimental state is suspended |When the experiment was suspended, the user, although in the traffic zone, was unable to hit. |
|5 |The experimental status is preview/debugging |The experiment was in a debugging state at the time, and the user was not a whitelisted user and could not be hit. |
|6 |The experimental state is frozen |The experiment was frozen at the time, and the user did not expose the experiment before freezing. Although it belonged to the traffic range, it was unable to hit. |
|7 |Flow filter conditions do not meet |The user does not meet the audience filter criteria and cannot be hit.<br><br>Eg. The user "OS = Windows" does not meet the filter "OS = MAC/Android" and cannot hit. |
|8 |Miss multilink experiment |The user request URL misses the target URL of the multilink experiment. |
