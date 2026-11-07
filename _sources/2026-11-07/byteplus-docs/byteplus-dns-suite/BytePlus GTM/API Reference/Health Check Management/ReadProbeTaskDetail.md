---
title: "ReadProbeTaskDetail"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ReadProbeTaskDetail"
---

Gets the details of a health check task by task ID.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=ReadProbeTaskDetail&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ReadProbeTaskDetail` |The name of the API. The value of this parameter is `ReadProbeTaskDetail`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|ProbeTaskId |Integer |Yes |`24277793` |ID of the health check task. Call [ListProbeTaskIds](https://docs.byteplus.com/en/docs/byteplus-dns-suite/ListProbeTaskIds) to get the ID of a health check task. |
|PageNumber |Integer |No |`1` |The page number. Default is 1. The maximum value is 100. The number of pages is determined by the total number of health check tasks retrieved and the `PageSize`. |
|PageSize |Integer |No |`10` |The number of GTM instances per page. Default is 10. The maximum value is 1000.<br><br>BytePlus GTM will display the retrieved health check tasks in pages. The number of pages is determined by the total number of health check tasks retrieved and the `PageSize`. |
|StartTime |Integer |Yes |`1639548697` |The start time. The format is a Unix timestamp in seconds. |
|EndTime |Integer |Yes |`1639548697` |The end time. The format is a Unix timestamp in seconds. The time span between `StartTime` and `EndTime` must not exceed 3 days. |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|TotalCount |Integer |The total number of tasks. |
|PageNumber |Integer |Page number for pagination. |
|PageSize |Integer |Number of tasks per page. |
|Data |JSON Object |Details of each health check task. |
|CommonData |Object |Tasks ID, health check probe information and the time when the health check task starts. |
|Id |Integer |ID of the health check task. |
|ClientInfo |Object |Health check probe information. |
|City |String |The city where the health check probe is located. |
|Ip |String |IPv4 address of the health check probe. |
|Ipv6 |String |IPv6 address of the health check probe. |
|Isp |String |ISP of the health check probe. |
|Region |String |Region of the health check probe. |
|Timestamp |Integer |The time when the health check result is returned to BytePlus GTM. |
|Log |Object |Health check result. TCP health check tasks utilize TCP Ping while Ping health check tasks utilize ICMP Ping. Therefore, the API returns the same result for both Ping and TCP health check tasks. |
|PingAvgCost |String |Average round trip time (RTT) of the ping test in milliseconds. This parameter is returned only when the protocol is set to ping or tcp. |
|PingDetail |String |Detailed information of the ping test in milliseconds. This parameter is returned only when the protocol is set to ping or tcp. |
|PingLossRatePerDetect |String |Packet loss rate of the ping test in milliseconds. This parameter is returned only when the protocol is set to ping or tcp. |
|HttpCode |String |HTTP status code. A value of `--` indicates HTTP request timeout. This parameter is returned only when the protocol is set to http or https. |
|HttpDns |String |The time it costs to complete the DNS query in milliseconds. This parameter is returned only when the protocol is set to http or https. |
|HttpSsl |String |The time it costs to establish an SSL connection in milliseconds. This parameter is returned only when the protocol is set to http or https. |
|HttpTcp |String |The time it costs to establish a TCP connection in milliseconds. This parameter is returned only when the protocol is set to http or https. |
|HttpTotal |String |Round trip time (RTT) of the HTTP request in milliseconds. This parameter is returned only when the protocol is set to http or https. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=ReadProbeTaskDetail&Version=2023-01-01&EndTime=1747735097&ProbeTaskId=24236263&StartTime=1747735068
```

### Response example

#### Ping and TCP tasks

TCP health check tasks utilize TCP Ping while Ping health check tasks utilize ICMP Ping. Therefore, the API returns the same result for both Ping and TCP health check tasks.

