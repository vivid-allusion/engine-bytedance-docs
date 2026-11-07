---
title: "Performance whitepaper"
product: "Cache for Redis"
product_code: "redis"
section: "Document"
source: "https://docs.byteplus.com/en/docs/redis/performance-whitepaper"
---

This topic describes the detailed method and test results of stress testing on Cache for Redis instances using the `Memtier-benchmark` stress testing tool. You can conduct your own tests and comparisons according to the instructions in this article to quickly understand the performance of the database system.

## Test environment

|Project |Actual environment and scope of evidence |
|---|---|
|Redis version |Redis 7.0 |
|Instance type / Access |Active\-standby architecture; both `GET`/`SET` requests are routed through a unified private network proxy, RESP/TCP |
|Region/Availability Zone/Network |North China 2 (Beijing), Availability Zone A, same VPC. |
|Memory/Number per shard |2GiB; 2, 4, 8, 16 shards, with a total memory of 4, 8, 16, 32 GiB |
|ECS Specs/OS |`ecs.g3i.8xlarge`、32 vCPU / 128 GiB、Debian 12 |
|Tools |`memtier_benchmark` 2.5.2 |

## Testing tools

`Memtier-benchmark` is used in this test. `Memtier-benchmark` is the command line tool developed by Redis Labs. It can be used for load generation and benchmark testing of non\-relational, key\-value databases. It is the official benchmark tool provided by Redis.Memtier\-benchmark is a command\-line tool developed by Redis Labs for load generation and benchmarking of non\-relational key\-value databases, and is the official benchmarking tool provided by Redis.

