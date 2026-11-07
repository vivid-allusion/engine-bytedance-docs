---
title: "Custom Chart Data Structure and Plugin Property Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Custom_Chart_Data_Structure_and_Plugin_Property_Configuration"
---

<span id="d04a719b"></span>
# 1. Overview

The chart data structure and plugin property configuration are among the core components for implementing custom visualizations. This document aims to introduce detailed information about data structure design and property configuration in chart plugin development. This document provides an in\-depth explanation of key fields in plugin development and explains how to set properties for your chart plugin, ensuring that your custom visualization plugin is not only fully functional but also meets specific business requirements and user preferences. (Currently, the custom visualization feature is still in the internal testing phase. If you have specific requirements for this feature, please contact the Volcano Engine business team to obtain more information about purchasing and collaboration.)

**Note: Before reading and completing the configuration items in this document, you need to first complete the relevant configurations in** [Custom visualization overview](https://docs.byteplus.com/docs/DataWind/Custom_Visualization_Overview) **and** [Structure and Development of Custom Chart Plugins](https://docs.byteplus.com/docs/DataWind/Structure_and_Development_of_Custom_Chart_Plugins) **in sequence.** 

<span id="66d7e851"></span>
# 2. Chart data structure

Both built\-in charts and custom charts in this product are rendered based on the general chart data structure `VizData`.

When developing custom charts, you need to pay attention to the relevant fields in `VizData`.

```TypeScript
type FieldId = string
interface VizData {  
    // 字段位置信息  
    locationMap: Record<string, FieldId[]>;  
    // 字段信息  
    fieldMap: Record<FieldId, FieldInfo>;  
    // 图表数据  
    datasets: Record<FieldId, string>[];
}
```


<span id="6bbd2b84"></span>
## 2.1 Field description

 **（1）locationMap**

Field location information, which records the `FieldId` array for each custom field.

 **（2）fieldMap**

Describes the complete field information corresponding to `FieldId`. The `FieldInfo` type is as follows:

```TypeScript
interface FieldInfo {  
    // Field alias (name)
    alias: string;  
    // Field type
    type: string;  
    // Field value range
    domain: string[];
}
```


**Note**: After using the sorting function, the `fieldInfo` field's `domain` will contain both the value range and the sorting result of the field. Refer to the value order of the `domain` field to implement chart sorting.

 **（3）datasets**

Array of chart query results. Each object in the array represents a row in the query result. The object's `key` is the field id, and the object's `value` is the field value.

<span id="f9aaef4e"></span>
## 2.2 Example

Taking the sample plugin package as an example: the `Pie Chart` chart is a pie chart drawn based on `echarts`, with one dimension field and one metric field.

The following is the relevant code for registering custom fields in the sample plugin package:

```TypeScript
export const activate = (context) => {  
    context.vizQueryChartRenderer.register({  
        fields: [
          {
            label: '维度',
            location: 'dimensions',
            fieldType: 0,
          },
          {
            label: '指标',
            location: 'measures',
            fieldType: 1,
          }
        ],
    })
}
```


<span id="80936e62"></span>
### 2.2.1 Obtain field id

You can obtain the `FieldId` based on the `locationMap` of `VizData`.

First, use `locationMap[location]` to get the array of `FieldId` on the `location`, then use the corresponding index to obtain the `FieldId` of the field.

The `Pie Chart` has two `location`s, `'dimensions'` and `'measures'`, and each `location` has exactly one field.

The following example shows how to obtain the `FieldId` of all custom fields in a `Pie Chart`:

```TypeScript
const { locationMap } = vizData
const xId = locationMap['dimensions'][0]
const yId = locationMap['measures'][0]
```


<span id="e39e0cce"></span>
### 2.2.2 Obtain detailed field information

You can obtain `FieldInfo`, that is, detailed field information, based on the `fieldMap` of `VizData`.

The following example obtains the detailed information of the field corresponding to `['dimensions'][0]` in the `Pie Chart`:

```TypeScript
const { locationMap, fieldMap } = vizData
const xId = locationMap['dimensions'][0]
const xFieldInfo = fieldMap[xId]
const { alias, type, domain } = xFieldInfo
```


<span id="5069b27d"></span>
### 2.2.3 Convert query results to an appropriate data structure

The `datasets` of `VizData` represents the result of a single query, with the type `Record<FieldId, string>[]`. To convert the `datasets` of a `Pie Chart` to the format `{ x: string, y: string }[]`, refer to the following code:

```TypeScript
const { locationMap, datasets } = vizData
const xId = locationMap['dimensions'][0]
const yId = locationMap['measures'][0]
const data: { x: string, y: string, z: string }[] = datasets.map(item => ({
    x: item[xId],
    y: item[yId],
}))
```


To preserve precision, the visualization query module of this product returns all `datasets` data in `string` format.

To aggregate numeric fields, you can directly convert them to the `number` type:

```TypeScript
const data: { x: string, y: string, z: number }[] = datasets.map(item => ({
    x: item[xId],
    y: +item[yId],
}))
```


<span id="7f3c289c"></span>
# 3. Chart property configuration

<span id="ae249b67"></span>
## 3.1 Custom property configuration

By default, custom charts have no chart property configuration. When registering a custom chart, you can define the property configuration form through the `settings` field.

The following `register` method registers two `SettingGroup`s for the custom chart. The first includes an `Input` component and a `Select` component, and the second includes a `CheckboxGroup` component.

```TypeScript
import { ContributeContext } from '@aeolus/extension-context'
import Localize, {
  localize
} from '@aeolus-developers/localize'
 
export enum FieldMap {
  Dimension = 'dimensions',
  Measure = 'measures',
}
 
export const activate = (context: ContributeContext) => {
  Localize.init(context.language)
  context.vizQueryChartRenderer.register({
    id: '@aeolus-developers/chartjs-line',
    fields: [
      {
        label: localize("settings.info.dimension"),
        location: FieldMap.Dimension,
        fieldType: 0,
      },
      {
        label: localize("settings.info.measure"),
        location: FieldMap.Measure,
        fieldType: 1,
      }
    ],
    constraints: [
      {
        [FieldMap.Dimension]: [1, 1],
        [FieldMap.Measure]: [1, 1],
      }
    ]
  })
}
```


<span id="e97a47ea"></span>
## 3.2 Interface description

The configuration of a chart contains multiple `SettingGroup`s, and each `SettingGroup` contains multiple `SettingItem`s.


* Each `SettingGroup` in the UI includes its `label` and `switch`. The `switch` is used to control whether the entire `SettingGroup` is enabled.

* Each `SettingItem` in the UI includes its `label` and `component`. The `component` describes the custom chart configuration component to be used.


<span id="6969187f"></span>
## 3.3 Type description

The following describes the type parameters of `settings` in `context.vizQueryChartRenderer.register`.

```TypeScript
interface VizQueryChartRendererRegisterParameters {
  /**   * ensure it is unique for all chart renderers,   * `extension-package-name:chart-name` is recommended   * for example `@aeolus-developers/extension-3d-bar-chart`   * */
  id: string;
  /**   * custom fields   * */
  fields: FieldGroup[];
  /**   * fields constraints   * */
  constraints?: Constraint[];
  /**   * custom chart settings   */
  settings?: SettingGroup[];
}
```


 **（1）SettingGroup**

Configuration group for custom chart configuration


|Property |Type |Description |
|---|---|---|
|key |string |Access custom configuration values in the chart plugin via [SettingGroup.key].[SettingItem.key] |
|label |string |Configuration group name |
|switch |boolean |Whether to display the configuration group switch; not displayed by default |
|items |<ins>SettingItem[]</ins> |Custom configuration items contained in the configuration group |


 **（2）SettingItem**

Custom configuration item


|Property |Type |Description |
|---|---|---|
|key |string |Access custom configuration values in the chart plugin via [SettingGroup.key][SettingItem.key] |
|label |string |Configuration item name |
|component |<ins>SettingComponentType</ins> |Configuration item component |


 **（3）SettingComponentType**

Configuration item component. The component types currently provided by `datawind` are as follows:

```TypeScript
type SettingComponentType =
  | CheckboxGroupType
  | InputType
  | InputNumberType
  | SelectType
  | SwitchType
  | RadioGroupType
  | ColorPickerType;
```


Each `SettingItem` must specify the `component` property, which can be one of the following component types.

 **（4）CheckboxGroupType**

```TypeScript
interface CheckboxGroupType {
  type: "CheckboxGroup";
  props: Partial<{
    defaultValue: string[] | number[];
    options: {
      label: string;
      value: string | number;
    }[];
    direction: "vertical" | "horizontal";
  }>;
}
```


 **（5）InputType**

```TypeScript
interface InputType {
  type: "Input";
  props: Partial<{
    defaultValue: string;
  }>;
}
```


 **（6）InputNumberType**

```TypeScript
interface InputNumberType {
  type: "InputNumber";
  props: Partial<{
    defaultValue: number;
    min: number;
    max: number;
    step: number;
  }>;
}
```


 **（7）SelectType**

```TypeScript
interface SelectType {
  type: "Select";
  props: Partial<{
    mode: "default" | "multiple";
    defaultValue: string | string[] | number | number[];
    options: {
      label: string;
      value: string;
    }[];
  }>;
}
```


 **（8）SwitchType**

```TypeScript
interface SwitchType {
  type: "Switch";
  props: Partial<{
    defaultValue: boolean;
    checkedText: string;
    uncheckedText: string;
  }>;
}
```


 **（9）RadioGroupType**

```TypeScript
interface RadioGroupType {
  type: "RadioGroup";
  props: Partial<{
    type: "radio" | "button";
    defaultValue: string | number;
    options: {
      label: string;
      value: string | number;
    }[];
    direction: "vertical" | "horizontal";
  }>;
}
```


 **（10）ColorPickerType**

```TypeScript
interface ColorPickerType {
  type: "ColorPicker";
  props: Partial<{
    type: "default" | "linear" | "theme";
    defaultValue: string[];
  }>;
}
```


<span id="b5a8c4d9"></span>
## 3.4 Example

<span id="ea04c6be"></span>
### 3.4.1 Plugin registration

```TypeScript
import { ContributeContext } from "@aeolus/extension-context";
 
export const activate = (context: ContributeContext) => {
  context.vizQueryChartRenderer.register({
    id: "@aeolus-developers/visual-data-explorer",
    extend: "table",
    settings: [
      {
        key: "checkboxGroup",
        label: "CheckboxGroup",
        switch: true,
        items: [
          {
            key: "base",
            label: "Base Component",
            component: {
              type: "CheckboxGroup",
              props: {
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                ],
              },
            },
          },
          {
            key: "vertical",
            label: "Vertical Layout",
            component: {
              type: "CheckboxGroup",
              props: {
                direction: "vertical",
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                ],
              },
            },
          },
          {
            key: "default",
            label: "Default Value",
            component: {
              type: "CheckboxGroup",
              props: {
                defaultValue: ["a", "b"],
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                ],
              },
            },
          },
        ],
      },
      {
        key: "input",
        label: "Input",
        switch: true,
        items: [
          {
            key: "base",
            label: "Base Component",
            component: {
              type: "Input",
              props: {},
            },
          },
        ],
      },
      {
        key: "inputNumber",
        label: "InputNumber",
        switch: true,
        items: [
          {
            key: "base",
            label: "Base Component",
            component: {
              type: "InputNumber",
              props: {},
            },
          },
          {
            key: "decimal",
            label: "Using min, max and step",
            component: {
              type: "InputNumber",
              props: {
                min: 0,
                max: 10,
                step: 0.5,
              },
            },
          },
        ],
      },
      {
        key: "select",
        label: "Select",
        switch: true,
        items: [
          {
            key: "base",
            label: "Base Component",
            component: {
              type: "Select",
              props: {
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                  { label: "D", value: "d" },
                ],
              },
            },
          },
          {
            key: "multiple",
            label: "Multiple",
            component: {
              type: "Select",
              props: {
                mode: "multiple",
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                  { label: "D", value: "d" },
                ],
              },
            },
          },
        ],
      },
      {
        key: "switch",
        label: "Switch",
        switch: true,
        items: [
          {
            key: "base",
            label: "Base Component",
            component: {
              type: "Switch",
              props: {},
            },
          },
        ],
      },
      {
        key: "radioGroup",
        label: "RadioGroup",
        switch: true,
        items: [
          {
            key: "base",
            label: "Base Component",
            component: {
              type: "RadioGroup",
              props: {
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                  { label: "D", value: "d" },
                ],
              },
            },
          },
          {
            key: "button",
            label: "Button Mode",
            component: {
              type: "RadioGroup",
              props: {
                type: "button",
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                  { label: "D", value: "d" },
                ],
              },
            },
          },
          {
            key: "vertical",
            label: "Vertical Layout",
            component: {
              type: "RadioGroup",
              props: {
                direction: "vertical",
                options: [
                  { label: "A", value: "a" },
                  { label: "B", value: "b" },
                  { label: "C", value: "c" },
                  { label: "D", value: "d" },
                ],
              },
            },
          },
        ],
      },
    ],
  });
};
```


<span id="40b69437"></span>
### 3.4.2 Chart rendering

In the plugin, you can listen for the `propertiesChange` event of the plugin chart via `window.onmessage`, and obtain the custom configuration values through `e.data.data.settings`.

```TypeScript
window.onmessage = (
  e: MessageEvent<{
    type: string;
    data: any;
  }>
) => {
  const { type, data } = e.data;
 
  if (type === "propertiesChange") {
    // outputs { vizData, settings }
    // using settings[settingGroup.key]?.[settingItem.key] to visit a value
    console.log(data);
  }
};
```
