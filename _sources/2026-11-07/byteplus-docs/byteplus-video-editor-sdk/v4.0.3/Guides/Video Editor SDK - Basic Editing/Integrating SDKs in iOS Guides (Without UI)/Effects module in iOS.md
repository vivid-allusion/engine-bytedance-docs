---
title: "Effects module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-effects-module-in-ios"
---

Effects module helps enhance visual effects of videos and images in your editing project. When using the Effect module, you can modify videos or images to better convey your intent. Effects module is categorized into two types: global effects and local effects. Global effects can be applied to a dedicated effect track while local effects can be directly added to their corresponding slots.

<span id="1f1cfa0f"></span>
# Naming conventions

For easier reference, the following names are used to represent related objects:


|**Class Name** |**Description** |
|---|---|
|nle |Refers to an `NLEInterface_OC` object. |
|modle |Refers to an `NLEModel` object. |
|track |Refers to an `NLETrack_OC` object. |
|slot |Refers to an `NLETrackSlot_OC` object. |
|effect |Refers to an `NLEEffect_OC` object. |
|segment |Refers to an `NLESegmentEffect_OC` object. |
|resource |Refers to an `NLEResourceNode_OC` object. |


<span id="5add46f4"></span>
# Module description

The following table introduces data classes related to the effects module.


|**Class Name** |**Description** |
|---|---|
|NLEResourceNode_OC |The resource module used to construct resources and record resource information. |
|NLESegmentEffect_OC |The effect segment. It is linked to a specific `resource`. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific transition segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="0a10bf61"></span>
# Creating an effect resource

Before creating an effect resource, ensure that you have obtained the address of your target effect resource. For example, `xx/ve_effect.bundle/fugumanhua_6945243963893760013/fugumanhua_6945243963893760013`. Then, you can proceed to construct `resource` (class type: NLEResourceNode_OC) with the address that you have obtained.

```Swift
func _effectResource(with path: String) -> NLEResourceNode_OC {
    // 1. get effect path
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    //  2. create a resource
    let resource = NLEResourceNode_OC()
    resource.resourceId = UUID().uuidString
    resource.resourceFile = url.absoluteString
    resource.resourceTag = .amazing
    resource.resourceType = .effect
    resource.resourceName = name
    return resource
}
```


<span id="6f189a8d"></span>
# Creating an effect object

This section introduces how to create an effect object.

**To create an effect object**:


1. Follow the instructions as described in "Creating an effect resource" and create `resource`.

2. Create `segment` and add `resource` to it.

3. Create `effect` and add `segment` to it.


```Swift
func _effect(with path: String) -> NLEEffect_OC {
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    // 1. create a resource 
    let resource = _effectResource(with: path)
    // 2. create a segment and add resource to the segment
    let segment = NLESegmentEffect_OC()
    segment.effectSDKEffect = resource
    segment.effectName = name
    // 3. create a effect and add segment to the effect
    let effect = NLEEffect_OC()
    effect.segmentEffect = segment
        
    return effect
}
```


<span id="13d008fe"></span>
# Global effects

This section introduces the addition, deletion and modification of global effects.

<span id="1ece311e"></span>
## Adding a global effect

This section introduces how to add a global effect.

**To add a global effect**:


1. Follow the instructions as described in "Creating an effect object" to create `effect`.

2. Create `slot` and add `segment` of the newly created `effect` object in Step 1 to the `slot`.

3. Create `track` and add `slot` to it.

4. Create `model` and add `track` to it.

5. To commit changes that you have made, call `nle.editor.commit()`.


```Swift
func addGlobal(with path: String) -> (String, String) {
    // 1. create a effect
    let effect = _effect(with: path)
    // 2. create a slot add effect.segmentEffect to the slot   
    let slot = NLETrackSlot_OC()
    effect.segmentEffect.applyTargetType = NLESegmentEffectApplyTargetType.global
    slot.segment = effect.segmentEffect
    slot.setStart(CMTime.zero)
    slot.layer = 0
    slot.setEnd(CMTime(seconds: 3, preferredTimescale: Int32(NSEC_PER_SEC)))
    // 3. create a track and add slot to the track
    let track = NLETrack_OC()
    track.layer = 0
    track.extraTrackType = .EFFECT
    track.addSlot(slot)
    // 4. add track to model
    nle.editor.model.addTrack(track)
    // 5. commit change
    nle.editor.commitAndRender()
    nle.editor.done()
        
    return (slot.uuid, effect.uuid)
}
```


