---
title: "Performance test results"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/performance_test_result"
---

This article describes the performance test results of each specification instance of RDS for PostgreSQL under each PostgreSQL edition.

<span id=".UG9zdGdyZVNRTCAxNCDmtYvor5Xnu5Pmnpw="></span>
## PostgreSQL 17 Test Results


|<div style="text-align: center"><br><strong>Specification code</strong></div><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>35,151</div><br> |<div style="text-align: center"><br>1,758</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>68,461</div><br> |<div style="text-align: center"><br>3,423</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>22</div><br> |<div style="text-align: center"><br>88,312</div><br> |<div style="text-align: center"><br>4,416</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>167,789</div><br> |<div style="text-align: center"><br>8,389</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>287,652</div><br> |<div style="text-align: center"><br>14,383</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>473,423</div><br> |<div style="text-align: center"><br>23,671</div><br> |


<span id="MeeSgWoi"></span>
## PostgreSQL 16 Test Rresults


|<div style="text-align: center"><br><strong>Specification code</strong></div><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>34,542</div><br> |<div style="text-align: center"><br>1,727</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>68,713</div><br> |<div style="text-align: center"><br>3,436</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>91,582</div><br> |<div style="text-align: center"><br>4,579</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>40</div><br> |<div style="text-align: center"><br>171,015</div><br> |<div style="text-align: center"><br>8,551</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>284,550</div><br> |<div style="text-align: center"><br>14,227</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>472,018</div><br> |<div style="text-align: center"><br>23,601</div><br> |


<span id="zFRmSKKV"></span>
## PostgreSQL 15 Test Results


|<div style="text-align: center"><br><strong>Specification code</strong></div><br><br><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>34,850</div><br> |<div style="text-align: center"><br>1,742</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>68,015</div><br> |<div style="text-align: center"><br>3,401</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>88,612</div><br> |<div style="text-align: center"><br>4,431</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>159,506</div><br> |<div style="text-align: center"><br>7,975</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>295,849</div><br> |<div style="text-align: center"><br>14,792</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>470,018</div><br> |<div style="text-align: center"><br>23,501</div><br> |


<span id="z0V7fjEg"></span>
## PostgreSQL 14 Test Results


|<div style="text-align: center"><br><strong>Specification code</strong></div><br><br><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>34,107</div><br> |<div style="text-align: center"><br>1,705</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>67,351</div><br> |<div style="text-align: center"><br>3,368</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>89,122</div><br> |<div style="text-align: center"><br>4,456</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>172,665</div><br> |<div style="text-align: center"><br>8,633</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>282,923</div><br> |<div style="text-align: center"><br>14,146</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>474,825</div><br> |<div style="text-align: center"><br>23,741</div><br> |


<span id="bspjK9sp"></span>
## PostgreSQL 13 Test Results


|<div style="text-align: center"><br><strong>Specification code</strong></div><br><br><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32,961</div><br> |<div style="text-align: center"><br>1,648</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>65,131</div><br> |<div style="text-align: center"><br>3,257</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>85,483</div><br> |<div style="text-align: center"><br>4,274</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>164,102</div><br> |<div style="text-align: center"><br>8,205</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>279,289</div><br> |<div style="text-align: center"><br>13,964</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>458,509</div><br> |<div style="text-align: center"><br>22,925</div><br> |


<span id="NDEdddUu"></span>
## PostgreSQL 12 Test Results


|<div style="text-align: center"><br><strong>Specification code</strong></div><br><br><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32,475</div><br> |<div style="text-align: center"><br>1,624</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>72,636</div><br> |<div style="text-align: center"><br>3,632</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>96,423</div><br> |<div style="text-align: center"><br>4,821</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>161,234</div><br> |<div style="text-align: center"><br>8,062</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>270,949</div><br> |<div style="text-align: center"><br>13,547</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>433,671</div><br> |<div style="text-align: center"><br>21,683</div><br> |


<span id="WbCnkP9d"></span>
## PostgreSQL 11 Test Results


|<div style="text-align: center"><br><strong>Specification code</strong></div><br><br><br> |<div style="text-align: center"><br><strong>number of tables</strong></div><br> |<div style="text-align: center"><br><strong>Single table data volume</strong></div><br> |<div style="text-align: center"><br><strong>thread count</strong></div><br> |<div style="text-align: center"><br><strong>QPS</strong></div><br> |<div style="text-align: center"><br><strong>TPS</strong></div><br> |
|---|---|---|---|---|---|
|<div style="text-align: center"><br>rds.postgres.2c4g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>33,899</div><br> |<div style="text-align: center"><br>1,695</div><br> |
|<div style="text-align: center"><br>rds.postgres.4c8g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>67,662</div><br> |<div style="text-align: center"><br>3,383</div><br> |
|<div style="text-align: center"><br>rds.postgres.8c16g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>20</div><br> |<div style="text-align: center"><br>87,470</div><br> |<div style="text-align: center"><br>4,374</div><br> |
|<div style="text-align: center"><br>rds.postgres.16c64g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>161,529</div><br> |<div style="text-align: center"><br>8,076</div><br> |
|<div style="text-align: center"><br>rds.postgres.32c128g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>266,105</div><br> |<div style="text-align: center"><br>13,305</div><br> |
|<div style="text-align: center"><br>rds.postgres.64c512g</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>10,000,000</div><br> |<div style="text-align: center"><br>120</div><br> |<div style="text-align: center"><br>438,769</div><br> |<div style="text-align: center"><br>21,938</div><br> |
