---
title: "Nonblocking DDL statements"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Nonblocking_DDL_statements"
---

NDB for MySQL supports a nonblocking DDL feature that effectively resolves table locking issues caused by DDL operations, minimizes business impact, and improves database performance.

<span id="NfYCu5VG"></span>
## Background

In MySQL, if a target table has uncommitted long\-running transactions or ongoing large queries, any DDL operation on it will continuously wait to acquire an MDL\-X lock. Because the MDL\-X lock has the highest priority, a DDL operation waiting to acquire it will block all new transactions on the target table, leading to a pile\-up of service connections and potentially crashing the entire service system. To solve this problem, NDB for MySQL provides a nonblocking DDL feature. By setting the timeout, retry interval, and retry count for an MDL\-X lock, it allows new transactions to access the target table even when it is unable to acquire the lock. This approach prevents DDL operations from blocking the service system, thus ensuring its availability and stability.

<span id="BFZkW04W"></span>
## Precautions

Enabling the nonblocking DDL feature can affect database performance and operations. The nonblocking DDL feature lowers the priority of DDL operations, and MDL lock acquisition may fail. This increases the probability of failure for DDL operations. Therefore, before you enable the nonblocking DDL feature, evaluate the database's concurrent operations and performance requirements to ensure its impact is acceptable.

<span id="4O9rFwCx"></span>
## Limitations

The following table lists the DDL types that support nonblocking operations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A DDL that does not support the nonblocking feature will be downgraded to a regular DDL, blocking other concurrent DMLs.</div>



|**DDL type** |**Operation** |**SQL statement** |**Support or not？**  |
|---|---|---|---|
|Instant DDL<br><br> |Column operations |ADD COLUMN |Support |
||Column operations |RENAME COLUMN |Support |
||Table operations |RENAME TABLE |Not supported |
||Table operations |TRUNCATE TABLE |Not supported |
||Database actions |ALTER DATABASE CHARACTER/COLLATE/ENCRYPTION/READ ONLY |Not supported |
|Online DDL |Index operations |ADD INDEX |Support |
||Column operations |DROP COLUMN |Support |
||Table operations |ALTER TABLE ENGINE |Support |
||Table operations |OPTIMIZE TABLE |Not supported |
|Copy DDL |Column operations |MODIFY COLUMN TYPE |Not supported |


<span id="KHcxfCch"></span>
## How to use

NDB for MySQL uses the following parameters to control the nonblocking DDL feature. The table below describes each parameter in detail.


|**Parameter** |**Effective scope** |**Description** |
|---|---|---|
|enable_nonblock_ddl<br><br> |Session<br><br> |Switch for the nonblocking DDL feature. The values are:<br><br><br>* ON: Enables the nonblocking DDL feature.<br><br>* OFF (default): Disables the nonblocking DDL feature. |
|nonblock_ddl_lock_wait_timeout<br><br> |Session |Sets the timeout duration in seconds for acquiring an MDL\-X lock. The default value is 1, and the value range is 1~31536000.<br><br>If this value is exceeded, the DDL temporarily releases the lock and waits for the next lock acquisition based on the retry interval and the number of retries. |
|nonblock_ddl_retry_interval |Session |Sets the retry interval for acquiring an MDL\-X lock after a timeout. The default value is 3. Value range: 1~31536000. Unit: Second. |
|nonblock_ddl_retry_times<br><br> |Session<br><br> |Sets the number of retries after an MDL\-X lock acquisition times out. The default value is 0, and the value range is 0~31536000.<br><br>In nonblocking DDL mode, the lock request is released after a period of waiting. |


<span id="Wfjz7A2Y"></span>
## Performance comparison

Use the SysBench tool to test the impact on services of enabling or disabling the nonblocking DDL feature.


1. Use SysBench to start and inject Read/Write transactions.

   ```Shell
   ./oltp_point_select.lua --mysql-storage-engine=innodb --tables=5 --mysql-db=sbtest --table-size=10000 --mysql-user=root --mysql-password=TAK**** --mysql-port=4200 --mysql-host=127.0.0.1 --rand-type=special --threads=128 --events=0 --range_selects=0 --rand-seed=42 --time=40 --report-interval=1 --percentile=99 --forced-shutdown=3 prepare
   
   ./oltp_read_write.lua --mysql-storage-engine=innodb --tables=1 --mysql-db=sbtest --table-size=10000 --mysql-user=root --mysql-password=TAK**** --mysql-port=4200 --mysql-host=127.0.0.1 --rand-type=special --threads=128 --events=0 --range_selects=0 --rand-seed=42 --time=600 --report-interval=1 --percentile=99 --forced-shutdown=3 run
   ```
   

