---
title: "Scheduling policy configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Scheduling_policy_configuration"
---

When creating a virtual cluster or adding services to a running virtual cluster (such as creating a RayCluster), EMR service Pods can be scheduled onto nodes with specific labels. This document describes how to configure scheduling policies.

<span id="a0b30510"></span>
## Use cases and limitations


1. Schedule service Pods onto the desired server nodes, such as local disk servers.

2. Configure affinity and anti\-affinity for different service Pods. Currently, only JSON configuration is supported.


<span id="a13928a0"></span>
## Instructions

<span id="84432739"></span>
### Scenario 1: Configure scheduling policies when creating a virtual cluster

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating a virtual cluster, only scenarios where the resource type is an existing VKE resource support scheduling policy configuration.</div>



1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to **Resource Management \> on VKE tab**.

3. Click \*\*\*\* \*\*Create virtual cluster \*\* to enter the virtual cluster creation details page

4. Select the VKE cluster for EMR deployment and the service to be deployed. In the **Configure Pod Deployment** table **Scheduling policycolumn**, click **Settings** to enter the scheduling policy configuration page


<span id="ffa3eda9"></span>
### Scenario 2: Configure scheduling policies when adding a service


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to **Resource Management \> on VKE \> Virtual Cluster Details \>**  **Service list tab**.

3. Click \*\*\*\* **Add service** to enter the add service details page

4. Select the service to be deployed. In the **Configure Pod Deployment** table **Scheduling policycolumn**, click **Settings** to enter the scheduling policy configuration page.


<span id="9d69225f"></span>
## Common configuration policies


<Tabs>
<Tab zoneid="AuogxW1RBM" title="Pod调度到本地盘规格节点上">
<TabTitle>Pod调度到本地盘规格节点上</TabTitle>

```JSON
{
    "nodeAffinity": { 
        "requiredDuringSchedulingIgnoredDuringExecution": {
            "nodeSelectorTerms": [
                {
                    "matchExpressions": [
                        {
                            "key": "emr-local-disk",
                            "operator": "Exists"
                        }
                    ]
                }
            ]
        }
    }
}
```



</Tab>
<Tab zoneid="ZELBQOmMMS" title="Pod调度到指定A10 GPU卡上">
<TabTitle>Pod调度到指定A10 GPU卡上</TabTitle>

```JSON
{
    "nodeAffinity": {
        "requiredDuringSchedulingIgnoredDuringExecution": {
            "nodeSelectorTerms": [
                {
                    "matchExpressions": [
                        {
                            "key": "machine.cluster.vke.volcengine.com/gpu-name",
                            "operator": "In",
                            "values": [
                                    "NVIDIA-A10"
                                ]
                        }
                    ]
                }
            ]
        }
    }
}
```



</Tab>
<Tab zoneid="B7moCxrmre" title="SparkHistoryServer和CelebornWorker反亲和部署">
<TabTitle>SparkHistoryServer和CelebornWorker反亲和部署</TabTitle>

```JSON
{
    "nodeAffinity": {
        "preferredDuringSchedulingIgnoredDuringExecution": [
            {
                "weight": 1,
                "preference": {
                    "matchExpressions": [
                        {
                            "key": "emr-local-disk",
                            "operator": "DoesNotExist"
                        }
                    ]
                }
            }
        ]
    },
    "podAntiAffinity": {
        "preferredDuringSchedulingIgnoredDuringExecution": [
            {
                "weight": 1,
                "podAffinityTerm": {
                    "labelSelector": {
                        "matchExpressions": [
                            {
                                "key": "app.kubernetes.io/name",
                                "operator": "In",
                                "values": [
                                    "celeborn-worker"
                                ]
                            },
                            {
                                "key": "app.kubernetes.io/role",
                                "operator": "In",
                                "values": [
                                    "worker"
                                ]
                            }
                        ]
                    },
                    "topologyKey": "kubernetes.io/hostname"
                }
            }
        ]
    }
}
```



</Tab>
</Tabs>


<span id="cffc89e0"></span>
## EMR default scheduling policies

Different services have different default scheduling policies. This section lists the default Pod scheduling policies for each core EMR service component in detail.

<span id="37538d99"></span>
### RAY


<Tabs>
<Tab zoneid="nVr2hDxuQW" title="KubeRayOperator">
<TabTitle>KubeRayOperator</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
```



</Tab>
<Tab zoneid="c4HCqYXTVX" title="RayHistoryServer">
<TabTitle>RayHistoryServer</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
```



</Tab>
</Tabs>


<span id="2f9bffca"></span>
### Spark


<Tabs>
<Tab zoneid="J1W7PcJ8AS" title="SparkHistoryServer">
<TabTitle>SparkHistoryServer</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
<Tab zoneid="c8YvooU7Xd" title="SparkOperator">
<TabTitle>SparkOperator</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        },
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "spark-operator"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 100
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
</Tabs>


<span id="594378a4"></span>
### Celeborn


<Tabs>
<Tab zoneid="eAMO3b7d3U" title="CelebornMaster">
<TabTitle>CelebornMaster</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }，
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/cluster-role",
                  "operator": "In",
                  "values": [
                    "proton-data-server"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": [
        {
          "labelSelector": {
            "matchExpressions": [
              {
                "key": "app.kubernetes.io/name",
                "operator": "In",
                "values": [
                  "celeborn-master"
                ]
              },
              {
                "key": "app.kubernetes.io/role",
                "operator": "In",
                "values": [
                  "master"
                ]
              }
            ],
            "matchLabels": null
          },
          "namespaceSelector": null,
          "namespaces": null,
          "topologyKey": "kubernetes.io/hostname"
        }
      ]
    }
  }
