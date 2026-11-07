---
title: "CreateResouCreateResourceGroup - Create resource grouprceGroup - Create resource group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/CreateResouCreateResourceGroup_-_Create_resource_grouprceGroup_-_Create_resource_group"
---

Create resource group

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
title: 'Required or Not', 
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
    Example: <RenderMd content={"CreateResourceGroup"} />, 
Description: <RenderMd content={"The action to perform, value: CreateResourceGroup."} />," 
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
    rowKey: '->Name', 
    Name: 'Name', 
    DataType: 'String', 
IsRequired: 'Yes', 
Example: <RenderMd content={"Test Resource Group"} /> 
Description: <RenderMd content={"Resource group name. Supports 1-128 visible characters and can only contain uppercase and lowercase letters, Chinese characters, numbers, hyphens, and underscores."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Description', 
    Name: 'Description', 
    DataType: 'String', 
IsRequired: 'No', 
Example: <RenderMd content={"This resource group is used for testing"} /> 
Description: <RenderMd content={"Resource group description. Supports 1 to 500 characters."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->ResourceConfig', 
    Name: 'ResourceConfig', 
    DataType: 'Object', 
IsRequired: 'No', 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"Resource configuration, only passed in for Prepaid resource groups"} /> 
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
Description: <RenderMd content={"Resource Instance Count"} />, 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->ResourceConfig->ComputeResources->ZoneId', 
              Name: 'ZoneId', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"resource availability zone ID"} /> 
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
IsRequired: 'Yes', 
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
Description: <RenderMd content={'Cloud disk capacity, unit GiB'} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->ResourceConfig->VolumeResources->ZoneId', 
              Name: 'ZoneId', 
              DataType: 'String', 
IsRequired: 'Yes', 
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
    rowKey: '->ChargeType', 
    Name: 'ChargeType', 
    DataType: 'String', 
IsRequired: 'Yes', 
    Example: <RenderMd content={"PrePaid"} />, 
