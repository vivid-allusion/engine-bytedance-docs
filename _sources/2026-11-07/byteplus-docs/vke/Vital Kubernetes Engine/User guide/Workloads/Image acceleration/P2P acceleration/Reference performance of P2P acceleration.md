---
title: "Reference performance of P2P acceleration"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/P2P_Performance_Testing"
---

The P2P acceleration performance varies depending on the storage type used by nodes. To help you evaluate the acceleration performance for container image pulls, this topic provides test data for three storage scenarios: local NVMe SSD, cloud ESSD Flex, and cloud ESSD PL0. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Actual performance is also affected by factors such as cluster size, instance type, network bandwidth, image size, and concurrency. Refer to the test results from your production environment.</div>


<span id="wuxzZTeu"></span>
## Test environment

The tests described in this topic were conducted with the same cluster size, ECS instance type, network performance, and P2P Peer specifications. Only the storage resource type varied. Different storage types have different read/write performance characteristics, resulting in differences in image pull performance. The test environment configuration is shown in the following table.


|<div style="text-align: center"><br>Test environment</div><br> |<div style="text-align: center"><br>Local disk</div><br> |<div style="text-align: center"><br>Cloud ESSD Flex</div><br> |<div style="text-align: center"><br>Cloud ESSD PL0</div><br> |
|---|---|---|---|
|<div style="text-align: center"><br>Cluster size</div><br> |<div style="text-align: center"><br>300 nodes</div><br> |||
|<div style="text-align: center"><br>ECS instances</div><br> |<div style="text-align: center"><br>Instance specification ecs.i4s.4xlarge</div><br> |||
|<div style="text-align: center"><br>Network performance</div><br> |<div style="text-align: center"><br>Baseline bandwidth 25 Gbit/s</div><br> |||
|<div style="text-align: center"><br>Storage resources</div><br> |<div style="text-align: center"><br>Local NVMe SSD</div><br> |<div style="text-align: center"><br>Cloud ESSD Flex</div><br> |<div style="text-align: center"><br>Cloud ESSD PL0</div><br> |
|<div style="text-align: center"><br>P2P Peer specifications</div><br> |<div style="text-align: center"><br>1C2G</div><br> |||
|<div style="text-align: center"><br>CR bandwidth</div><br> |<div style="text-align: center"><br>100Gbit/s</div><br> |||


<span id="jIU73D0P"></span>
## Test result

<span id="FtXnPrFR"></span>
### **Local NVMe SSD**

When a local NVMe SSD is used as the cache disk, the end\-to\-end container image startup time (including the time for containerd to download and decompress the image) is shown in the following table.


|<div style="text-align: center"><br><strong>Image specification</strong></div><br> |<div style="text-align: center"><br><strong>P50 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P90 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P95 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P99 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>Number of origin\-pull nodes</strong></div><br> |
|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>1 GiB (256 MiB × 4 layers)</div><br> |<div style="text-align: center"><br>3.73</div><br> |<div style="text-align: center"><br>4.46</div><br> |<div style="text-align: center"><br>5.03</div><br> |<div style="text-align: center"><br>9.21</div><br> |<div style="text-align: center"><br>20.64</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>2 GiB (256 MiB × 8 layers)</div><br> |<div style="text-align: center"><br>6.52</div><br> |<div style="text-align: center"><br>8.55</div><br> |<div style="text-align: center"><br>9.96</div><br> |<div style="text-align: center"><br>11.68</div><br> |<div style="text-align: center"><br>12.63</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>4 GiB (512 MiB × 8 layers)</div><br> |<div style="text-align: center"><br>11.59</div><br> |<div style="text-align: center"><br>13.62</div><br> |<div style="text-align: center"><br>15.24</div><br> |<div style="text-align: center"><br>17.11</div><br> |<div style="text-align: center"><br>18.28</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>10 GiB (1 GiB × 10 layers)</div><br> |<div style="text-align: center"><br>25.27</div><br> |<div style="text-align: center"><br>28.38</div><br> |<div style="text-align: center"><br>29.79</div><br> |<div style="text-align: center"><br>33.83</div><br> |<div style="text-align: center"><br>37.51</div><br> |<div style="text-align: center"><br>1</div><br> |