For information on how to download and install `Memtier-benchmark` tools, refer to [Memtier-benchmark](https://github.com/RedisLabs/memtier_benchmark#prerequisites).

## Test commands

Three scenarios: pure `GET`, pure `SET`, and SET:GET=1:1; with a fixed key range and access distribution, the `GET` hit rate is confirmed after pre\-filling.

|Parameters |Test settings |
|---|---|
|Operation ratio |Pure GET: `--ratio=0:1`; Pure SET: `--ratio=1:0`; Mixed: `--ratio=1:1` |
|Data size |Baseline Value is 32 B |
|Pipeline |Baseline `--pipeline=1` |
|Connections and threads |`-c` is the number of connections per thread, `-t` is the number of threads per process; Total connections = Number of ECS instances × Number of processes per instance × `t` × `c` |
|Test duration |180s warm\-up; 600s official test, repeated for 3 rounds |

## Test results

### Benchmark testing for typical scenarios

Typical scenario benchmark: Value 32B, Pipeline=1.

#### **Test results**

![图片](https://internal-api-drive-stream.larkoffice.com/space/api/box/stream/download/authcode/?code=ZTU0NTVlMTNmNmIwNTQ5MjQ2MWQ3NmYxZDVmNTFkNTdfOTI0ZGJmNmVhMWY4ZmFjNmM1NTQ2Zjg4OTIwMGMyZWFfSUQ6NzcwNDE5MzE5NDkzNDYwMzAxOV8xNzkzNzcyNDEwOjE3OTM4NTg4MTBfVjM)

![图片](https://internal-api-drive-stream.larkoffice.com/space/api/box/stream/download/authcode/?code=MDA0MTgxMDJjNTRiZWFiZjQ3NTQyZDllNGI5OTVjMjlfMGU4ZTc5OTkwOWI3ZGQzNjc4ZDE4OTNmNWVmYTY3ZGJfSUQ6NzcwNDE5MzE5NzcxNDQ5MjcxMF8xNzkzNzcyNDEwOjE3OTM4NTg4MTBfVjM)

|Number of shard(s) |Scenario |Total QPS |Single shard QPS |Connection configuration |
|---|---|---|---|---|
|2 |Pure GET |944,700 |472,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|2 |Pure SET |596,000 |297,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|2 |SET:GET = 1 : 1 |720,000 |360,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|4 |Pure GET |1,861,000 |465,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|4 |Pure SET |1,137,000 |284,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|4 |SET:GET = 1 : 1 |1,367,000 |342,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|8 |Pure GET |3,366,000 |420,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|8 |Pure SET |2,074,000 |259,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|8 |SET:GET = 1 : 1 |2,507,000 |313,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|16 |Pure GET |5,738,000 |358,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |
|16 |Pure SET |3,742,000 |234,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |
|16 |SET:GET = 1 : 1 |4,428,000 |277,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |

### Pipeline test

Value is 32B, SET:GET=1:1; each shard specification maintains a constant connection configuration, comparing Pipeline depths of 1, 4, 16, 64.

#### Test results

![图片](https://internal-api-drive-stream.larkoffice.com/space/api/box/stream/download/authcode/?code=Mzc0MDIzZmM2MmQ2ZDhkZGMxM2FjZjFkODY3NmM3YjFfMjc5YjQ0ZTVlN2IwN2UyOGNlMjZmN2Y4YWUwYTljYmRfSUQ6NzcwNDE5MzY3ODYyMzE2NTcwMl8xNzkzNzcyNDEwOjE3OTM4NTg4MTBfVjM)

![图片](https://internal-api-drive-stream.larkoffice.com/space/api/box/stream/download/authcode/?code=YWYzN2E3YjM4OThiNTljZjkzODBkZGQ5MDFkYTJmOGNfNjM5MmU4Yjk5Y2M3ZWJhM2MzOGIzNDgyYmQxOGI5YzZfSUQ6NzcwNDE5MzY4MzQwNjgwMjE2Nl8xNzkzNzcyNDEwOjE3OTM4NTg4MTBfVjM)

|Number of shard(s) |Scenario |Total QPS |Single shard QPS |Connection configuration |
|---|---|---|---|---|
|2 |Pipeline = 1 |720,000 |360,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|2 |Pipeline = 4 |812,000 |406,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|2 |Pipeline = 16 |978,000 |489,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|2 |Pipeline = 64 |974,000 |487,000 |1 ECS instance, `-t 20 -c 100`, totaling 2,000 connections |
|4 |Pipeline = 1 |1,367,000 |342,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|4 |Pipeline = 4 |1,693,000 |423,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|4 |Pipeline = 16 |1,872,000 |468,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|4 |Pipeline = 64 |1,927,000 |482,000 |2 ECS instances, `-t 20 -c 100`, totaling of 4000 connections |
|8 |Pipeline = 1 |2,507,000 |313,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|8 |Pipeline = 4 |3,278,000 |409,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|8 |Pipeline = 16 |3,390,000 |423,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|8 |Pipeline = 64 |3,727,000 |465,000 |4 ECS instances, `-t 20 -c 100`, totaling of 8000 connections |
|16 |Pipeline = 1 |4,428,000 |277,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |
|16 |Pipeline = 4 |5,854,000 |366,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |
|16 |Pipeline = 16 |6,560,000 |410,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |
|16 |Pipeline = 64 |7,184,000 |449,000 |8 ECS instances, `-t 20 -c 100`, totaling 16,000 connections |

### Customer self\-test guide

Customer self\-test  steps:

1. Prepare independent stress test ECS and test instances in the same region, availability zone, and VPC. Confirm the private network Proxy address, authentication, version, sharding, persistence configuration, and tool version.

2. Pre\-fill data within a fixed key range; pure `GET` operations require pre\-filling first.

3. Each ECS executes the same scenario parameters, first warming up for 180 seconds, then simultaneously starting three rounds of independent 600\-second tests and saving the results separately.

4. Summarize the total QPS and GET hit rate for each ECS per round, and observe the CPU and network of the Proxy, Redis primary shards, and ECS.

   ```Bash
   memtier_benchmark -s <proxy-address> -p 6379 \
     -c <connections per thread> -t <Threads per process> \
     --ratio=1:1 --select-db=0 --test-time=600 \
     -d 32 --pipeline=1 \
     --key-minimum=1 --key-maximum=<Limit for pre-populated keys> \
     --key-pattern=R:R \
     -a <password>
   ```

   Replace corresponding parameters for pure `GET`, pure `SET`, and Pipeline scenarios.