Description: <RenderMd content={"billing type"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->PeriodUnit', 
    Name: 'PeriodUnit', 
    DataType: 'String', 
IsRequired: 'No', 
    Example: <RenderMd content={"Month"} />, 
Description: <RenderMd content={"purchase period unit"} />," 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->Period', 
    Name: 'Period', 
    DataType: 'Integer', 
IsRequired: 'No', 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"Number of purchase cycles. Must be specified when the billing type is Prepaid."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->AutoRenew', 
    Name: 'AutoRenew', 
    DataType: 'Boolean', 
IsRequired: 'No', 
    Example: <RenderMd content={"true"} />, 
Description: <RenderMd content={"Whether to turn on Automatic renewal. Must be specified when the billing type is Prepaid."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->AutoRenewPeriod', 
    Name: 'AutoRenewPeriod', 
    DataType: 'Integer', 
IsRequired: 'No', 
    Example: <RenderMd content={"1"} />, 
Description: <RenderMd content={"The number of renewal cycles for a single automatic renewal. Must be specified when the billing type is Prepaid."} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->StorageConfig', 
    Name: 'StorageConfig', 
    DataType: 'Object', 
IsRequired: 'No', 
    Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"storage configuration"} />, 
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
Description: <RenderMd content={"user security group list"} /> 
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
Description: <RenderMd content={"Number of data replicas written (Not allowed when using an existing SFCS storage settings instance)"} /> 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->Sfcs->Description', 
              Name: 'Description', 
              DataType: 'String', 
IsRequired: 'No', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"SFCS instance description (when using an existing SFCS instance, setting is not allowed)"} />, 
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
Description: <RenderMd content={"vePFS configuration"} />," 
          children: [ 
            { 
              rowKey: '->StorageConfig->Vepfs->MountServiceId', 
              Name: 'MountServiceId', 
              DataType: 'String', 
IsRequired: 'Yes', 
              Example: <RenderMd content={"."} />, 
Description: <RenderMd content={"vePFS mount service ID"} />," 
              children: [ 
              ] 
            }, 
            { 
              rowKey: '->StorageConfig->Vepfs->FileSystemIds', 
              Name: 'FileSystemIds', 
              DataType: 'Array of String', 
IsRequired: 'Yes', 
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
Description: <RenderMd content={ "Whether to turn on client prefetch" } /> 
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
Description: <RenderMd content={"Load network mode, optional values: SingleNIC, DualNIC; when the value is DualNIC, WorkloadNetworkConfig must be filled in; the default value is DualNIC"} /> 
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
IsRequired: 'Yes', 
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
Description: <RenderMd content={"User Security Group List"} /> 
          children: [ 
          ] 
        }, 
    ] 
  }, 
  { 
    rowKey: '->MGpuEnabled', 
    Name: 'MGpuEnabled', 
    DataType: 'Boolean', 
IsRequired: 'No', 
    Example: <RenderMd content={"true"} />, 
Description: <RenderMd content={"whether to turn on the mGPU function"} /> 
    children: [ 
    ] 
  }, 
  { 
    rowKey: '->DryRun', 
    Name: 'DryRun', 
    DataType: 'Boolean', 
IsRequired: 'No', 
    Example: <RenderMd content={"`true`"} />, 
Description: <RenderMd content={"Whether to only pre-check this request.\nValues:\n- true: Send a check request without creating resources. Check items include whether required parameters are filled in, request format, business restrictions, and quotas. If the check fails, return the corresponding error. If the check passes, return the error code DryRunOperation.\n- false: Send a normal request and directly create resources after passing the check."} /> 
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
    "AutoRenew": false, 
    "AutoRenewPeriod": 1, 
    "ChargeType": "PrePaid", 
"Description": "This is a Prepaid resource group", 
    "DryRun": false, 
"Name": "Prepaid resource group", 
    "Period": 3, 
    "PeriodUnit": "Day", 
    "ResourceConfig": { 
        "ComputeResources": [ 
            { 
                "Count": 1, 
                "InstanceTypeId": "ml.g3a.16xlarge", 
                "ZoneId": "cn-beijing-b" 
            } 
        ], 
        "VolumeResources": [ 
            { 
                "Size": 100, 
                "VolumeTypeId": "ml.essd.pl0", 
                "ZoneId": "cn-beijing-b" 
            } 
        ] 
    }, 
    "StorageConfig": { 
        "StorageNetworkConfig": { 
            "SubnetIds": [ 
                "subnet-mimoz59wzbi85smt1bk*****" 
            ], 
            "VpcId": "vpc-mimoxzu9m60w5smt1bp*****" 
        } 
    }, 
    "UseMGpu": false, 
    "WorkloadNetworkConfig": { 
        "SecurityGroupIds": [ 
            "sg-mimoy5rcyby85smt1bv*****" 
        ], 
        "SubnetIds": [ 
            "subnet-mimoz59wzbi85smt1bk*****" 
        ], 
        "VpcId": "vpc-mimoxzu9m60w5smt1bp*****" 
    } 
}
```

## Back Example 1

```json
{ 
    "Id": "r-20250414212247-*****" 
}
```

## Request Example 2

```text
{ 
    "ChargeType": "OnDemand", 
"Description": "This is an on-demand post-payment resource group", 
    "DryRun": false, 
"Name": "On-demand Post-payment Resource Group", 
    "StorageConfig": { 
        "StorageNetworkConfig": { 
            "SubnetIds": [ 
                "subnet-mimoz59wzbi85smt1bk*****" 
            ], 
            "VpcId": "vpc-mimoxzu9m60w5smt1bp*****" 
        } 
    }, 
    "UseMGpu": false, 
    "WorkloadNetworkConfig": { 
        "SecurityGroupIds": [ 
            "sg-mimoy5rcyby85smt1bv*****" 
        ], 
        "SubnetIds": [ 
            "subnet-mimoz59wzbi85smt1bk*****" 
        ], 
        "VpcId": "vpc-mimoxzu9m60w5smt1bp*****" 
    } 
}
```

## Back Example 2

```json
{ 
    "Id": "r-20250414212247-*****" 
}
```

## Error Code

For a list of error codes, see [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