<span id="a7f12941"></span>
## Deleting a global effect

For instructions on how to delete a global effect, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="436bbb6f"></span>
## Substituting a global effect

The substitution of a global effect is achieved by deleting the original effect within your target slot and adding a new effect. Before substituting a global effect, ensure that you have obtained your target `slot`. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To substitute a global effect**:


1. Delete the original effect within your target slot.

2. Follow the instructions as described in "Creating an effect object" to create `effect` and add it to your target slot.

3. To commit changes that you have made, call `nle.editor.commit()`.


```Swift
func changeGlobal(with path: String, slotID: String) -> String? {
    // 1. get slot
    guard let slot = slot(with: slotID) else {
        return nil
    }
    // 2. remove effect
    let effect = _effect(with: path)
    for e in slot.getEffect() {
        guard let e = e as? NLEEffect_OC,
            e.segmentEffect.getResNode().resourceType == .effect
        else {
            continue
        }
        slot.removeEffect(e)
    }
    // 3. add new effect
    slot.segment = effect.segmentEffect
    // 4. commit change
    nle.editor.commitAndRender()
    nle.editor.done()

    return effect.uuid
}
```


<span id="439ba44e"></span>
# Local effects

This section introduces the addition, deletion and modification of local effects.

<span id="4ddf7285"></span>
## Adding a local effect

This section introduces how to add a local effect. Before adding a local effect, ensure that you have obtained your target `slot`. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To add a local effect**:


1. Follow the instructions as described in "Creating an effect object" to create `effect` and add it to your target slot.

2. To commit changes that you have made, call `nle.editor.commit()`.


```Swift
func addPartly(with path: String, slotID: String) -> String? {
    // 1. get slot
    guard let slot = slot(with: slotID) else {
        return nil
    }
    // 2. create a effect and add the effect to slot
    let effect = _effect(with: path)
    effect.setStart(CMTime.zero)
    effect.setEnd(CMTime(seconds: 3, preferredTimescale: Int32(NSEC_PER_SEC)))
    effect.layer = 0
    effect.segmentEffect.applyTargetType = NLESegmentEffectApplyTargetType.mainVideo
    slot.addEffect(effect)
    // 3. commit change
    nle.editor.commitAndRender()
    nle.editor.done()

    return effect.uuid
}
```


<span id="d2a206c0"></span>
## Deleting a local effect

This section introduces how to delete a local effect. Before deleting a local effect, ensure that you have obtained the `slot` that contains the local effect. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".


1. To find your target effect by `effect.uuid`, use `slot.getEffect()`.

2. To delete your target effect, call `slot.removeEffect()`.

3. To commit changes that you have made, call `nle.editor.commit()`.


```Swift
func removePartly(with slotID: String, effectID: String) {
    // 1. get slot
    guard let slot = slot(with: slotID),
        let effects = slot.getEffect() as? [NLEEffect_OC],
        let effect = effects.first(where: {
            // 2. find the effect based on uuid
            $0.uuid == effectID
        }) else {
        return
    }
    // 3. remove effect     
    slot.removeEffect(effect)
    // 4. commit change
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


<span id="4e5f296a"></span>
## Substituting a local effect

The substitution of a local effect is achieved by modifying `effect.segmentEffect`. Before substituting a local effect, ensure that you have obtained the `slot` that contains the local effect. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".


1. To find your target effect by `effect.uuid`, use `slot.getEffect()`.

2. Follow the instructions as described in "Creating an effect resource" to create `resource` and add it to `effect.segmentEffect`.

3. To commit changes that you have made, call `nle.editor.commit()`.


```Swift
func changePartly(with path: String, slotID: String, effectID: String) {
    // 1. get slot
    guard let slot = slot(with: slotID),
        let effects = slot.getEffect() as? [NLEEffect_OC],
        let effect = effects.first(where: {
            // 2. find the effect based on uuid
            $0.uuid == effectID
        }) else {
        return
    }
    let url = URL(fileURLWithPath: path)
    let name = url.deletingPathExtension().lastPathComponent
    // 3. create a resource and add the resource to effect.segmentEffect  
    let resource = _effectResource(with: path)
        
    let segment = effect.segmentEffect
    segment.effectSDKEffect = resource
    segment.effectName = name
    segment.applyTargetType = NLESegmentEffectApplyTargetType.mainVideo
    // 4. commit change
    nle.editor.commitAndRender()
    nle.editor.done()
}
```
