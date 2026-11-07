---
title: "Component API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Component_API"
---

DataWind provides some APIs for components. When using the SDK, you can call the component APIs on the Web Component to implement certain business functions.

<span id="_1-api-参数"></span>
# 1. API parameters

The interface description for the calling method is as follows:

```Plain
abstract class Component {
  abstract async invoke(functionName: string, data?: any): Promise<any>
}

```


The corresponding method names, parameters, and return values are as follows:


|Component |FunctionName |Data |ReturnType |Description |
|---|---|---|---|---|
|dashboard |createSnapshot |void |Promise |Obtain the current dashboard bookmark (snapshot) ID. When `aeolus-dashboard` is passed the `snapshotId`, the dashboard control parameters corresponding to `snapshotId`, such as filter values and dynamic field values, will be restored |
|dashboard |refreshDashboard |void |Promise |Refresh the dashboard. Effective from v2.46 |
|dashboard |showExportModal |void |Promise |Display the dashboard export modal. Effective from v2.46 |


<span id="_2-代码示例"></span>
# 2. Code example

An example of obtaining the dashboard bookmark (snapshot) ID is as follows

```js
import React from 'react'
import ReactDOM from 'react-dom'


class BIComponent extends React.Component {
  componentDidMount() {
    /**     * Using `document.querySelector(YOUR_SELECTOR)` or `ref.current` to access the aeolus component dom element     *@example ref.current.invoke(FUNC, DATA)     */
    document
      .querySelector('bi-dashboard')
      .invoke('createSnapshot')
      .then(({ snapshotId }) => {
        // do something with `snapshotId`
      })
  }

  render() {
    return (
      <bi-dashboard
        urlPrefix='https://console.volcengine.com/bi/datawind'
        dashboardId='******'
        appId='******'
      />

    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))


```
