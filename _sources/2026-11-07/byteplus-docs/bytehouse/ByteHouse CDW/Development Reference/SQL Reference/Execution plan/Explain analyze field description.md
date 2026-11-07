---
title: "Explain analyze field description"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/explain-analyze-field-description"
---

<span id="2fe23ade"></span>
### Text format

```SQL
│ Segment[0]                                                                                          │
│    Output Exchange: Output                                                                          │
│    Parallel Size: 1, Cluster Name: test_shard_localhost, Exchange Parallel Size: 1                  │
│    Output Columns: [a, t2.b]                                                                        │
│       Gather Exchange segment[1] Est. ? rows                                                        │
│                                                                                                     │
│ Segment[1]                                                                                          │
│    Output Exchange: GATHER                                                                          │
│    Parallel Size: 1, Cluster Name: test_shard_localhost, Exchange Parallel Size: 1                  │
│    Outputs: [( SegmentID:0 PlanSegmentType:EXCHANGE ParallelSize:1 ShuffleFunctionName:cityHash64)] │
│    Output Columns: [a, t2.b]                                                                        │
│       Projection Est. ? rows                                                                        │
│       │     Expressions: a:=a_1, t2.b:=b_2                                                          │
│       └─ Inner Join Est. ? rows                                                                     │
│          │     Condition: a_1 == a_2                                                                │
│          ├─ Buffer Est. ? rows                                                                      │
│          │  └─ CTERef[0] <-- segment[2] Est. ? rows                                                 │
│          └─ Buffer Est. ? rows                                                                      │
│             └─ CTERef[0] <-- segment[2] Est. ? rows                                                 │
│                                                                                                     │
│ Segment[2]                                                                                          │
│    Output Exchange: REPARTITION[a, a]                                                               │
│    Parallel Size: 1, Cluster Name: test_shard_localhost, Exchange Parallel Size: 1                  │
│    Outputs: [( SegmentID:1 PlanSegmentType:EXCHANGE ParallelSize:1 ShuffleFunctionName:cityHash64)  │
│              ( SegmentID:1 PlanSegmentType:EXCHANGE ParallelSize:1 ShuffleFunctionName:cityHash64)] │
│    Output Columns: [a, b]                                                                           │
│       TableScan test.t48028 Est. ? rows                                                             │
│             Outputs: [a, b]                                                                         │
│
```



* Output Exchange: The current segment's data output method, representing how the current segment transmits data to the next segment. The methods include Output, LOCAL_NO_NEED_REPARTITION, LOCAL_MAY_NEED_REPARTITION, BROADCAST, REPARTITION, GATHER, UNKNOWN. When it is Repartition, shuffle keys will be displayed in brackets afterwards

* Output Columns: The column names output by the segment

* Outputs: Information on the current segment’s results output to the next segment

* Parallel size: The degree of parallelism of the current segment

* Cluster Name: Name of the cluster

* Exchange Parallel Size: Exchange parallel size

* Est.: Estimated information, based on statistical data on the estimated number of rows and cost

* Act. : Actual execution information, output: number of output lines, data size, wait time for outputting data, wall time: elapsed time for all operators. Input: number of input lines, data size, wait time for inputting data

* QError: The ratio of the actual output line count of the operator to the estimated line count based on statistical information

* Filtered: (Max input line count \- output line count) / Max input line count


Both Where and Condition are filters

<span id="80065e35"></span>
### JSON format

JSON form with statistical information removed

