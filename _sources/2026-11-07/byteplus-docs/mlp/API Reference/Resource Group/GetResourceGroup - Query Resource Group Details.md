---
title: "GetResourceGroup - Query Resource Group Details"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/GetResourceGroup_-_Query_Resource_Group_Details"
---

Query Resource Group Details

## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

```mixin-react
const columns = [ 
  { 
    width: '20%', 
title: 'Parameter', 
    dataIndex: 'Name', 
    className: 'openapi-doc-parameter-table-name' 
  }, 
  { 
    width: 130, 
title: 'type', 
    dataIndex: 'DataType', 
    className: 'openapi-doc-parameter-table-type' 
  }, 
  { 
    width: 90, 
title: 'Required', 
    dataIndex: 'IsRequired', 
    className: 'openapi-doc-parameter-table-required' 
  }, 
  { 
    width: '20%', 
title: 'Example Value', 
    dataIndex: 'Example', 
    className: 'openapi-doc-parameter-table-example' 
  }, 
  { 
title: 'description', 
    dataIndex: 'Description', 
    className: 'openapi-doc-parameter-table-description' 
  }, 
]; 

const data = [ 
  { 
    rowKey: '->Action', 
    Name: 'Action', 
    DataType: 'String', 
IsRequired: 'Yes', 
    Example: <RenderMd content={"GetResourceGroup"} />, 
Description: <RenderMd content={"The action to perform. Value: GetResourceGroup."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Version', 
    Name: 'Version', 
    DataType: 'String', 
IsRequired: 'Yes', 
    Example: <RenderMd content={"2024-07-01"} />, 
Description: <RenderMd content={"API version; value: 2024-07-01."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Id', 
    Name: 'Id', 
    DataType: 'String', 
IsRequired: 'Yes', 
    Example: <RenderMd content={"r-20240923155410-*****"} />, 
Description: <RenderMd content={"Resource Group ID"} /> 
    children: [ 
    ] 
  }, 

]; 

return (<Table 
  rowKey="rowKey" 
  className="openapi-doc-parameter-table" 
  columns={columns} 
  data={data} 
  border={ { cell: true, wrapper: true } } 
  scroll={ { x: "auto" } } 
  pagination={false} 
/>);
```

## Response parameters

