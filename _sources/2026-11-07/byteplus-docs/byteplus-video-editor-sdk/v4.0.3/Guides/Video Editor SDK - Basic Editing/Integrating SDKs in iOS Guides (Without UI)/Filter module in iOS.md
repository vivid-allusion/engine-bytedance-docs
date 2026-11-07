---
title: "Filter module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-filter-module-in-ios"
---

Filter module is used to add filters for videos and images in your project. Filters are classified into three types: single\-point filters (local filters) and global filters. Global filters are applied to a single filter track while local filters are applied to their corresponding slots.

<span id="3b74d6ed"></span>
# Naming conventions

For easier reference, the following names are used to represent related objects:


|**Name** |**Referent Object** |
|---|---|
|nle |Refers to an `NLEInterface_OC` object. |
|modle |Refers to an `NLEModel` object. |
|track |Refers to an `NLETrack_OC` object. |
|slot |Refers to an `NLETrackSlot_OC` object. |
|filter |Refers to an `NLEFilter_OC` object. |
|segment |Refers to an `NLESegmentFilter_OC` object. |
|resource |Refers to an `NLEResourceNode_OC` object. |


<span id="2803c9c3"></span>
# Module description

The following table introduces data classes related to the filter module.


|**Class Name** |**Description** |
|---|---|
|NLEInterface_OC |The universal interface for NLE. |
|NLEModel |The core data module for NLE. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |
|NLESegmentFilter_OC |The filter segment module. |
|NLEFilter_OC |The filter data module. |


<span id="0c692a82"></span>
# Creating a filter resource

Before creating a filter, ensure that you have obtained the address of your target filter. For example, `xx/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198`.

Use the address that you have obtained to construct `resource`(Class type: `NLEResourceNode_OC`) .

**Sample code**

```Swift
func _filterResource(with path: String) -> NLEResourceNode_OC {
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    
    let resource = NLEResourceNode_OC()
    resource.resourceId = UUID().uuidString
    resource.resourceFile = url.absoluteString
    resource.resourceTag = .amazing
    resource.resourceType = .filter
    resource.resourceName = name
    return resource
}
```


<span id="04b06ec3"></span>
# Creating a filter object

This section introduces how to create a filter object.

**To create a filter object**:


1. Create `resource`. For instructions on how to create `resource`, refer to "Creating a filter".

2. Create `segment` and add `resource` to it.

3. Create `filter` and add `segment` to it.


**Sample code**

```Swift
func _filter(with path: String) -> NLEFilter_OC {
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    
    let resource = _filterResource(with: path)
    
    let segment = NLESegmentFilter_OC()
    segment.effectSDKFilter = resource
    segment.filterName = name
    segment.intensity = 0.8
    segment.applyTargetType = Int(NLESegmentEffectApplyTargetType.global.rawValue)
    
    let filter = NLEFilter_OC()
    filter.segmentFilter = segment
    
    return filter
}
```


<span id="bf966cc2"></span>
# Global filters

This section introduces the addition, deletion and modification of global filters.

<span id="382990b3"></span>
## Adding a global filter

This section introduces the addition of global filters.

**To add a global filter**:


1. Create `filter`. For instructions on how to create `filter`, refer to "Creating a filter object".

2. Create `segment` (class type: `NLESegmentFilter_OC`).

3. Create `slot` and add `filter` and `segment` that you have created in Step 1 and Step 2 to it.

4. Create `track` and add `slot` to it.

5. Create `model` and add `track` to it.

6. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
func addGlobal(with path: String) -> (String, String) {
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    
    let filter = _filter(with: path)
    
    let mainFilterSegment = NLESegmentFilter_OC()
    mainFilterSegment.filterName = name
    
    // Different from Android，the iOS guide demand seting up segment and calling addFilter
    let slot = NLETrackSlot_OC()
    slot.segment = mainFilterSegment
    slot.addFilter(filter)
    slot.setStart(CMTime.zero)
    slot.layer = 0
    slot.duration = CMTime(seconds: 3, preferredTimescale: Int32(NSEC_PER_SEC))
    
    let track = NLETrack_OC()
    track.layer = 0
    track.extraTrackType = .FILTER
    track.addSlot(slot)
    
    nle.editor.model.addTrack(track)
    nle.editor.commitAndRender()
    nle.editor.done()
    
    return (slot.uuid, filter.uuid)
}
```


<span id="4097e628"></span>
## Deleting a global filter

For instructions on how to delete a global filter, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="421407ec"></span>
## Substituting a global filter

The substitution of a global filter is achieved by deleting the global filter within your target slot and then adding a new global filter. Before substituting the global filter, ensure that you have obtained the `slot`. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".


1. Modify `slot.segment.filterName`.

2. Delete all filters of your target slot.

3. Create a new filter and add it to your target slot. For instructions on how to create a global filter, refer to "Creating a filter object".

4. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
func changeGlobal(with path: String, slotID: String) -> String? {
    guard let slot = slot(with: slotID) else {
        return nil
    }
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    
    if let mainFilterSegment = slot.segment as? NLESegmentFilter_OC  {
        mainFilterSegment.filterName = name
    }
    
    // remove all filters on the slot
    for f in slot.getFilter() {
        guard let f = f as? NLEFilter_OC,
              f.segmentFilter.getResNode().resourceType == .filter
        else {
            continue
        }
        slot.removeFilter(f)
    }
    
    let filter = _filter(with: path)
    slot.addFilter(filter)
    nle.editor.commitAndRender()
    nle.editor.done()
    
    return filter.uuid
}
```


<span id="a822a9d1"></span>
# Local filters

This section introduces the addition, deletion and modification of local filters.

<span id="27f54bb2"></span>
## Adding a local filter

This section introduces the addition of local filters. Before adding a local filter, ensure that you have obtained `slot`. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To add a local filter**:


1. Create a filter and add it to your target slot. For instructions on how to create a local filter, refer to "Creating a filter object".

2. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
func addPartly(with path: String, slotID: String) -> String? {
    guard let slot = slot(with: slotID) else {
        return nil
    }
    let filter = _filter(with: path)
    slot.addFilter(filter)
    
    nle.editor.commitAndRender()
    nle.editor.done()
    
    return filter.uuid
}
```


<span id="3053d417"></span>
## Deleting a local filter

This section introduces the deletion of local filters. Before deleting a local filter, ensure that you have obtained `slot`. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To delete a local filter**:


1. To find your target filter by `filter.uuid`, use `slot.getFilter()`.

2. To delete a local filter, call `slot.removeFilter()`.

3. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
func removePartly(with slotID: String, filterID: String) {
    guard let slot = slot(with: slotID),
          let filters = slot.getFilter() as? [NLEFilter_OC],
          let filter = filters.first(where: {
              $0.uuid == filterID
          }) else {
        return
    }
    slot.removeFilter(filter)
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


<span id="dbfd3050"></span>
## Substituting a local filter

This substitution of a local filter is achieved by modifying `filter.segmentFilter`. Before substituting a local filter, ensure that you have obtained `slot`. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To substitute a local filter**:


1. To find your target filter by `filter.uuid`, use `slot.getFilter()`.

2. Create `resource` and add it to `filter.segmentFilter`. For instructions on how to create a filter resource, refer to "Creating a filter resource".

3. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
func changePartly(with path: String, slotID: String, filterID: String) {
    guard let slot = slot(with: slotID),
          let filters = slot.getFilter() as? [NLEFilter_OC],
          let filter = filters.first(where: {
              $0.uuid == filterID
          }) else {
        return
    }
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    
    let resource = _filterResource(with: path)
    
    let segment = filter.segmentFilter
    segment.effectSDKFilter = resource
    segment.filterName = name
    segment.intensity = 0.8
    segment.applyTargetType = Int(NLESegmentEffectApplyTargetType.global.rawValue)
    
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


<span id="3e9fb497"></span>
# Modifying filter intensity

This section introduces how to modify filter intensity. Before modifying filter intensity, ensure that you have obtained `slot` that contains your target filter. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

For global filters and local filters, the referent object of `slot` differs. Their differences are as follows:


* For global filters, `slot` refers to the slot within a filter track.

* For local filters, `slot` refers to the slot within a video track, such as the main track.


**To modify filter intensity**:


1. To find your target filter by `filter.uuid`, use `slot.getFilter()`.

2. Modify `filter.segmentFilter.intensity`.

3. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
func changeIntensity(with intensity: Float, slotID: String, filterID: String) {
    guard let slot = slot(with: slotID),
          let filters = slot.getFilter() as? [NLEFilter_OC],
          let filter = filters.first(where: {
              $0.uuid == filterID
          }) else {
        return
    }
    
    filter.segmentFilter.intensity = intensity
    nle.editor.commitAndRender()
    nle.editor.done()
}
```
