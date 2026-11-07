---
title: "Event"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Event"
---

Various events are triggered during the process of accessing Smart Data Insight DataWind. When using the SDK, events are dispatched to the corresponding `Web Component`, allowing you to listen for these events.

<span id="_1-事件类型"></span>
# Event types

The types of Smart Data Insight events are as follows. The specific `type` and `data` are provided in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><code>type</code>: A string\-type field (<code>string</code>) used to identify the specific event type.</div>


* <div data-tips="true" data-tips-type="tip"><code>data</code>: An optional field of any type (<code>any</code>) used to carry specific data or parameters related to the event.</div>



```Plain
interface BIEvent extends Event {
  detail: {
    type: string;
    data?: any
  }
}
```



|Module |Type |Data |Description |
|---|---|---|---|
|Global |load |void |Page load event. The page load event does not indicate chart display; it only indicates that the initial screen resources have finished loading. |
|Global |focus |void |The page gains focus. |
|Dashboard |dashboardChange | |Dashboard or Sheet page switch event<br><br><br>* `dashboardId`: Target dashboard ID (after switching)<br><br>* `sheetId`: Target Sheet page ID (after switching) |
|Dashboard |dashboardHeightChange | |When the dashboard layout changes, the height information is returned.<br><br><br>* `height`: Current dashboard container height (pixels) |
|Dashboard |dashboardCreate | |Create dashboard<br><br><br>* `dashboardId`: Newly created dashboard ID |
|Dashboard |dashboardSave | |Save dashboard<br><br><br>* `dashboardId`: Saved dashboard ID |
|Dashboard |dashboardSaveStatusChange |boolean |When the dashboard save status changes, it returns whether it has been saved. |
|Dashboard |dashboardBackClick |void |After enabling the configuration feature `dashboard.enableCustomEditBackClickHandler` = `true`, the default handling of the dashboard edit back event is blocked, and custom handling is performed. |
|Dashboard |enterVizQuery | |Triggered when clicking the dashboard chart title, edit icon, or enter visualization query icon.<br><br><br>* `reportId`: Report ID of the clicked chart<br><br>* `dataSetId`: Data set ID associated with the chart |
|VizQuery |vizQueryDataSetChange | |Switch data set<br><br><br>* `dashboardId`: Target dashboard ID (after switching) |
|VizQuery |vizQueryQuery | |Query completed<br><br><br>* `queryId`: Unique identifier of the current query |
|VizQuery |vizQuerySave | |Save chart<br><br><br>* `reportId`: Saved chart report ID<br><br>* `dashboardId`: Optional, dashboard ID to which the chart belongs (if saved to a dashboard) |
|Report |chartItemSelect |{ data: Record<Id, string |number\>, fieldMap: Record<Id, FieldInfo\>, fieldId?: Id, reportId?: number }<br><br><br>* `data`: Query result row data<br><br>* `fieldMap`: Field information key\-value pairs<br><br>* `fieldId`: Metric ID when selecting a table<br><br>* `reportId`: Chart ID |


<span id="_2-代码示例"></span>
# Code example

The following is a code example for listening to the dashboard save event:

```Plain
import React from 'react'
import ReactDOM from 'react-dom'

interface AeolusEvent extends Event {
  detail: {
    type: string;
    data?: any
  }
}

class BIComponent extends React.Component {
  componentDidMount() {
    /**
     * Using `document.querySelector(YOUR_SELECTOR)` or `ref.current` to access the aeolus component dom element, 
     * and call `addEventListener` with your listener
     * @example ref.current.addEventListener('aeolusevent', ...)
     */
    document.querySelector('bi-dashboard').addEventListener('aeolusevent', (e: BIEvent) => {
      const { type, data } = e.detail
      if (type === 'dashboardChange') { console.log('dashboard change', data) }
    })
  }

  render() {
    return (
      <bi-dashboard
        urlPrefix='https://console.volcengine.com/bi/datawind'
        appId='******'
        dashboardId='******'
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```
