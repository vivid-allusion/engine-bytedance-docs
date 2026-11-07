---
title: "DeleteResourceGroup - Delete Resource Group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/DeleteResourceGroup_-_Delete_Resource_Group"
---

Delete Resource Group

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
title: 'Is Required', 
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
    Example: <RenderMd content={"DeleteResourceGroup"} />, 
Description: <RenderMd content={"The actions to perform, value: DeleteResourceGroup."} /> 
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
Description: <RenderMd content={"resource group ID"} /> 
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

This API has no specific response parameters. For more information, see [Response Response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
{ 
    "Id": "r-20250414212247-*****" 
}
```

## Sample responses

```json
{}
```

## Error Code

For a list of error codes, see [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