The following table describes only the specific response parameters of this API. For more information, see [Response Response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

```mixin-react
const columns = [ 
  { 
    width: '25%', 
title: 'parameter', 
    dataIndex: 'Name', 
    className: 'openapi-doc-parameter-table-name', 
  }, 
  { 
    width: 130, 
title: 'type', 
    dataIndex: 'DataType', 
    className: 'openapi-doc-parameter-table-type' 
  }, 
  { 
    width: '25%', 
title: 'Example Value', 
    dataIndex: 'Example', 
    className: 'openapi-doc-parameter-table-example' 
  }, 
  { 
title: 'description', 
    dataIndex: 'Description', 
    className: 'openapi-doc-parameter-table-description' 
  }, 
]; 

const data = [ 
  { 
    rowKey: "->Id", 
    Name: "Id", 
    DataType: "String", 
    Example: <RenderMd content={"r-20240923155410-*****"} />, 
Description: <RenderMd content={"Resource Group ID"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->Name", 
    Name: "Name", 
    DataType: "String", 
Example: <RenderMd content={"Test Resource Group"} /> 
Description: <RenderMd content={"resource group name"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->Description", 
    Name: "Description", 
    DataType: "String", 
Example: <RenderMd content={"This resource group is for testing"} /> 
Description: <RenderMd content={"resource group description"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->Status", 
    Name: "Status", 
    DataType: "Object", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"status"} /> 
    children: [ 
        { 
          rowKey: "->Status->State", 
          Name: "State", 
          DataType: "String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"state"} />," 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Status->SecondaryState", 
          Name: "SecondaryState", 
          DataType: "String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"secondary state"} /> 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Status->Message", 
          Name: "Message", 
          DataType: "String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"status information"} /> 
          children: [ 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: "->ZoneIds", 
    Name: "ZoneIds", 
    DataType: "Array of String", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"availability zone ID list"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->ResourceCapability", 
    Name: "ResourceCapability", 
    DataType: "Object", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Total Resources"} /> 
    children: [ 
        { 
          rowKey: "->ResourceCapability->ComputeResources", 
          Name: "ComputeResources", 
          DataType: "Array of Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group compute resources"} /> 
          children: [ 
            { 
              rowKey: "->ResourceCapability->ComputeResources->InstanceTypeId", 
              Name: "InstanceTypeId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource specification ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceCapability->ComputeResources->Count", 
              Name: "Count", 
              DataType: 'Integer', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource instance count"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceCapability->ComputeResources->ZoneId", 
              Name: "ZoneId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource availability zone ID"} /> , 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->ResourceCapability->VolumeResources", 
          Name: "VolumeResources", 
          DataType: "Array of Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource group cloud disk resources"} />, 
          children: [ 
            { 
              rowKey: "->ResourceCapability->VolumeResources->VolumeTypeId", 
              Name: "VolumeTypeId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud Drive type ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceCapability->VolumeResources->Size", 
              Name: "Size", 
              DataType: 'Integer', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud disk capacity, unit GiB"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceCapability->VolumeResources->ZoneId", 
              Name: "ZoneId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource Availability Zone ID"} /> 
              children: [ 
              ] 
            }, 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: "->ResourceAllocated", 
    Name: "ResourceAllocated", 
    DataType: "Object", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"allocated resource amount"} /> 
    children: [ 
        { 
          rowKey: "->ResourceAllocated->ComputeResources", 
          Name: "ComputeResources", 
          DataType: "Array of Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group compute resources"} /> 
          children: [ 
            { 
              rowKey: "->ResourceAllocated->ComputeResources->InstanceTypeId", 
              Name: "InstanceTypeId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource specification ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceAllocated->ComputeResources->Count", 
              Name: "Count", 
              DataType: 'Integer', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"number of resource instances"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceAllocated->ComputeResources->ZoneId", 
              Name: "ZoneId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource availability zone ID"} />, 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->ResourceAllocated->VolumeResources", 
          Name: "VolumeResources", 
          DataType: "Array of Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group cloud disk resources"} /> 
          children: [ 
            { 
              rowKey: "->ResourceAllocated->VolumeResources->VolumeTypeId", 
              Name: "VolumeTypeId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"cloud disk type ID"} />," 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceAllocated->VolumeResources->Size", 
              Name: "Size", 
              DataType: 'Integer', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud disk capacity, unit GiB"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->ResourceAllocated->VolumeResources->ZoneId", 
              Name: "ZoneId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource availability zone ID"} /> 
              children: [ 
              ] 
            }, 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: "->ChargeType", 
    Name: "ChargeType", 
    DataType: "String", 
    Example: <RenderMd content={"PrePaid"} />, 
Description: <RenderMd content={"Billing Mode"} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->PeriodUnit", 
    Name: "PeriodUnit", 
    DataType: "String", 
    Example: <RenderMd content={"Month"} />, 
Description: <RenderMd content={"purchase period unit"} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->ExpireTime", 
    Name: "ExpireTime", 
    DataType: "String", 
    Example: <RenderMd content={"2020-05-20T13:00:55Z"} />, 
Description: <RenderMd content={"Expiration time. Follows the YYYY-MM-DD'T'HH:MM:SS'Z' format."} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->RenewType", 
    Name: "RenewType", 
    DataType: "Integer", 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"Renewal type. 1 for manual renewal, 2 for automatic renewal."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->AutoRenewPeriod", 
    Name: "AutoRenewPeriod", 
    DataType: "Integer", 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"number of renewal cycles for single-time automatic renewal"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->RemainAutoRenewTimes", 
    Name: "RemainAutoRenewTimes", 
    DataType: "Integer", 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"The remaining number of renewals. If it is -1, it means unlimited and will continue to perform Automatic renewal actions."} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->StorageConfig", 
    Name: "StorageConfig", 
    DataType: "Object", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Storage configuration"} />, 
    children: [ 
        { 
          rowKey: "->StorageConfig->StorageNetworkConfig", 
          Name: "StorageNetworkConfig", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Storage Network Configuration"} />, 
          children: [ 
            { 
              rowKey: "->StorageConfig->StorageNetworkConfig->VpcId", 
              Name: "VpcId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user's private network"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->StorageNetworkConfig->SubnetIds", 
              Name: "SubnetIds", 
              DataType: 'Array of String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user subnet list"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->StorageNetworkConfig->SecurityGroupIds", 
              Name: "SecurityGroupIds", 
              DataType: 'Array of String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User Security Group List"} /> 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->StorageConfig->Sfcs", 
          Name: "Sfcs", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS configuration"} /> 
          children: [ 
            { 
              rowKey: "->StorageConfig->Sfcs->Name", 
              Name: "Name", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance name"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Sfcs->Id", 
              Name: "Id", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Sfcs->Replicas", 
              Name: "Replicas", 
              DataType: 'Long', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"number of write data replicas"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Sfcs->Description", 
              Name: "Description", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance description"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Sfcs->Status", 
              Name: "Status", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance status"} />," 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Sfcs->ZoneId", 
              Name: "ZoneId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance availability zone ID"} />,, 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->StorageConfig->Vepfs", 
          Name: "Vepfs", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS configuration"} />," 
          children: [ 
            { 
              rowKey: "->StorageConfig->Vepfs->MountServiceId", 
              Name: "MountServiceId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS mount service ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Vepfs->FileSystemIds", 
              Name: "FileSystemIds", 
              DataType: 'Array of String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS File System ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Vepfs->UnavailableNodeCount", 
              Name: "UnavailableNodeCount", 
              DataType: 'Integer', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Unavailable Node Count"} />," 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->StorageConfig->Vepfs->PrefetchEnabled", 
              Name: "PrefetchEnabled", 
              DataType: 'Boolean', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Whether to turn on client prefetch"} />," 
              children: [ 
              ] 
            }, 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: "->WorkloadNetworkConfig", 
    Name: "WorkloadNetworkConfig", 
    DataType: "Object", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"load private network configuration"} />, 
    children: [ 
        { 
          rowKey: "->WorkloadNetworkConfig->VpcId", 
          Name: "VpcId", 
          DataType: "String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user private network"} />, 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->WorkloadNetworkConfig->SubnetIds", 
          Name: "SubnetIds", 
          DataType: "Array of String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User Subnet List"} />, 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->WorkloadNetworkConfig->SecurityGroupIds", 
          Name: "SecurityGroupIds", 
          DataType: "Array of String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User Security Group List"} />," 
          children: [ 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: "->MGpuEnabled", 
    Name: "MGpuEnabled", 
    DataType: "Boolean", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"use mGPU function"} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->WorkloadNetworkMode", 
    Name: "WorkloadNetworkMode", 
    DataType: "String", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Workload Network Mode, optional values: SingleNIC, DualNIC"} /> 
    children: [ 
    ] 
  }, 
]; 

return (<Table 
  rowKey="rowKey" 
  className="openapi-doc-parameter-table" 
  columns={columns} 
  data={data} 
  border={ { cell: true, wrapper: true } } 
  scroll={ { x: "auto" } } 
  pagination={false} 
/>);
```

## Request example

```text
{ 
    "Id": "r-20250408201328-*****" 
}
```

## Sample responses

```json
{ 
    "ChargeType": "PrePaid", 
\t"Description": "This is a resource group", 
    "ExpireTime": "2025-05-08T15:59:59Z", 
    "Id": "r-20250408201328-*****", 
"Name": "resource group name", 
    "PeriodUnit": "Month", 
    "RenewType": 1, 
    "ResourceAllocated": { 
        "ComputeResources": [ 
            { 
                "Count": 1, 
                "InstanceTypeId": "ml.g3i.16xlarge", 
                "ZoneId": "cn-shanghai-b" 
            } 
        ], 
        "VolumeResources": [ 
            { 
                "Size": 200, 
                "VolumeTypeId": "ml.essd.pl1", 
                "ZoneId": "cn-shanghai-b" 
            } 
        ] 
    }, 
    "ResourceCapability": { 
        "ComputeResources": [ 
            { 
                "Count": 2, 
                "InstanceTypeId": "ml.g3i.16xlarge", 
                "ZoneId": "cn-shanghai-b" 
            } 
        ], 
        "VolumeResources": [ 
            { 
                "Size": 200, 
                "VolumeTypeId": "ml.essd.pl1", 
                "ZoneId": "cn-shanghai-b" 
            } 
        ] 
    }, 
    "Status": { 
        "State": "Running" 
    }, 
    "StorageConfig": { 
        "StorageNetworkConfig": { 
            "SubnetIds": [ 
                "subnet-3qdjzt425tqm87prml10*****" 
            ], 
            "VpcId": "vpc-3qdjzs6imwt1c7prmkzs*****" 
        } 
    }, 
    "WorkloadNetworkConfig": { 
        "SecurityGroupIds": [ 
            "sg-3qdjzscfq8yyo7prml00*****" 
        ], 
        "SubnetIds": [ 
            "subnet-3qdjzt425tqm87prml10*****" 
        ], 
        "VpcId": "vpc-3qdjzs6imwt1c7prmkzs*****" 
    }, 
    "ZoneIds": [ 
        "cn-shanghai-b" 
    ] 
}
```

## Error Code

For a list of error codes, see [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
