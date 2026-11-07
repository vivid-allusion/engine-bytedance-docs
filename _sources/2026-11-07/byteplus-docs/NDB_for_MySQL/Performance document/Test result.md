---
title: "Test result"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Test_result"
---

This article introduces the performance test results of read\-only, write\-only and read\-write of NDB for MySQL under MySQL version 8.0.

<span id="只读性能"></span>
## Read\-only performance


|<div style="text-align: center"><br>Specification code</div><br> |<div style="text-align: center"><br>Max connections</div><br> |<div style="text-align: center"><br>CPU</div><br> |<div style="text-align: center"><br>Memory</div><br> |<div style="text-align: center"><br>Number of tables</div><br> |<div style="text-align: center"><br>Single table data volume</div><br> |<div style="text-align: center"><br>Thread count</div><br> |<div style="text-align: center"><br>QPS</div><br> |<div style="text-align: center"><br>TPS</div><br> |
|---|---|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>vedb.mysql.x4.large</div><br> |<div style="text-align: center"><br>8000</div><br> |<div style="text-align: center"><br>4C</div><br> |<div style="text-align: center"><br>16GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>204683.91</div><br> |<div style="text-align: center"><br>20468.39</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.xlarge</div><br> |<div style="text-align: center"><br>16000</div><br> |<div style="text-align: center"><br>8C</div><br> |<div style="text-align: center"><br>32GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>512</div><br> |<div style="text-align: center"><br>415016.47</div><br> |<div style="text-align: center"><br>41501.65</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.2xlarge</div><br> |<div style="text-align: center"><br>32000</div><br> |<div style="text-align: center"><br>16C</div><br> |<div style="text-align: center"><br>64GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>512</div><br> |<div style="text-align: center"><br>753576.38</div><br> |<div style="text-align: center"><br>75357.64</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.4xlarge</div><br> |<div style="text-align: center"><br>64000</div><br> |<div style="text-align: center"><br>32C</div><br> |<div style="text-align: center"><br>128GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>1024</div><br> |<div style="text-align: center"><br>1278639.53</div><br> |<div style="text-align: center"><br>127863.96</div><br> |


<span id="只写性能"></span>
## Write\-only performance


|<div style="text-align: center"><br>Specification code</div><br> |<div style="text-align: center"><br>Max connections</div><br> |<div style="text-align: center"><br>CPU</div><br> |<div style="text-align: center"><br>Memory</div><br> |<div style="text-align: center"><br>Number of tables</div><br> |<div style="text-align: center"><br>Single table data volume</div><br> |<div style="text-align: center"><br>Thread count</div><br> |<div style="text-align: center"><br>QPS</div><br> |<div style="text-align: center"><br>TPS</div><br> |
|---|---|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>vedb.mysql.x4.large</div><br> |<div style="text-align: center"><br>8000</div><br> |<div style="text-align: center"><br>4C</div><br> |<div style="text-align: center"><br>16GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>42710.68</div><br> |<div style="text-align: center"><br>7118.45</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.xlarge</div><br> |<div style="text-align: center"><br>16000</div><br> |<div style="text-align: center"><br>8C</div><br> |<div style="text-align: center"><br>32GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>512</div><br> |<div style="text-align: center"><br>89429.02</div><br> |<div style="text-align: center"><br>14904.84</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.2xlarge</div><br> |<div style="text-align: center"><br>32000</div><br> |<div style="text-align: center"><br>16C</div><br> |<div style="text-align: center"><br>64GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>1024</div><br> |<div style="text-align: center"><br>177916.55</div><br> |<div style="text-align: center"><br>29652.75</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.4xlarge</div><br> |<div style="text-align: center"><br>64000</div><br> |<div style="text-align: center"><br>32C</div><br> |<div style="text-align: center"><br>128GiB</div><br> |<div style="text-align: center"><br>250</div><br> |<div style="text-align: center"><br>25000</div><br> |<div style="text-align: center"><br>1024</div><br> |<div style="text-align: center"><br>289969.8</div><br> |<div style="text-align: center"><br>48328.29</div><br> |


<span id="读写性能"></span>
## Read/Write performance


|<div style="text-align: center"><br>Specification code</div><br> |<div style="text-align: center"><br>Max connections</div><br> |<div style="text-align: center"><br>CPU</div><br> |<div style="text-align: center"><br>Memory</div><br> |<div style="text-align: center"><br>Number of tables</div><br> |<div style="text-align: center"><br>Single table data volume</div><br> |<div style="text-align: center"><br>Thread count</div><br> |<div style="text-align: center"><br>QPS</div><br> |<div style="text-align: center"><br>TPS</div><br> |
|---|---|---|---|---|---|---|---|---|
|<div style="text-align: center"><br>vedb.mysql.x4.large</div><br> |<div style="text-align: center"><br>8000</div><br> |<div style="text-align: center"><br>4C</div><br> |<div style="text-align: center"><br>16GiB</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>250000</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>82500.51</div><br> |<div style="text-align: center"><br>4125.03</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.xlarge</div><br> |<div style="text-align: center"><br>10000</div><br> |<div style="text-align: center"><br>8C</div><br> |<div style="text-align: center"><br>32GiB</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>250000</div><br> |<div style="text-align: center"><br>512</div><br> |<div style="text-align: center"><br>162264.56</div><br> |<div style="text-align: center"><br>8113.23</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.2xlarge</div><br> |<div style="text-align: center"><br>32000</div><br> |<div style="text-align: center"><br>16C</div><br> |<div style="text-align: center"><br>64GiB</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>250000</div><br> |<div style="text-align: center"><br>1024</div><br> |<div style="text-align: center"><br>317159.66</div><br> |<div style="text-align: center"><br>15857.98</div><br> |
|<div style="text-align: center"><br>vedb.mysql.x4.4xlarge</div><br> |<div style="text-align: center"><br>64000</div><br> |<div style="text-align: center"><br>32C</div><br> |<div style="text-align: center"><br>128GiB</div><br> |<div style="text-align: center"><br>25</div><br> |<div style="text-align: center"><br>250000</div><br> |<div style="text-align: center"><br>512</div><br> |<div style="text-align: center"><br>564132.33</div><br> |<div style="text-align: center"><br>28206.62</div><br> |