<span id="xV62GX9O"></span>
### **Cloud ESSD Flex**

When a cloud ESSD Flex is used as the cache disk, the end\-to\-end container image startup time (including the time for containerd to download and decompress the image) is shown in the following table.


|<div style="text-align: center"><br><strong>Image specification</strong></div><br> |<div style="text-align: center"><br><strong>P50 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P90 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P95 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P99 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>Number of origin\-pull nodes</strong></div><br> |
|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>1 GiB (256 MiB × 4 layers)</div><br> |<div style="text-align: center"><br>9.14</div><br> |<div style="text-align: center"><br>9.83</div><br> |<div style="text-align: center"><br>10.13</div><br> |<div style="text-align: center"><br>13.67</div><br> |<div style="text-align: center"><br>13.84</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>2 GiB (256 MiB × 8 layers)</div><br> |<div style="text-align: center"><br>16.61</div><br> |<div style="text-align: center"><br>17.48</div><br> |<div style="text-align: center"><br>17.84</div><br> |<div style="text-align: center"><br>21.44</div><br> |<div style="text-align: center"><br>21.78</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>4 GiB (512 MiB × 8 layers)</div><br> |<div style="text-align: center"><br>34.08</div><br> |<div style="text-align: center"><br>36.82</div><br> |<div style="text-align: center"><br>37.26</div><br> |<div style="text-align: center"><br>39.81</div><br> |<div style="text-align: center"><br>47.05</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>10 GiB (1 GiB × 10 layers)</div><br> |<div style="text-align: center"><br>115.99</div><br> |<div style="text-align: center"><br>125.31</div><br> |<div style="text-align: center"><br>127.11</div><br> |<div style="text-align: center"><br>131.16</div><br> |<div style="text-align: center"><br>137.10</div><br> |<div style="text-align: center"><br>1</div><br> |


<span id="xAe2epa7"></span>
### **Cloud ESSD PL0**

When a cloud ESSD PL0 ** ** is used as the cache disk, the end\-to\-end container image startup time (including the time for containerd to download and decompress the image) is shown in the following table.


|<div style="text-align: center"><br><strong>Image specification</strong></div><br> |<div style="text-align: center"><br><strong>P50 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P90 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P95 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>P99 latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>Maximum latency (s)</strong></div><br> |<div style="text-align: center"><br><strong>Number of origin\-pull nodes</strong></div><br> |
|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>1 GiB (256 MiB × 4 layers)</div><br> |<div style="text-align: center"><br>10.19</div><br> |<div style="text-align: center"><br>11.03</div><br> |<div style="text-align: center"><br>11.26</div><br> |<div style="text-align: center"><br>14.99</div><br> |<div style="text-align: center"><br>15.13</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>2 GiB (256 MiB × 8 layers)</div><br> |<div style="text-align: center"><br>19.97</div><br> |<div style="text-align: center"><br>20.81</div><br> |<div style="text-align: center"><br>21.05</div><br> |<div style="text-align: center"><br>24.71</div><br> |<div style="text-align: center"><br>24.77</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>4 GiB (512 MiB × 8 layers)</div><br> |<div style="text-align: center"><br>40.33</div><br> |<div style="text-align: center"><br>41.52</div><br> |<div style="text-align: center"><br>43.97</div><br> |<div style="text-align: center"><br>44.38</div><br> |<div style="text-align: center"><br>44.51</div><br> |<div style="text-align: center"><br>1</div><br> |
|<div style="text-align: center"><br>10 GiB (1 GiB × 10 layers)</div><br> |<div style="text-align: center"><br>105.92</div><br> |<div style="text-align: center"><br>110.53</div><br> |<div style="text-align: center"><br>111.57</div><br> |<div style="text-align: center"><br>113.26</div><br> |<div style="text-align: center"><br>114.44</div><br> |<div style="text-align: center"><br>1</div><br> |