2. Set nonblocking DDL parameters.

   ```SQL
   set session enable_nonblock_ddl = 0 ;
   set session nonblock_ddl_lock_wait_timeout = 1;
   set session nonblock_ddl_retry_interval = 1;
   set session nonblock_ddl_retry_times = 3;
   ```
   

3. Test DDL in a blocking state and observe the changes in TPS.

   ```SQL
   -- Enable a long transaction in session 1 and do not submit
   begin;
   select * from sbtest1;
   
    -- Execute DDL actions in session 2
    alter table sbtest1 add index idx_k_4(k);
   ```
   

   * When the nonblocking DDL feature is disabled, TPS continuously drops to 0.

      ```SQL
      [ 317s ] thds: 128 tps: 90.00 qps: 1412.03 (r/w/o: 877.02/349.01/186.00) lat (ms,99%): 3208.88 err/s: 6.00 reconn/s: 0.00
      [ 318s ] thds: 128 tps: 73.00 qps: 1360.07 (r/w/o: 885.05/323.02/152.01) lat (ms,99%): 3208.88 err/s: 6.00 reconn/s: 0.00
      [ 319s ] thds: 128 tps: 132.00 qps: 1804.01 (r/w/o: 1017.01/505.00/282.00) lat (ms,99%): 3773.42 err/s: 18.00 reconn/s: 0.00
      [ 320s ] thds: 128 tps: 78.00 qps: 400.00 (r/w/o: 0.00/243.00/157.00) lat (ms,99%): 3448.53 err/s: 1.00 reconn/s: 0.00
      [ 321s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      [ 322s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      [ 323s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      [ 324s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      [ 325s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      [ 326s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      [ 327s ] thds: 128 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,99%): 0.00 err/s: 0.00 reconn/s: 0.00
      ```
      

   * When the nonblocking DDL feature is enabled, TPS decreases but does not drop to 0.

      ```SQL
      -- Enable nonblocking DDL
      set session enable_nonblock_ddl =1;
      alter table sbtest1 add index idx_k_4(k);
      
      [ 28s ] thds: 128 tps: 31.00 qps: 818.96 (r/w/o: 529.97/225.99/63.00) lat (ms,99%): 2159.29 err/s: 1.00 reconn/s: 0.00
      [ 29s ] thds: 128 tps: 24.00 qps: 410.99 (r/w/o: 263.99/95.00/52.00) lat (ms,99%): 7346.49 err/s: 4.00 reconn/s: 0.00
      [ 30s ] thds: 128 tps: 45.00 qps: 717.03 (r/w/o: 449.02/176.01/92.00) lat (ms,99%): 6026.41 err/s: 2.00 reconn/s: 0.00
      [ 31s ] thds: 128 tps: 65.00 qps: 1103.99 (r/w/o: 703.00/267.00/134.00) lat (ms,99%): 5033.35 err/s: 4.00 reconn/s: 0.00
      [ 32s ] thds: 128 tps: 47.00 qps: 844.00 (r/w/o: 540.00/203.00/101.00) lat (ms,99%): 6026.41 err/s: 7.00 reconn/s: 0.00
      [ 33s ] thds: 128 tps: 78.00 qps: 1245.97 (r/w/o: 783.98/301.99/160.00) lat (ms,99%): 6713.97 err/s: 4.00 reconn/s: 0.00
      [ 34s ] thds: 128 tps: 48.00 qps: 789.01 (r/w/o: 493.01/196.00/100.00) lat (ms,99%): 4683.57 err/s: 4.00 reconn/s: 0.00
      [ 35s ] thds: 128 tps: 45.00 qps: 873.02 (r/w/o: 593.02/183.00/97.00) lat (ms,99%): 7346.49 err/s: 7.00 reconn/s: 0.00
      [ 36s ] thds: 128 tps: 57.99 qps: 930.86 (r/w/o: 573.92/237.96/118.98) lat (ms,99%): 6476.48 err/s: 3.00 reconn/s: 0.00
      [ 37s ] thds: 128 tps: 91.01 qps: 1467.16 (r/w/o: 909.10/374.04/184.02) lat (ms,99%): 6713.97 err/s: 2.00 reconn/s: 0.00
      [ 38s ] thds: 128 tps: 69.00 qps: 1138.04 (r/w/o: 719.02/279.01/140.00) lat (ms,99%): 5409.26 err/s: 2.00 reconn/s: 0.00
      [ 39s ] thds: 128 tps: 40.00 qps: 698.97 (r/w/o: 453.98/162.99/82.00) lat (ms,99%): 3841.98 err/s: 2.00 reconn/s: 0.00
      [ 40s ] thds: 128 tps: 39.00 qps: 712.02 (r/w/o: 458.01/172.00/82.00) lat (ms,99%): 5312.73 err/s: 4.00 reconn/s: 0.00
      [ 41s ] thds: 128 tps: 38.00 qps: 618.01 (r/w/o: 386.01/153.00/79.00) lat (ms,99%): 7086.63 err/s: 3.00 reconn/s: 0.00
      [ 42s ] thds: 128 tps: 47.00 qps: 827.01 (r/w/o: 544.00/183.00/100.00) lat (ms,99%): 5607.61 err/s: 5.00 reconn/s: 0.00
      [ 43s ] thds: 128 tps: 42.00 qps: 709.99 (r/w/o: 450.00/172.00/88.00) lat (ms,99%): 6135.91 err/s: 4.00 reconn/s: 0.00
      [ 44s ] thds: 128 tps: 56.00 qps: 848.01 (r/w/o: 515.01/220.00/113.00) lat (ms,99%): 6247.39 err/s: 1.00 reconn/s: 0.00
      [ 45s ] thds: 128 tps: 80.00 qps: 1252.98 (r/w/o: 781.99/309.00/162.00) lat (ms,99%): 7215.39 err/s: 2.00 reconn/s: 0.00
      [ 46s ] thds: 128 tps: 49.00 qps: 918.02 (r/w/o: 615.01/201.00/102.00) lat (ms,99%): 8038.61 err/s: 4.00 reconn/s: 0.00
      [ 47s ] thds: 128 tps: 34.00 qps: 601.00 (r/w/o: 378.00/152.00/71.00) lat (ms,99%): 7086.63 err/s: 2.00 reconn/s: 0.00
      [ 48s ] thds: 128 tps: 52.00 qps: 855.00 (r/w/o: 525.00/221.00/109.00) lat (ms,99%): 5217.92 err/s: 5.00 reconn/s: 0.00
      [ 49s ] thds: 128 tps: 79.00 qps: 1268.94 (r/w/o: 798.96/308.99/160.99) lat (ms,99%): 5217.92 err/s: 3.00 reconn/s: 0.00
      [ 50s ] thds: 128 tps: 47.00 qps: 859.02 (r/w/o: 547.01/214.01/98.00) lat (ms,99%): 6835.96 err/s: 4.00 reconn/s: 0.00
      [ 51s ] thds: 128 tps: 66.00 qps: 1067.02 (r/w/o: 670.01/261.00/136.00) lat (ms,99%): 5607.61 err/s: 4.00 reconn/s: 0.00
      [ 52s ] thds: 128 tps: 44.00 qps: 815.01 (r/w/o: 539.00/184.00/92.00) lat (ms,99%): 7895.16 err/s: 4.00 reconn/s: 0.00
      [ 53s ] thds: 128 tps: 20.00 qps: 348.99 (r/w/o: 227.99/78.00/43.00) lat (ms,99%): 4683.57 err/s: 4.00 reconn/s: 0.00
      [ 54s ] thds: 128 tps: 53.00 qps: 878.00 (r/w/o: 552.00/218.00/108.00) lat (ms,99%): 9977.52 err/s: 1.00 reconn/s: 0.00
      [ 55s ] thds: 128 tps: 32.00 qps: 539.00 (r/w/o: 346.00/126.00/67.00) lat (ms,99%): 6835.96 err/s: 3.00 reconn/s: 0.00
      [ 56s ] thds: 128 tps: 35.00 qps: 593.01 (r/w/o: 374.01/147.00/72.00) lat (ms,99%): 6960.17 err/s: 2.00 reconn/s: 0.00
      ```
