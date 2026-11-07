---
title: "Inter-Side Preset Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Inter-Side_Preset_Properties"
---

Inter\-side preset properties are preset events and preset properties that are available on all sides.


|**Event name** |**Event display name** |**Attribute** |**Property display name** |**Attribute value type** |**Property value example or description** |**Trigger timing** |
|---|---|---|---|---|---|---|
|any_event |arbitrary event |param/$app_version |Event production version number information |string |This event is a reserved event and does not represent any true event. |without |
|any_active_event |arbitrary active event |param/$app_version |Event production version number information |string ||without |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">any_event 'and any_active_event' are not events that will be actually reported, but "pseudo\-events" after removing the event filter when using all reported events, which is convenient for you to use when querying and analyzing, so these two events will not be billed.</div>


For details of preset events and preset properties specific to each side, please refer to the preset event/property document of the corresponding side.