```json
{
  "ResponseMetadata": {
    "RequestId": "20240722065033A59118D3AD7C1B0B6628",
    "Action": "ReadProbeTaskDetail",
    "Version": "2023-01-01",
    "Service": "gtm",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 360,
    "PageNumber": 1,
    "PageSize": 10,
    "Data": [
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "101.226.**.***",
            "Ipv6": "240e:96c:200:****:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748500944
        },
        "Log": {
          "PingAvgCost": "337",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=54 time=289.341ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=54 time=302.738ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=54 time=323.532ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=54 time=382.554ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=54 time=329.71ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=54 time=399.056ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=54 time=342.002ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=54 time=328.088ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 8 packets received, 20% loss\nround-trip min/avg/max/stddev = 289.34/337.13/399.06/34.84ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0.20"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Guangzhou",
            "Ip": "118.145.***.*",
            "Ipv6": "",
            "Isp": "China Mobile",
            "Region": "Guangdong"
          },
          "Timestamp": 1748500943
        },
        "Log": {
          "PingAvgCost": "183",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=47 time=183.031ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=47 time=183.081ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=47 time=183.104ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=47 time=183.055ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=47 time=183.073ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=47 time=183.101ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=47 time=183.131ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=47 time=183.12ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=47 time=183.109ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=47 time=183.035ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 183.03/183.08/183.13/0.03ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "140.207.***.**",
            "Ipv6": "2408:870c:1000:5:****:*:***:**",
            "Isp": "China Unicom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748500942
        },
        "Log": {
          "PingAvgCost": "177",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=54 time=176.903ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=54 time=179.813ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=54 time=176.916ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=54 time=179.216ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=54 time=177.069ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=54 time=176.859ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=54 time=176.963ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=54 time=176.83ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=54 time=176.935ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=54 time=176.921ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 176.83/177.44/179.81/1.05ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Guangzhou",
            "Ip": "183.240.***.**",
            "Ipv6": "2409:8c54:b010:**:****:*:***:**",
            "Isp": "China Mobile",
            "Region": "Guangdong"
          },
          "Timestamp": 1748500942
        },
        "Log": {
          "PingAvgCost": "43",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=51 time=53.298ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=51 time=42.764ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=51 time=42.924ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=51 time=42.811ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=51 time=42.755ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=51 time=42.727ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=51 time=42.836ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=51 time=42.972ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=51 time=42.748ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=51 time=42.816ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 42.73/43.87/53.30/3.14ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "140.207.***.**",
            "Ipv6": "2408:870c:1000:5:****:*:***:**",
            "Isp": "China Unicom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748500942
        },
        "Log": {
          "PingAvgCost": "176",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=54 time=176.834ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=54 time=176.892ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=54 time=176.902ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=54 time=176.919ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=54 time=176.849ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=54 time=176.953ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=54 time=176.99ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=54 time=176.833ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=54 time=176.852ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=54 time=176.943ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 176.83/176.90/176.99/0.05ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "101.226.**.***",
            "Ipv6": "240e:96c:200:5500:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748500941
        },
        "Log": {
          "PingAvgCost": "369",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=54 time=275.646ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=54 time=397.435ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=54 time=288.926ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=54 time=390.617ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=54 time=393.212ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=54 time=383.149ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=54 time=379.094ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=54 time=399.125ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=54 time=393.08ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=54 time=392.252ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 275.65/369.25/399.12/43.95ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "101.226.**.***",
            "Ipv6": "240e:96c:200:5500:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748500885
        },
        "Log": {
          "PingAvgCost": "355",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=54 time=317.692ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=54 time=281.218ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=54 time=392.682ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=54 time=347.081ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=54 time=388.829ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=54 time=330.82ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=54 time=390.65ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=54 time=357.322ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=54 time=395.042ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 9 packets received, 10% loss\nround-trip min/avg/max/stddev = 281.22/355.70/395.04/37.89ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0.10"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Guangzhou",
            "Ip": "183.240.***.**",
            "Ipv6": "2409:8c54:b010:10:****:*:***:**",
            "Isp": "China Mobile",
            "Region": "Guangdong"
          },
          "Timestamp": 1748500883
        },
        "Log": {
          "PingAvgCost": "42",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=51 time=42.835ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=51 time=42.848ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=51 time=42.705ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=51 time=42.788ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=51 time=42.737ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=51 time=42.713ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=51 time=42.733ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=51 time=42.751ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=51 time=42.795ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=51 time=42.737ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 42.71/42.76/42.85/0.05ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Guangzhou",
            "Ip": "118.145.***.***",
            "Ipv6": "",
            "Isp": "China Mobile",
            "Region": "Guangdong"
          },
          "Timestamp": 1748500882
        },
        "Log": {
          "PingAvgCost": "180",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=46 time=180.14ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=46 time=180.095ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=46 time=180.148ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=46 time=180.397ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=46 time=180.194ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=46 time=180.077ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=46 time=180.112ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=46 time=180.165ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=46 time=180.078ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=46 time=180.102ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 180.08/180.15/180.40/0.09ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      },
      {
        "CommonData": {
          "Id": 24280097,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "101.226.**.***",
            "Ipv6": "240e:96c:200:5500:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748500882
        },
        "Log": {
          "PingAvgCost": "365",
          "PingDetail": "PING 10.11.***.***(10.11.***.***) 32 bytes of data\n40 bytes from 10.11.***.***: icmp_seq=0 ttl=54 time=315.729ms\n40 bytes from 10.11.***.***: icmp_seq=1 ttl=54 time=335.038ms\n40 bytes from 10.11.***.***: icmp_seq=2 ttl=54 time=384.914ms\n40 bytes from 10.11.***.***: icmp_seq=3 ttl=54 time=397.701ms\n40 bytes from 10.11.***.***: icmp_seq=4 ttl=54 time=385.979ms\n40 bytes from 10.11.***.***: icmp_seq=5 ttl=54 time=391.727ms\n40 bytes from 10.11.***.***: icmp_seq=6 ttl=54 time=315.864ms\n40 bytes from 10.11.***.***: icmp_seq=7 ttl=54 time=391.514ms\n40 bytes from 10.11.***.***: icmp_seq=8 ttl=54 time=351.984ms\n40 bytes from 10.11.***.***: icmp_seq=9 ttl=54 time=381.347ms\n--- 10.11.***.*** ping statistics ---\n10 packets sent, 10 packets received, 0% loss\nround-trip min/avg/max/stddev = 315.73/365.18/397.70/30.82ms\ndns lookup time 0ms",
          "PingLossRatePerDetect": "0"
        }
      }
    ]
  }
}
```

