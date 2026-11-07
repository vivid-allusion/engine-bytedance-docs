---
title: "Description of the Explain Analyze Field"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/description-of-the-explain-analyze-field"
---

The output of the EXPLAIN ANALYZE statement can be displayed in either Text or JSON format. This article presents two types of output examples and explains the meaning of the operators in these examples.

<span id="87dd71b2"></span>
# Text format

<span id="90b7ff47"></span>
## Example

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


<span id="f7c25f9f"></span>
## Operator meaning


* Output Exchange: The method used by the current segment to output data represents the form in which its data is transmitted to the next segment. Supported forms include Output, LOCAL_NO_NEED_REPARTITION, LOCAL_MAY_NEED_REPARTITION, BROADCAST, REPARTITION, GATHER, and UNKNOWN. When the form is Repartition, the shuffle keys are displayed in square brackets following Repartition.

* The name of the column output by segment.

* Outputs: The results of the current segment are output to the next segment information.

* Parallel size: The parallelism of the current segment.

* Cluster name: The name of your cluster.

* Exchange parallel size: The size of exchange parallel.

* Est.: Estimated information, namely the number of rows and cost calculated based on statistical information.

* Act.: Actual execution information, including the following information:

   * Output: number of output rows, data size

   * wait time: The time to wait when outputting data.

   * Wall time: Elapsed time for all operators

   * Input: Number of rows, data size, wait time (the time to wait when entering data).

* QError: The ratio of the actual number of rows output by an operator to the number of rows estimated based on statistical information.

* Filtered: The calculation formula is (maximum number of input rows \- number of output rows) / maximum number of input rows.

* Both Where and Condition are filtering criteria.


<span id="42c3e5cb"></span>
# JSON format

Statistical information has been removed from the JSON format.

<span id="ea926720"></span>
## Example

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


<span id="ffa8c858"></span>
## Operator meaning


* NodeId: ID of the plan node.

* NodeType: The type of a plan node.

* Profiles: Profile information.