```SQL
{
 "DistributedPlan" : [
  {
   "SegmentID" : 2,
   "OutputExchangeMode" : "REPARTITION",
   "ShuffleKeys" : "REPARTITION",
   "ParallelSize" : 1,
   "ClusterName" : "test_shard_localhost",
   "ExchangeParallelSize" : 1,
   "OutputColumns" : [
    "a",
    "b"
   ],
   "Outputs" : [
    {
     "SegmentID" : 1,
     "PlanSegmentType" : "EXCHANGE",
     "ParallelSize" : 1,
     "ShuffleFunctionName" : "cityHash64"
    },
    {
     "SegmentID" : 1,
     "PlanSegmentType" : "EXCHANGE",
     "ParallelSize" : 1,
     "ShuffleFunctionName" : "cityHash64"
    }
   ],
   "QueryPlan" : {
    "NodeId" : 58,
    "NodeType" : "TableScan",
    "Outputs" : [
     "b",
     "a"
    ],
    "Profiles" : {
     "WallTimeMs" : 1,
     "OutputRows" : 3,
     "OutputBytes" : 24,
     "OutputWaitTimeMs" : 0,
     "Inputs" : [
      {
       "InputNodeId" : -1,
       "InputRows" : 0,
       "InputBytes" : 0,
       "InputWaitTimeMs" : 4
      }
     ],
     "FilteredRate" : 0
    }
   }
  },
  {
   "SegmentID" : 1,
   "OutputExchangeMode" : "GATHER",
   "ParallelSize" : 1,
   "ClusterName" : "test_shard_localhost",
   "ExchangeParallelSize" : 1,
   "OutputColumns" : [
    "a_1",
    "a_2",
    "b_2"
   ],
   "Outputs" : [
    {
     "SegmentID" : 0,
     "PlanSegmentType" : "EXCHANGE",
     "ParallelSize" : 1,
     "ShuffleFunctionName" : "cityHash64"
    }
   ],
   "QueryPlan" : {
    "NodeId" : 69,
    "NodeType" : "Join",
    "Strictness" : "",
    "JoinKind" : "Inner",
    "Condition" : [
     "a_1 == a_2"
    ],
    "Profiles" : {
     "WallTimeMs" : 1,
     "OutputRows" : 3,
     "OutputBytes" : 36,
     "OutputWaitTimeMs" : 0,
     "Inputs" : [
      {
       "InputNodeId" : 72,
       "InputRows" : 3,
       "InputBytes" : 12,
       "InputWaitTimeMs" : 75
      },
      {
       "InputNodeId" : 73,
       "InputRows" : 3,
       "InputBytes" : 24,
       "InputWaitTimeMs" : 72
      }
     ],
     "FilteredRate" : 0
    },
    "Children" : [
     {
      "NodeId" : 72,
      "NodeType" : "Buffer",
      "Profiles" : {
       "WallTimeMs" : 0,
       "OutputRows" : 3,
       "OutputBytes" : 12,
       "OutputWaitTimeMs" : 40,
       "Inputs" : [
        {
         "InputNodeId" : 75,
         "InputRows" : 3,
         "InputBytes" : 12,
         "InputWaitTimeMs" : 86
        }
       ],
       "FilteredRate" : 0
      },
      "Children" : [
       {
        "NodeId" : 75,
        "NodeType" : "Projection",
        "Expressions" : [
         "a_1:=a"
        ],
        "Profiles" : {
         "WallTimeMs" : 0,
         "OutputRows" : 3,
         "OutputBytes" : 12,
         "OutputWaitTimeMs" : 0,
         "Inputs" : [
          {
           "InputNodeId" : 65,
           "InputRows" : 3,
           "InputBytes" : 24,
           "InputWaitTimeMs" : 89
          }
         ],
         "FilteredRate" : 0
        },
        "Children" : [
         {
          "NodeId" : 65,
          "NodeType" : "RemoteExchangeSource",
          "Segment[2]" : [
           "a",
           "b"
          ],
          "Profiles" : {
           "WallTimeMs" : 0,
           "OutputRows" : 3,
           "OutputBytes" : 24,
           "OutputWaitTimeMs" : 5,
           "Inputs" : [
            {
             "InputNodeId" : -1,
             "InputRows" : 0,
             "InputBytes" : 0,
             "InputWaitTimeMs" : 55
            }
           ],
           "FilteredRate" : 0
          }
         }
        ]
       }
      ]
     },
     {
      "NodeId" : 73,
      "NodeType" : "Buffer",
      "Profiles" : {
       "WallTimeMs" : 0,
       "OutputRows" : 3,
       "OutputBytes" : 24,
       "OutputWaitTimeMs" : 0,
       "Inputs" : [
        {
         "InputNodeId" : 76,
         "InputRows" : 3,
         "InputBytes" : 24,
         "InputWaitTimeMs" : 74
        }
       ],
       "FilteredRate" : 0
      },
      "Children" : [
       {
        "NodeId" : 76,
        "NodeType" : "Projection",
        "Expressions" : [
         "a_2:=a",
         "b_2:=b"
        ],
        "Profiles" : {
         "WallTimeMs" : 0,
         "OutputRows" : 3,
         "OutputBytes" : 24,
         "OutputWaitTimeMs" : 0,
         "Inputs" : [
          {
           "InputNodeId" : 68,
           "InputRows" : 3,
           "InputBytes" : 24,
           "InputWaitTimeMs" : 76
          }
         ],
         "FilteredRate" : 0
        },
        "Children" : [
         {
          "NodeId" : 68,
          "NodeType" : "RemoteExchangeSource",
          "Segment[2]" : [
           "a",
           "b"
          ],
          "Profiles" : {
           "WallTimeMs" : 0,
           "OutputRows" : 3,
           "OutputBytes" : 24,
           "OutputWaitTimeMs" : 5,
           "Inputs" : [
            {
             "InputNodeId" : -1,
             "InputRows" : 0,
             "InputBytes" : 0,
             "InputWaitTimeMs" : 40
            }
           ],
           "FilteredRate" : 0
          }
         }
        ]
       }
      ]
     }
    ]
   }
  },
  {
   "SegmentID" : 0,
   "OutputExchangeMode" : "Output",
   "ParallelSize" : 1,
   "ClusterName" : "test_shard_localhost",
   "ExchangeParallelSize" : 1,
   "OutputColumns" : [
    "Explain Analyze"
   ],
   "QueryPlan" : {
    "NodeId" : 71,
    "NodeType" : "Projection",
    "Expressions" : [
     "Explain Analyze"
    ],
    "Children" : [
     {
      "NodeId" : 74,
      "NodeType" : "ExplainAnalyze",
      "Profiles" : {
       "WallTimeMs" : 0,
       "OutputRows" : 3,
       "OutputBytes" : 36,
       "OutputWaitTimeMs" : 0,
       "Inputs" : [
        {
         "InputNodeId" : 70,
         "InputRows" : 3,
         "InputBytes" : 36,
         "InputWaitTimeMs" : 110
        }
       ],
       "FilteredRate" : 0
      },
      "Children" : [
       {
        "NodeId" : 70,
        "NodeType" : "RemoteExchangeSource",
        "Segment[1]" : [
         "a_1",
         "a_2",
         "b_2"
        ],
        "Profiles" : {
         "WallTimeMs" : 105,
         "OutputRows" : 3,
         "OutputBytes" : 36,
         "OutputWaitTimeMs" : 0,
         "Inputs" : [
          {
           "InputNodeId" : -1,
           "InputRows" : 0,
           "InputBytes" : 0,
           "InputWaitTimeMs" : 7
          }
         ],
         "FilteredRate" : 0
        }
       }
      ]
     }
    ]
   }
  }
 ]
}
```



* NodeId: id of the plan node

* NodeType: type of the plan node

* Profiles: Profile information