#### HTTP and HTTPS tasks

```json
{
  "ResponseMetadata": {
    "RequestId": "20240722065033A59118D3AD7C1B0B6628",
    "Action": "ReadProbeTaskDetail",
    "Version": "2023-01-01",
    "Service": "gtm",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 959,
    "PageNumber": 1,
    "PageSize": 10,
    "Data": [
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Harbin",
            "Ip": "42.101.**.***",
            "Ipv6": "240e:908:10a:0:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Heilongjiang"
          },
          "Timestamp": 1748518881
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3991",
          "HttpTotal": "3991"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Shanghai",
            "Ip": "101.226.41.150",
            "Ipv6": "240e:96c:200:5500:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Shanghai"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Xining",
            "Ip": "118.213.***.***",
            "Ipv6": "240e:90:2006:2:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Qinghai"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Xining",
            "Ip": "118.213.***.***",
            "Ipv6": "240e:90:2006:2:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Qinghai"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Chongqing",
            "Ip": "219.151.***.***",
            "Ipv6": "240e:930:c200:205:****:*:***:**",
            "Isp": "China Telecom",
            "Region": "Chongqing"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Dalian",
            "Ip": "42.202.***.***",
            "Ipv6": "240e:90c:a201:100:****:*:***:*",
            "Isp": "China Telecom",
            "Region": "Liaoning"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Guangzhou",
            "Ip": "125.94.**.***",
            "Ipv6": "240e:97c:**:***::***:***",
            "Isp": "China Telecom",
            "Region": "Guangdong"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Chongqing",
            "Ip": "219.151.***.***",
            "Ipv6": "240e:930:c200:205:****:*:***:18",
            "Isp": "China Telecom",
            "Region": "Chongqing"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Dalian",
            "Ip": "42.202.***.***",
            "Ipv6": "240e:90c:a201:100:****:*:***:8",
            "Isp": "China Telecom",
            "Region": "Liaoning"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      },
      {
        "CommonData": {
          "Id": 24294732,
          "ClientInfo": {
            "City": "Beijing",
            "Ip": "220.181.**.***",
            "Ipv6": "240e:904:800:1480::***:18",
            "Isp": "China Telecom",
            "Region": "Beijing"
          },
          "Timestamp": 1748518880
        },
        "Log": {
          "HttpCode": "--",
          "HttpDns": "0",
          "HttpSsl": "0",
          "HttpTcp": "3990",
          "HttpTotal": "3990"
        }
      }
    ]
  }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
