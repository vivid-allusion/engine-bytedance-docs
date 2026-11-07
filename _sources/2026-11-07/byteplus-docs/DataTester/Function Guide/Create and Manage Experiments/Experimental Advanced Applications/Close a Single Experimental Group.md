---
title: "Close a Single Experimental Group"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Close-a-Single-Experimental-Group"
---

<span id="一-概述及使用场景"></span>
# 1. Overview and usage scenarios

When multiple groups are started in the experiment, one group has an unacceptable negative direction due to engineering or strategy problems. It is necessary to stop the loss in time, but it is hoped that other groups will continue the experiment without being affected. Support closing a certain experimental group.

For example, the experiment turned on groups A, B, C, and D, and found that group B was significantly negative. They wanted to turn off group B but continued to try groups C and D.

<span id="二-关闭后分流说明"></span>
# 2. Traffic\-splitting instructions after closing


1. Users will no longer hit the experimental group, and the experimental group will have no data after today.

2. The traffic will not be released, nor will it enter other groups in the experiment nor be used by other experiments in the same layer. For example, in an experiment, four groups were started, and a total of 20% of the traffic was used; at this time, the available traffic on the experimental layer was 80%. After group B was closed, groups A, C, and D remained at 5% traffic each. And the available traffic on the experimental layer is still 80% (instead of 85%).

3. After the experimental group is closed, it cannot be reopened.

4. If the experiment continues to expand after closing the experimental group, the amount will be evenly expanded to four groups: A, B, C, and D, but the flow rate of group B is not effective. Still taking this example as an example, suppose that after closing group B, the experimental traffic is expanded to 40%; at this time, the available traffic on the experimental layer is 60%, and groups A, C, and D become 10% of each traffic. The closed group B will still occupy 10% of the traffic, but the traffic will not hit the group, and the configuration will not take effect.

5. When all the experimental groups in the experiment are closed, the experiment will be completed


<span id="三-功能入口"></span>
# 3. Function entrance

The experimental report page is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08954d014a7e40e2b51a00106d10b36b~tplv-goo7wpa0wc-image.image) </span>
