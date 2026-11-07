---
title: "Structure and Development of Custom Chart Plugins"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Structure_and_Development_of_Custom_Chart_Plugins"
---

<span id="9a7f163e"></span>
# 1. Overview

The development of chart plugins is a key component of custom visualization, enabling users to turn personalized data presentations into reality. This article will explore the internal structure and development process of chart plugins in depth, guiding you through concrete examples to understand the project architecture and complete the creation of a custom chart plugin. (Currently, the custom visualization feature is still in the internal testing phase. To address specific needs for this feature, please contact the Volcano Engine business team to obtain more details about purchasing and collaboration.)

**Caution: Before reading and completing the configuration items in this article, you need to first complete the preparation steps such as environment setup, initialization, and debugging. For details, refer to** [Custom visualization overview](https://docs.byteplus.com/docs/DataWind/Custom_Visualization_Overview) **.** 

<span id="79448ae1"></span>
# 2. Chart plugin structure

In [Custom visualization overview](https://docs.byteplus.com/docs/DataWind/Custom_Visualization_Overview), you completed the following configuration items:


* Implemented chart rendering using Html and Javascript.

* Specified Id, Html, Icon, and other information through the `contributes` property in the structure descriptor file `package.json`.

* Registered the custom rendering logic in this product by calling the Context API in the plugin entry file.


This section will explain the above configuration items in detail using the project structure of a sample plugin:

```Plain
├── assets                // 存放资源的目录，比如 icon
├── dist                  // dev/build 的产物
│   └── index.html        // src/index.html 的编译产物
│   └── main.umd.js       // src/main.ts 的编译产物
├── src                   // 源码目录
│   └── index.html        // （存在自定义图表时）自定义图表的 html 文件
│   └── main.ts           // 插件入口文件，用于本产品中注册插件
├── package.json          // 插件描述文件
├── extension.config.js   // 插件 CLI 配置文件
```


<span id="60f49083"></span>
## 2.1 Plugin entry file src/main.ts

In this file, you need to export two lifecycle methods, `activate` and `deactivate`. The application will call these methods when the plugin is activated and deactivated.


* In the `activate` method, you need to call the registration method in the plugin context object provided by the application to complete the registration of chart information.

* The `deactivate` method is used to perform cleanup when uninstalling the plugin and is empty by default.


```JavaScript
export function activate(context) {
    context.vizQueryChartRenderer.register({    
        id: 'extension-demo'
    })
}
export function deactivate() {} 
```


> For security reasons, the plugin entry file runs in an isolated Javascript sandbox, so you cannot call browser APIs within it.


<span id="96e26014"></span>
## 2.2 Rendering implementation

For extension features such as custom charts that require rendering, you also need to provide an HTML file to load the chart, such as `src/index.html`.

The code related to rendering runs in an Iframe sandbox, and you can call browser APIs to implement the required functionality.

<span id="cf3ed879"></span>
## 2.3 Plugin description file package.json

This file is a superset of package.json, and uses the `main` and `contributes` fields to specify the plugin entry file location and the extension features included in the plugin, respectively.

For example, for the custom chart in the sample plugin package, you need to fill in the relevant information in the `vizQuery.chart.renderer` extension point.

```JSON
{
  "name": "@datawind/extension-template-react-echarts",
  "version": "2.0.3",
  "main": "dist/main.umd.js",
  "scripts": {
    "dev": "datawind-extension dev",
    "build": "datawind-extension build"
  },
  "dependencies": {
    "react": "^16.0.0",
    "react-dom": "^16.0.0",
    "echarts": "~5.3.2"
  },
  "devDependencies": {
    "@types/react": "~18.0.9",
    "@types/react-dom": "^16.0.0",
    "typescript": "^4.3.2"
  },
  "contributes": {
    "vizQuery.chart.renderer": [
      {
        "id": "extension-demo",
        "name": "extension-react",
        "content": "dist/index.html",
        "icon": ""
      }
    ]
  }
}
```


Note that the file paths configured in this description file (such as image icons and plugin entry files) are not source code paths, but rather paths to the build output, such as files under `assets/**` and `dist/**`.

<span id="24d0afec"></span>
## 2.4 Plugin CLI configuration file extension.config.js

extension.config.js allows users to configure behaviors related to @datawind/extension\-cli.


* `entry` \- Configures the plugin entry file. In the sample code, this configuration compiles `src/main.ts` as the entry file into `dist/main.umd.js`.

* `htmlEntry` \- Configures the HTML entry file. Currently, this is only used in custom chart scenarios. In the sample code, this configuration compiles `src/index.html` as the entry file into `dist/index.html`.

* `devPort` \- Configures the plugin debug port. The default is 5000.


The configuration example is as follows:

```JavaScript
module.exports = {
  entry: {
    main: 'src/main.ts',
  },
  htmlEntry: {
    index: 'src/index.html',
  }
}
```


<span id="206998e1"></span>
# 3. Chart plugin development

After initializing the project, you can see the following contents in the project folder:


* `assets` \- Stores resource files

* `src/main.ts` \- Plugin entry file. You need to register the chart plugin in the `activate` function.

* `src/index.html` \- Chart HTML file

* `src/chart.ts` \- Chart implementation code

* `package.json` \- Plugin information. You need to configure chart information in the `contributes` section under the `vizQuery.chart.renderer` extension point.

* `extension.config.js` \- Plugin build configuration


Next, you can learn more about the file structure of this project.

<span id="0c9b30b8"></span>
## 3.1 src/main.ts

First, for chart plugins, call the `activate` method in the plugin entry file to register a custom chart renderer via `context.vizQueryChartRenderer.register`.

```JavaScript
import { FieldMap } from './types'

export const activate = (context) => {
  context.vizQueryChartRenderer.register({
    id: "extension-demo",
    fields: [
      {
        label: "维度",
        location: FieldMap.Dimension,
        fieldType: 0,
      },
      {
        label: "指标",
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

export const deactivate = () => { }
```


Second, the object passed in the `register` method call contains several fields:


* `id` \- Custom chart ID, which needs to be consistent with the corresponding description in package.json

* `fields` \- Custom fields. `Pie Chart` requires two fields, `Dimension` and `Measure`. Use `fieldType` to specify whether the field needs to be aggregated.

* `constraints` \- Custom description of field count restrictions for chart drawing. `Pie Chart` supports using one dimension and one metric.


```TypeScript
type Constraints = Record<string, number[]>[]
```


Each constraint is in an OR relationship with the others, while multiple conditions within a constraint are in an AND relationship.

For more examples, please refer to the following code:

```TypeScript
context.vizQueryChartRenderer.register({
  // ...
  constraints: [
    {
      // This configuration means: at least one field must be placed in the dimension field area
      [FieldMap.Dimension]: [1, Infinity],
      // This configuration means: there is no restriction on the metric field area
      [FieldMap.Measure]: [0, Infinity],
    },
    {
      // This configuration indicates that the dimension field area can only contain one field
      [FieldMap.Dimension]: [1],
      // This configuration indicates that the measure field area can contain between two and ten fields
      [FieldMap.Measure]: [2, 10],
    },
  ],
});
```



* `settings` \- Custom configuration. `Pie Chart` currently does not support custom configuration.


You can also read [Custom visualization overview](https://docs.byteplus.com/docs/DataWind/Custom_Visualization_Overview) for detailed explanations of the relevant fields.

<span id="2b7d10b1"></span>
## 3.2 src/index.html

Chart HTML, where the imported resource file `./chart.ts` can implement the chart plugin. All `<script type="module" src='*' />` imports in this file, if the configured `src` is a local relative path, will undergo dependency analysis and be packaged together with the HTML resource during the compilation phase. As follows:

```HTML
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>react echarts</title>
</head>

<body>
  <div id="root"></div>
  <script type="module" src="/src/index.tsx"></script>
</body>

</html>
```


<span id="a3508ddd"></span>
## 3.3 src/App.tsx

Chart implementation code:


* When `window.onmessage` receives an event where the type in `e.data` is `propertiesChange`, it retrieves the chart data from `data.vizData` and calls the `setVizData` method.

* Use the `transformData` method to convert `vizData` into the data structure required by echarts.

* Render using echarts


```TypeScript
import React, { useEffect, useState, useRef } from 'react'
import * as echarts from 'echarts'

import { FieldMap } from './types'

interface RenderData {
  name: string
  value: number
}

const useChart = (chartRef: React.RefObject<HTMLElement>, options: any) => {
  let chartInstance: echarts.ECharts

  const renderChart = () => {
    if (chartRef?.current) {
      chartInstance = echarts.init(chartRef?.current)
      chartInstance.setOption(options)
    }
  }
  useEffect(() => {
    renderChart()
  }, [options])
  useEffect(() => {
    return () => {
      chartInstance && chartInstance.dispose()
    }
  }, [])

  return
}

const App: React.FC = () => {
  const chartRef = useRef<HTMLElement>(null)
  const [vizData, setVizData] = useState<any>(null)
  const [renderData, setRenderData] = useState<RenderData[]>()

  useEffect(() => {
    window.onmessage = (
      e: MessageEvent<{
        type: string
        data: {
          vizData: any;
          language: 'zh_CN' | 'en_US';
        }
      }>
    ) => {
      const { type, data } = e.data
      if (type === 'propertiesChange') {
        setVizData(data.vizData)
      }
    }
  }, [])

  useEffect(() => {
    if (vizData) {
      const data = transformData(vizData)
      setRenderData(data)
    }
  }, [vizData])

  // Convert vizData to the echarts data structure
  const transformData = (vizData) => {
    const { locationMap, datasets } = vizData
    const nameField = locationMap[FieldMap.Dimension]?.[0]
    const valueField = locationMap[FieldMap.Measure]?.[0]

    const data = datasets.map((item) => ({
      name: item[nameField],
      value: parseFloat(item[valueField]),
    }))
    return data
  }

  const options = {
    title: {
      text: 'react echarts demo',
      left: 'center'
    },
    tooltip: {
      trigger: 'item'
    },
    legend: {
      left: "center",
      top: "bottom",
      orient: "horizontal",
    },
    series: [
      {
        name: 'Access From',
        type: 'pie',
        radius: '50%',
        data: renderData,
      }
    ]
  }
  useChart(chartRef, options)

  return (
    <>
      <div
        style={{ width: "1280px", height: "480px" }}
        ref={chartRef}
      />
    </>
  )
}

export default App
```


`VizData` is the data structure used by this product to describe charts. For more information, refer to [Custom Chart Data Structure and Plugin Property Configuration](https://docs.byteplus.com/docs/DataWind/Custom_Chart_Data_Structure_and_Plugin_Property_Configuration).

Since the chart implementation code runs in an Iframe sandbox, there are no API restrictions on its execution environment. Therefore, you are free to use browser APIs to implement custom charts.

<span id="7790ef0e"></span>
## 3.4 package.json

For custom charts, you need to describe the chart extension point in the `contributes` section of `package.json`.

The custom chart extension point for visual query is `vizQuery.chart.renderer`:


* `id` \- Must be consistent with the chart `id` registered in the plugin entry file

* `name` \- Chart name, which appears in the chart information of visual query

* `icon` \- Chart icon file path, used as the chart icon in visual query

* `content` \- Chart HTML file path


```JSON
{
  "name": "@datawind/extension-template-react-echarts",
  "version": "2.0.3",
  "main": "dist/main.umd.js",
  "scripts": {
    "dev": "datawind-extension dev",
    "build": "datawind-extension build"
  },
  "dependencies": {
    "react": "^16.0.0",
    "react-dom": "^16.0.0",
    "echarts": "~5.3.2"
  },
  "devDependencies": {
    "@types/react": "~18.0.9",
    "@types/react-dom": "^16.0.0",
    "typescript": "^4.3.2"
  },
  "contributes": {
    "vizQuery.chart.renderer": [
      {
        "id": "extension-demo",
        "name": "extension-react",
        "content": "dist/index.html",
        "icon": ""
      }
    ]
  }
}
```


<span id="be9a3cca"></span>
## 3.5 extension.config.js

In the sample code, `entry` indicates that `src/main.ts` needs to be compiled as the plugin entry file to `dist/main.umd.js`.

In addition to the default plugin entry compilation configuration, custom charts also need to provide chart HTML compilation configuration. In the sample code, `htmlEntry` indicates that `src/index.html` needs to be compiled as the entry file to `dist/index.html`.

```JavaScript
module.exports = {
  entry: {
    main: 'src/main.ts',
  },
  htmlEntry: {
    index: 'src/index.html',
  },
  react: true,
}
```
