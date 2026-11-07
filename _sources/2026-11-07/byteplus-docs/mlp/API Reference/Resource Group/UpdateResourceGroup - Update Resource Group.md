---
title: "UpdateResourceGroup - Update Resource Group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/UpdateResourceGroup_-_Update_Resource_Group"
---

Update Resource Group

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
    Example: <RenderMd content={"UpdateResourceGroup"} />, 
Description: <RenderMd content={"The operation to perform, value: UpdateResourceGroup."} />," 
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
    rowKey: '->Id', 
    Name: 'Id', 
    DataType: 'String', 
IsRequired: 'Yes', 
    Example: <RenderMd content={"r-20240923155410-*****"} />, 
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
Description: <RenderMd content={"Resource group name. Supports 1-200 visible characters, and can only contain uppercase and lowercase letters, Chinese characters, numbers, hyphens, and underscores."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Description', 
    Name: 'Description', 
    DataType: 'String', 
IsRequired: 'No', 
Example: <RenderMd content={"This resource group is used for testing"} />, 
Description: <RenderMd content={"Resource group description. Supports 1 to 500 characters."} />, 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->ResourceConfig', 
    Name: 'ResourceConfig', 
    DataType: 'Object', 
IsRequired: 'No', 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={'Resource configuration. When updating resource configuration, do not update other settings at the same time.'} /> 
    children: [ 
        { 
          rowKey: '->ResourceConfig->ComputeResources', 
          Name: 'ComputeResources', 
          DataType: 'Array of Object', 
IsRequired: 'Yes', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group compute resources"} /> 
          children: [ 
            { 
              rowKey: '->ResourceConfig->ComputeResources->InstanceTypeId', 
              Name: 'InstanceTypeId', 
              DataType: 'String', 
IsRequired: 'Yes' 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource specification ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->ResourceConfig->ComputeResources->Count', 
              Name: 'Count', 
              DataType: 'Integer', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={ "resource instance count" } /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->ResourceConfig->ComputeResources->ZoneId', 
              Name: 'ZoneId', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource Availability Zone ID"} /> 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: '->ResourceConfig->VolumeResources', 
          Name: 'VolumeResources', 
          DataType: 'Array of Object', 
IsRequired: 'No', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource group cloud disk resource"} /> 
          children: [ 
            { 
              rowKey: '->ResourceConfig->VolumeResources->VolumeTypeId', 
              Name: 'VolumeTypeId', 
              DataType: 'String', 
IsRequired: 'Yes' 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"cloud disk type ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->ResourceConfig->VolumeResources->Size', 
              Name: 'Size', 
              DataType: 'Integer', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Cloud disk capacity, unit GiB"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->ResourceConfig->VolumeResources->ZoneId', 
              Name: 'ZoneId', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={ "Resource Availability Zone ID" } />, 
              children: [ 
              ] 
            }, 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: '->StorageConfig', 
    Name: 'StorageConfig', 
    DataType: 'Object', 
IsRequired: 'No', 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"storage configuration"} /> 
    children: [ 
        { 
          rowKey: '->StorageConfig->StorageNetworkConfig', 
          Name: 'StorageNetworkConfig', 
          DataType: 'Object', 
IsRequired: 'No', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"storage network configuration"} /> 
          children: [ 
            { 
              rowKey: '->StorageConfig->StorageNetworkConfig->VpcId', 
              Name: 'VpcId', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user private network"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->StorageNetworkConfig->SubnetIds', 
              Name: 'SubnetIds', 
              DataType: 'Array of String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User Subnet List"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->StorageNetworkConfig->SecurityGroupIds', 
              Name: 'SecurityGroupIds', 
              DataType: 'Array of String', 
IsRequired: 'No', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User security group list"} />, 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: '->StorageConfig->Sfcs', 
          Name: 'Sfcs', 
          DataType: 'Object', 
IsRequired: 'No', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS configuration"} />, 
          children: [ 
            { 
              rowKey: '->StorageConfig->Sfcs->Name', 
              Name: 'Name', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance name"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->Sfcs->Replicas', 
              Name: 'Replicas', 
              DataType: 'Long', 
IsRequired: 'No', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={'Number of data replicas written (When using an existing SFCS instance, settings are not allowed)'} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->Sfcs->Description', 
              Name: 'Description', 
              DataType: 'String', 
IsRequired: 'No', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance description (when using an existing SFCS instance, it cannot be set)"} /> 
              children: [ 
              ] 
            }, 
          ] 
        }, 
        { 
          rowKey: '->StorageConfig->Vepfs', 
          Name: 'Vepfs', 
          DataType: 'Object', 
IsRequired: 'No', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS configuration"} />, 
          children: [ 
            { 
              rowKey: '->StorageConfig->Vepfs->MountServiceId', 
              Name: 'MountServiceId', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS mount service ID"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->Vepfs->FileSystemIds', 
              Name: 'FileSystemIds', 
              DataType: 'Array of String', 
IsRequired: 'No', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS file system ID"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->Vepfs->EnablePrefetch', 
              Name: 'EnablePrefetch', 
              DataType: 'Boolean', 
IsRequired: 'No', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Whether to turn on client prefetch"} />, 
              children: [ 
              ] 
            }, 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: '->WorkloadNetworkMode', 
    Name: 'WorkloadNetworkMode', 
    DataType: 'String', 
IsRequired: 'No', 
    Example: <RenderMd content={"DualNIC"} />, 
Description: <RenderMd content={"Load network mode. Optional values: SingleNIC, DualNIC. When the value is DualNIC, WorkloadNetworkConfig must be filled in. The default value is DualNIC"} />," 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->WorkloadNetworkConfig', 
    Name: 'WorkloadNetworkConfig', 
    DataType: 'Object', 
IsRequired: 'No', 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"load private network configuration"} /> 
    children: [ 
        { 
          rowKey: '->WorkloadNetworkConfig->VpcId', 
          Name: 'VpcId', 
          DataType: 'String', 
IsRequired: 'Yes', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user private network"} /> 
          children: [ 
          ] 
        }, 
        { 
          rowKey: '->WorkloadNetworkConfig->SubnetIds', 
          Name: 'SubnetIds', 
          DataType: 'Array of String', 
IsRequired: 'Yes' 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"User Subnet List"} />, 
          children: [ 
          ] 
        }, 
        { 
          rowKey: '->WorkloadNetworkConfig->SecurityGroupIds', 
          Name: 'SecurityGroupIds', 
          DataType: 'Array of String', 
IsRequired: 'No', 
          Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"user security group list"} /> 
          children: [ 
          ] 
        }, 
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

## Request Example 1

```text
{ 
    "Id": "r-20241008220728-*****", 
    "ResourceConfig": { 
        "ComputeResources": [ 
            { 
                "Count": 100, 
                "InstanceTypeId": "ml.hpcpni2l.28xlarge", 
                "ZoneId": "cn-beijing-b" 
            } 
        ], 
        "VolumeResources": [ 
            { 
                "Size": 1024, 
                "VolumeTypeId": "ml.essd.pl1", 
                "ZoneId": "cn-beijing-b" 
            } 
        ] 
    } 
}
```

## Back Example 1

```json
{ 
    "Id": "r-20250313215822-*****" 
}
```

## Request Example 2

```text
{ 
    "Id": "r-20250313215822-*****", 
    "StorageConfig": { 
        "StorageNetworkConfig": { 
            "SubnetIds": [ 
                "subnet-mj8yfuk853i85smt1b0*****", 
                "subnet-13g1zgpd9979c3n6nu4e*****" 
            ], 
            "VpcId": "vpc-mj8yet2n01z45smt1b9*****" 
        } 
    }, 
    "WorkloadNetworkConfig": { 
        "SecurityGroupIds": [ 
            "sg-mj8yeyzqc7wg5smt1ao*****" 
        ], 
        "SubnetIds": [ 
            "subnet-mj8yfuk853i85smt1b0*****", 
            "subnet-13g1zgpd9979c3n6nu4e*****" 
        ], 
        "VpcId": "vpc-mj8yet2n01z45smt1b9*****" 
    } 
}
```

## Back Example 2

```json
{ 
    "Id": "r-20250313215822-*****" 
}
```

## Error Code

For a list of error codes, see [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
