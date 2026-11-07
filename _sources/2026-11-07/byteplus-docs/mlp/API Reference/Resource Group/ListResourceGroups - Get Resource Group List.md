---
title: "ListResourceGroups - Get Resource Group List"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/ListResourceGroups_-_Get_Resource_Group_List"
---

Get Resource Group List

## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

```mixin-react
const columns = [ 
  { 
    width: '20%', 
title: 'Parameters', 
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
title: 'Whether Required', 
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
    Example: <RenderMd content={"ListResourceGroups"} />, 
Description: <RenderMd content={"The actions to perform, Value: ListResourceGroups."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Version', 
    Name: 'Version', 
    DataType: 'String', 
IsRequired: 'Yes', 
    Example: <RenderMd content={"2024-07-01"} />, 
Description: <RenderMd content={"API version, value: 2024-07-01."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Ids', 
    Name: 'Ids', 
    DataType: 'Array of String', 
IsRequired: 'No', 
    Example: <RenderMd content={"["r-20240923155410-*****"]"} />, 
Description: <RenderMd content={"Resource Group ID"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Name', 
    Name: 'Name', 
    DataType: 'String', 
IsRequired: 'No', 
Example: <RenderMd content={"Test Resource Group"} /> 
Description: <RenderMd content={"Resource Group Name"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->NameContains', 
    Name: 'NameContains', 
    DataType: 'String', 
IsRequired: 'No', 
Example: <RenderMd content={"test"} /> 
Description: <RenderMd content={"Resource group name contains"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->States', 
    Name: 'States', 
    DataType: 'Array of String', 
IsRequired: 'No', 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"status filter"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->ChargeType', 
    Name: 'ChargeType', 
    DataType: 'String', 
IsRequired: 'No', 
    Example: <RenderMd content={"PrePaid"} />, 
Description: <RenderMd content={"Billing Mode"} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->PageNumber', 
    Name: 'PageNumber', 
    DataType: 'Integer', 
IsRequired: 'No', 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"pagination page number"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->PageSize', 
    Name: 'PageSize', 
    DataType: 'Integer', 
IsRequired: 'No', 
    Example: <RenderMd content={"10"} />, 
Description: <RenderMd content={"The number of records per page for pagination queries"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->SortBy', 
    Name: 'SortBy', 
    DataType: 'String', 
IsRequired: 'No', 
    Example: <RenderMd content={"CreateTime"} />, 
Description: <RenderMd content={"sorting basis"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->SortOrder', 
    Name: 'SortOrder', 
    DataType: 'String', 
IsRequired: 'No', 
    Example: <RenderMd content={"Ascend"} />, 
Description: <RenderMd content={"sorting order"} /> 
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
title: 'Parameter', 
    dataIndex: 'Name', 
    className: 'openapi-doc-parameter-table-name', 
  }, 
  { 
    width: 130, 
title: 'Type', 
    dataIndex: 'DataType', 
    className: 'openapi-doc-parameter-table-type' 
  }, 
  { 
    width: '25%', 
title: 'Example', 
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
    rowKey: "->Items", 
    Name: "Items", 
    DataType: "Array of Object", 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group list"} />," 
    children: [ 
        { 
          rowKey: "->Items->Id", 
          Name: "Id", 
          DataType: "String", 
          Example: <RenderMd content={"r-20240923155410-*****"} />, 
Description: <RenderMd content={"resource group ID"} />," 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->Name", 
          Name: "Name", 
          DataType: "String", 
Example: <RenderMd content={"Test Resource Group"} />, 
Description: <RenderMd content={"Resource Group Name"} />, 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->Description", 
          Name: "Description", 
          DataType: "String", 
Example: <RenderMd content={"This resource group is for testing"} />, 
Description: <RenderMd content={"resource group description"} />, 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->Status", 
          Name: "Status", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"status"} /> 
          children: [ 
            { 
              rowKey: "->Items->Status->State", 
              Name: "State", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"status"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->Items->Status->SecondaryState", 
              Name: "SecondaryState", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"sub-status"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->Items->Status->Message", 
              Name: "Message", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"status information"} /> 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->Items->ZoneIds", 
          Name: "ZoneIds", 
          DataType: "Array of String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"availability zone ID list"} /> 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->ResourceCapability", 
          Name: "ResourceCapability", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Total Resources"} /> 
          children: [ 
            { 
              rowKey: "->Items->ResourceCapability->ComputeResources", 
              Name: "ComputeResources", 
              DataType: 'Array of Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource Group Compute Resources"} /> 
              children: [ 
                { 
                  rowKey: "->Items->ResourceCapability->ComputeResources->InstanceTypeId", 
                  Name: "InstanceTypeId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource specification ID"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceCapability->ComputeResources->Count", 
                  Name: "Count", 
                  DataType: "Integer", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Number of resource instances"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceCapability->ComputeResources->ZoneId", 
                  Name: "ZoneId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource Availability Zone ID"} /> 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
            { 
              rowKey: "->Items->ResourceCapability->VolumeResources", 
              Name: "VolumeResources", 
              DataType: 'Array of Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group cloud disk resource"} /> 
              children: [ 
                { 
                  rowKey: "->Items->ResourceCapability->VolumeResources->VolumeTypeId", 
                  Name: "VolumeTypeId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud Disk Type ID"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceCapability->VolumeResources->Size", 
                  Name: "Size", 
                  DataType: "Integer", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud Disk Capacity, unit: GiB"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceCapability->VolumeResources->ZoneId", 
                  Name: "ZoneId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource availability zone ID"} />, 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->Items->ResourceAllocated", 
          Name: "ResourceAllocated", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Allocated Resource Quantity"} /> 
          children: [ 
            { 
              rowKey: "->Items->ResourceAllocated->ComputeResources", 
              Name: "ComputeResources", 
              DataType: 'Array of Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource Group Compute Resources"} />," 
              children: [ 
                { 
                  rowKey: "->Items->ResourceAllocated->ComputeResources->InstanceTypeId", 
                  Name: "InstanceTypeId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource specification ID"} />," 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceAllocated->ComputeResources->Count", 
                  Name: "Count", 
                  DataType: "Integer", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource instance count"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceAllocated->ComputeResources->ZoneId", 
                  Name: "ZoneId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource availability zone ID"} /> 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
            { 
              rowKey: "->Items->ResourceAllocated->VolumeResources", 
              Name: "VolumeResources", 
              DataType: 'Array of Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group cloud disk resources"} /> 
              children: [ 
                { 
                  rowKey: "->Items->ResourceAllocated->VolumeResources->VolumeTypeId", 
                  Name: "VolumeTypeId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"cloud disk type ID"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceAllocated->VolumeResources->Size", 
                  Name: "Size", 
                  DataType: "Integer", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud disk capacity, unit GiB"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->ResourceAllocated->VolumeResources->ZoneId", 
                  Name: "ZoneId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource availability zone ID"} /> 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->Items->ChargeType", 
          Name: "ChargeType", 
          DataType: "String", 
          Example: <RenderMd content={"PrePaid"} />, 
Description: <RenderMd content={"billing mode"} /> 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->PeriodUnit", 
          Name: "PeriodUnit", 
          DataType: "String", 
          Example: <RenderMd content={"Month"} />, 
Description: <RenderMd content={"purchase cycle unit"} /> 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->ExpireTime", 
          Name: "ExpireTime", 
          DataType: "String", 
          Example: <RenderMd content={"2020-05-20T13:00:55Z"} />, 
Description: <RenderMd content={"Expiration time. Follow the YYYY-MM-DD'T'HH:MM:SS'Z' format."} />, 
          children: [ 
          ] 
        }, 
        { 
          rowKey: "->Items->StorageConfig", 
          Name: "StorageConfig", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"storage configuration"} />, 
          children: [ 
            { 
              rowKey: "->Items->StorageConfig->StorageNetworkConfig", 
              Name: "StorageNetworkConfig", 
              DataType: 'Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Storage Network Configuration"} />," 
              children: [ 
                { 
                  rowKey: "->Items->StorageConfig->StorageNetworkConfig->VpcId", 
                  Name: "VpcId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user private network"} />, 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->StorageNetworkConfig->SubnetIds", 
                  Name: "SubnetIds", 
                  DataType: "Array of String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user subnet list"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->StorageNetworkConfig->SecurityGroupIds", 
                  Name: "SecurityGroupIds", 
                  DataType: "Array of String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User Security Group List"} /> 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
            { 
              rowKey: "->Items->StorageConfig->Sfcs", 
              Name: "Sfcs", 
              DataType: 'Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={'SFCS configuration'} /> 
              children: [ 
                { 
                  rowKey: "->Items->StorageConfig->Sfcs->Name", 
                  Name: "Name", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={'SFCS instance name'} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Sfcs->Id", 
                  Name: "Id", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance ID"} />, 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Sfcs->Replicas", 
                  Name: "Replicas", 
                  DataType: "Long", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"number of write data replicas"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Sfcs->Description", 
                  Name: "Description", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance description"} />, 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Sfcs->Status", 
                  Name: "Status", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance status"} />, 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Sfcs->ZoneId", 
                  Name: "ZoneId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={ "SFCS instance availability zone ID" } />, 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
            { 
              rowKey: "->Items->StorageConfig->Vepfs", 
              Name: "Vepfs", 
              DataType: 'Object', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS configuration"} /> 
              children: [ 
                { 
                  rowKey: "->Items->StorageConfig->Vepfs->MountServiceId", 
                  Name: "MountServiceId", 
                  DataType: "String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS mount service ID"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Vepfs->FileSystemIds", 
                  Name: "FileSystemIds", 
                  DataType: "Array of String", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS file system ID"} />," 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Vepfs->UnavailableNodeCount", 
                  Name: "UnavailableNodeCount", 
                  DataType: "Integer", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Unavailable Node Count"} /> 
                  children: [ 
                  ] 
                }, 
                { 
                  rowKey: "->Items->StorageConfig->Vepfs->PrefetchEnabled", 
                  Name: "PrefetchEnabled", 
                  DataType: "Boolean", 
                  Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Whether to turn on client prefetch"} /> 
                  children: [ 
                  ] 
                }, 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->Items->WorkloadNetworkConfig", 
          Name: "WorkloadNetworkConfig", 
          DataType: "Object", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"load private network configuration"} />," 
          children: [ 
            { 
              rowKey: "->Items->WorkloadNetworkConfig->VpcId", 
              Name: "VpcId", 
              DataType: 'String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user private network"} />," 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->Items->WorkloadNetworkConfig->SubnetIds", 
              Name: "SubnetIds", 
              DataType: 'Array of String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user subnet list"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: "->Items->WorkloadNetworkConfig->SecurityGroupIds", 
              Name: "SecurityGroupIds", 
              DataType: 'Array of String', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user security group list"} />, 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: "->Items->WorkloadNetworkMode", 
          Name: "WorkloadNetworkMode", 
          DataType: "String", 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Workload network mode, optional values: SingleNIC, DualNIC"} />, 
          children: [ 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: "->TotalCount", 
    Name: "TotalCount", 
    DataType: "Integer", 
    Example: <RenderMd content={"1000"} />, 
Description: <RenderMd content={"total count of the data list"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->PageNumber", 
    Name: "PageNumber", 
    DataType: "Integer", 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"current page number"} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: "->PageSize", 
    Name: "PageSize", 
    DataType: "Integer", 
    Example: <RenderMd content={"10"} />, 
Description: <RenderMd content={"number of records per page for pagination query"} /> 
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
\t"NameContains": "test", 
    "PageSize": 10, 
    "SortBy": "CreateTime", 
    "SortOrder": "Descend", 
    "States": [ 
        "Running" 
    ] 
}
```

## Sample responses

```json
{ 
    "Items": [ 
        { 
            "ChargeType": "PrePaid", 
            "Description": "", 
            "ExpireTime": "2025-05-08T15:59:59Z", 
            "Id": "r-20250408201328-*****", 
\t\t\t"Name": "Test Resource Group 1", 
            "PeriodUnit": "Month", 
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
        }, 
        { 
            "ChargeType": "PostPaid", 
            "Description": "", 
            "Id": "r-20250310151441-*****", 
"Name": "Test Resource Group 2", 
            "ResourceAllocated": { 
                "ComputeResources": [] 
            }, 
            "ResourceCapability": { 
                "ComputeResources": [ 
                    { 
                        "Count": 1, 
                        "InstanceTypeId": "ml.g3i.8xlarge", 
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
    ], 
    "PageNumber": 1, 
    "PageSize": 10, 
    "TotalCount": 2 
}
```

## Error Code

For a list of error codes, see [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