```



</Tab>
<Tab zoneid="XDWvYs0D6l" title="CelebornWorker">
<TabTitle>CelebornWorker</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": null,
      "requiredDuringSchedulingIgnoredDuringExecution": {
        "nodeSelectorTerms": [
          {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "Exists",
                "values": null
              }
            ],
            "matchFields": null
          }
        ]
      }
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "emr/clusterId",
                  "operator": "Exists",
                  "values": null
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": [
        {
          "labelSelector": {
            "matchExpressions": [
              {
                "key": "app.kubernetes.io/name",
                "operator": "In",
                "values": [
                  "celeborn-worker"
                ]
              },
              {
                "key": "app.kubernetes.io/role",
                "operator": "In",
                "values": [
                  "worker"
                ]
              }
            ],
            "matchLabels": null
          },
          "namespaceSelector": null,
          "namespaces": null,
          "topologyKey": "kubernetes.io/hostname"
        },
        {
          "labelSelector": {
            "matchExpressions": [
              {
                "key": "app.kubernetes.io/cluster-role",
                "operator": "In",
                "values": [
                  "proton-data-server"
                ]
              }
            ],
            "matchLabels": null
          },
          "namespaceSelector": null,
          "namespaces": null,
          "topologyKey": "kubernetes.io/hostname"
        }
      ]
    }
  }
```



</Tab>
</Tabs>


<span id="c1c150a7"></span>
### Hive


<Tabs>
<Tab zoneid="xJhYoDLmBA" title="HiveMetaStore">
<TabTitle>HiveMetaStore</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        },
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "hive-metastore"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 100
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
</Tabs>


<span id="ff11d161"></span>
### Zookeeper


<Tabs>
<Tab zoneid="W8B7qc2Jvb" title="Zookeeper">
<TabTitle>Zookeeper</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": [
        {
          "labelSelector": {
            "matchExpressions": [
              {
                "key": "app",
                "operator": "In",
                "values": [
                  "zk"
                ]
              }
            ],
            "matchLabels": null
          },
          "namespaceSelector": null,
          "namespaces": null,
          "topologyKey": "kubernetes.io/hostname"
        }
      ]
    }
  }
```



</Tab>
</Tabs>


<span id="994dd9fd"></span>
### Kyuubi


<Tabs>
<Tab zoneid="Gb5CxkUrWl" title="KyuubiServer">
<TabTitle>KyuubiServer</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        },
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "kyuubi"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 100
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
</Tabs>


<span id="6f0fac24"></span>
### Volcano


<Tabs>
<Tab zoneid="qsIE5fDzXt" title="VolcanoAdmission">
<TabTitle>VolcanoAdmission</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        },
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "volcano-admission"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 100
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
<Tab zoneid="HWawWyqBbH" title="VolcanoControllerManager">
<TabTitle>VolcanoControllerManager</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        },
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "volcano-controller-manager"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 100
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
<Tab zoneid="sx1Dg8u76n" title="VolcanoScheduler">
<TabTitle>VolcanoScheduler</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/role",
                  "operator": "In",
                  "values": [
                    "worker"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        },
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "volcano-scheduler"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 100
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
</Tabs>


<span id="229c8248"></span>
### Proton


<Tabs>
<Tab zoneid="jN7coco9WU" title="ProtonDataServer">
<TabTitle>ProtonDataServer</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": null,
      "requiredDuringSchedulingIgnoredDuringExecution": {
        "nodeSelectorTerms": [
          {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "Exists",
                "values": null
              }
            ],
            "matchFields": null
          }
        ]
      }
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-master"
                  ]
                },
                {
                  "key": "app.kubernetes.io/cluster-role",
                  "operator": "In",
                  "values": [
                    "proton-meta-server"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": [
        {
          "labelSelector": {
            "matchExpressions": [
              {
                "key": "app.kubernetes.io/name",
                "operator": "In",
                "values": [
                  "celeborn-worker"
                ]
              },
              {
                "key": "app.kubernetes.io/cluster-role",
                "operator": "In",
                "values": [
                  "proton-data-server"
                ]
              }
            ],
            "matchLabels": null
          },
          "namespaceSelector": null,
          "namespaces": null,
          "topologyKey": "kubernetes.io/hostname"
        }
      ]
    }
  }
```



</Tab>
<Tab zoneid="U3fjZAihCU" title="ProtonMetaServer">
<TabTitle>ProtonMetaServer</TabTitle>

```JSON
"affinity": {
    "nodeAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "preference": {
            "matchExpressions": [
              {
                "key": "emr-local-disk",
                "operator": "DoesNotExist",
                "values": null
              }
            ],
            "matchFields": null
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    },
    "podAffinity": null,
    "podAntiAffinity": {
      "preferredDuringSchedulingIgnoredDuringExecution": [
        {
          "podAffinityTerm": {
            "labelSelector": {
              "matchExpressions": [
                {
                  "key": "app.kubernetes.io/name",
                  "operator": "In",
                  "values": [
                    "celeborn-worker"
                  ]
                },
                {
                  "key": "app.kubernetes.io/cluster-role",
                  "operator": "In",
                  "values": [
                    "proton-data-server"
                  ]
                }
              ],
              "matchLabels": null
            },
            "namespaceSelector": null,
            "namespaces": null,
            "topologyKey": "kubernetes.io/hostname"
          },
          "weight": 1
        }
      ],
      "requiredDuringSchedulingIgnoredDuringExecution": null
    }
  }
```



</Tab>
</Tabs>
