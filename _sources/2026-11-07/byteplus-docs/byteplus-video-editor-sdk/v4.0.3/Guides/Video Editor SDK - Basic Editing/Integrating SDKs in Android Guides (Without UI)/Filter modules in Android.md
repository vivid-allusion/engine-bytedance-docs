---
title: "Filter modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-filter-modules-in-android"
---

Filters are classified into three types: single\-point filters (local filters), track filters, and global filters. You can choose different types of filters on demand.

<span id="9f63e1e3"></span>
# Filter types

This table provides a clear comparison of the three types of filters, including their application scope, duration, and how to add them, along with common use cases for each filter type.


|**Filter Type** |**Application Scope** |**Duration** |**How to Add** |**Use Case** |
|---|---|---|---|---|
|Single\-point filters (local filters) |Apply to a track slot |Same as the track slot |Set the filter field of NLETrackSlot |Adding a filter to a specific track slot with the same duration |
|Track filters |Apply to the entire track |Adjustable |Set the filter field of NLETrack |Applying a filter to all track slots in the main track or different filters to different tracks |
|Global filters |Apply to multiple videos |Adjustable |Set the mainSegment field of NLETrackSlot |Applying the same filter to both the main track and PiP track |


<span id="31fa4f4d"></span>
# Module descriptions

These are some of the key modules within the SDK.


|**Modukle** |**Description** |
|---|---|
|NLETrack |* A track within an NLEModel, containing at least one track (the main track) and potentially multiple sub\-tracks.<br><br>* Tracks serve as containers for NLETrackSlot elements.<br><br>* NLETrackSlots within a track must not overlap in time.<br><br>* The NLETrackSlots in the main track should be contiguous, while those in sub\-tracks can be sparse. |
|NLETrackSlot |* A track slot that represents a time slot within a track.<br><br>* NLETrackSlots serve as containers for NLESegments and their derived classes.<br><br>* Each NLETrackSlot can contain only one NLESegment and its derived class. |
|NLEFilter |* The NLEFilter class is used to adjust filters for NLETrackSlots or NLETracks. Filters in an NLETrack affect multiple NLETrackSlots, while filters in an NLETrackSlot affect only that specific NLETrackSlot.<br><br>* Space\-Time Coordinates: The space\-time coordinates of an NLEFilter class in an NLETrack depend on the coordinates of the NLETrack.<br><br>* Components: An NLEFilter class includes an NLESegmentFilter, which contains the filter resource and effect parameters of the global filter. |
|NLESegmentFilter |A derived class of NLESegment, the NLESegmentFilter is a content class that represents a filter type. |


<span id="474c9164"></span>
# Filter module resources

The following are the filter module resources information, including its storage location, package contents, and path identification within the SDK for user reference.


* **Storage Location:**  During resource delivery, all filter resources are stored in the `ve_filter.bundle` package.

* **Contents of Each Package:**  Each `ve_filter.bundle` package includes two key components:

   * **Filter Resource:**  This package contains the primary filter resource, which is used for applying filter effects to media content.

   * **Effect Preview:**  Additionally, it includes a preview of the filter effect, allowing users to visualize how the filter will alter their media.

* **Path Identification:**  To access these resources within the SDK, the path to the filter is indicated by the red box in the diagram below, ensuring that the SDK can locate and utilize the filter resource effectively.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5ec1e01c62741eaa297cedbdedcd17f~tplv-goo7wpa0wc-image.image" width="456px" /></div>


<span id="119517b2"></span>
# Adding filters

Users can add the three filters by following these code samples.

<span id="3dfec1a9"></span>
## Adding global filters

You can add a global filter by following these steps.

Before beginning, take note of the following:


* **Filter Selection:**  In this example, we demonstrate how to add a global filter. You can choose built\-in filters or download filters from your server that suit your business needs.

* **Built\-In Filters:**  Built\-in filters are stored in the assets directory of the sample code. When you click the "Add" button, a copying logic is executed to copy these filters to the SD card of your mobile phone.

* **Filter Path:**  The path to the built\-in filters on the SD card is directly used in the following code block.


**To add a global filter:** 


1. Replace the path with the actual path where your filters are stored.

   ```Kotlin
   // Replace this path with the actual path where your filters are stored.
   resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"
   ```
   

2. Determine the video duration in microseconds. The duration depends on the longest track in the video.

   ```Kotlin
   // Obtain the duration of the video in μs.
   val playDuration = nleMediaSession.playerApi.duration
   ```
   

3. Add the filter to a new or existing track.

   ```Kotlin
   nleEditor.model.addTrack(NLETrack().apply {
       // Whether to set the track as the main track. Default value: false.
       mainTrack = false
   
       // Add a track filter. You can find the filter track by searching for track filters in subsequent steps.
       extraTrackType = NLETrackType.FILTER
   ```
   

4. Set the filter duration in microseconds.

   ```Kotlin
   addSlot(NLETrackSlot().apply {
       // The start time of the filter in μs. This parameter is required.
       startTime = 0
   
       // The end time of the filter in μs. This parameter is required.
       endTime = playDuration
   ```
   

5. Define the filter by setting the resource type to `FILTER` and setting the tag to `AMAZING`.

   ```Kotlin
   mainSegment = NLESegmentFilter().apply {
       effectSDKFilter = NLEResourceNode().apply {
           // The path of the filter resource in the SD card.
           resourceFile =
               "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"
           // Set the resource type to FILTER.
           resourceType = NLEResType.FILTER
           // Set the tag to AMAZING. This parameter is required.
           resourceTag = NLEResTag.AMAZING
       }
   })
   ```
   

6. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full sample code**

```Kotlin
/**
 * This method shows how to add a global filter. 
 * 1. Some built-in filters are used in this example for demonstration. You can download filters that meet your business requirements from the server. 
 * 2. The built-in filters are stored in the assets directory of the sample code. When the "Add" button is clicked, the copy logic is executed to copy the filters to the SD card of the mobile phone. 
 * 3. The path of the built-in filters in the SD card is directly used in the following code block. Replace the path with the actual path where your filters are stored. 
 */

/**
 * Assume that the duration of the video is unknown when you add the filter. The duration depends on the length of the video file that you select from the album.
 * Therefore, in the following code, you need to obtain the duration of the video first. The duration of the filter depends on the duration of the video.
 */

/**
 * Obtain the duration of the video in μs. 
 * The duration depends on the longest track. 
 */
val playDuration = nleMediaSession.playerApi.duration

/**
 *  For demonstration, we add the filter to a new track.
 */
nleEditor.model.addTrack(NLETrack().apply {
    /**
     * Whether to set the track as the main track. Default value: false.
     */
    mainTrack = false

    /**
     * Add a track filter. You can find the filter track by searching for track filters in subsequent steps.
     */
    extraTrackType = NLETrackType.FILTER

    addSlot(NLETrackSlot().apply {
        /**
         * The start time of the filter in μs. This parameter is required.
         */
        startTime = 0

        /**
         * The end time of the filter in μs. This parameter is required.
         */
        endTime = playDuration

        mainSegment = NLESegmentFilter().apply {
            effectSDKFilter = NLEResourceNode().apply {
                // The path of the filter resource in the SD card.
                resourceFile =
                    "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"

                // Set the resource type to FILTER.
                resourceType = NLEResType.FILTER
                // Set the tag to AMAZING. This parameter is required.
                resourceTag = NLEResTag.AMAZING
            }
        }
    })
})

/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="9d5d8dd4"></span>
## Adding single\-point filters

These steps illustrate how to add a single\-point filter (local filter), including filter selection, filter application to a video slot, and the final step of committing changes for the filter effect to be applied to the selected slot.


* **Filter Selection:**  In this example, we demonstrate how to add a single\-point filter (local filter). You can choose built\-in filters or download filters that meet your business requirements from your server.

* **Built\-In Filters:**  Built\-in filters are stored in the assets directory of the sample code. When the "Add" button is clicked, a copying logic is executed to copy the filters to the SD card of your mobile phone.

* **Filter Path:**  The path to the built\-in filters on the SD card is directly used in the following code block.


**To add a single\-point filter:** 


1. Replace the path with the actual path where your filters are stored.

   ```Kotlin
   // Replace this path with the actual path where your filters are stored.
   resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"
   ```
   

2. Obtain the first video slot in the main track.

   ```Kotlin
   val firstSlot = nleEditor.model.mainTrack.sortedSlots.firstOrNull()
   ```
   

3. Add the filter to the selected video slot. The filter's properties including its path, resource type, and tag are defined in the `NLESegmentFilter`.

4. Define the filter by setting the resource type to `FILTER` and setting the tag to `AMAZING`.

   ```Kotlin
   firstSlot?.apply {
       this.addFilter(NLEFilter().apply {
           segment = NLESegmentFilter().apply {
               effectSDKFilter = NLEResourceNode().apply {
                   // The path of the filter resource in the SD card.
                   resourceFile =
                       "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"
                   // Set the resource type to FILTER.
                   resourceType = NLEResType.FILTER
                   // Set the tag to AMAZING. This parameter is required.
                   resourceTag = NLEResTag.AMAZING
               }
               // Set the initial intensity of the filter.
               intensity = 1f
           }
       })
   }
   ```
   

5. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full sample code**

```Kotlin
/**
 * This method shows how to add a single-point filter (local filter). 
 * 1. Some built-in filters are used in this example for demonstration. You can download filters that meet your business requirements from the server. 
 * 2. The built-in filters are stored in the assets directory of the sample code. When the "Add" button is clicked, the copy logic is executed to copy the filters to the SD card of the mobile phone. 
 * 3. The path of the built-in filters in the SD card is directly used in the following code block. Replace the path with the actual path where your filters are stored. 
 */

/**
 * A single-point filter (local filter) applies to only one video slot. For demonstration, we add the filter to a video slot in the main track.
 */
val firstSlot = nleEditor.model.mainTrack.sortedSlots.firstOrNull()
firstSlot?.apply {
    this.addFilter(NLEFilter().apply {
        // The startTime and endTime parameters do not take effect on local filters.
        segment = NLESegmentFilter().apply {
            effectSDKFilter = NLEResourceNode().apply {
                // The path of the filter resource in the SD card.
                resourceFile =
                    "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"

                // Set the resource type to FILTER.
                resourceType = NLEResType.FILTER
                // Set the tag to AMAZING. This parameter is required.
                resourceTag = NLEResTag.AMAZING
            }
             // Set the initial intensity of the filter.
            intensity = 1f
        }
    })
}

/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="2055b053"></span>
## Adding track filters

These steps explain how to add a track filter, including filter selection, filter application to the main track, and the final steps of committing changes and refreshing to view the effect.


1. **Filter Selection:**  In this example, we demonstrate how to add a track filter. You can use built\-in filters or download filters that suit your business requirements from a server.

2. **Built\-In Filters:**  Built\-in filters are stored in the assets directory of the sample code. When the "Add" button is clicked, the copy logic is executed to copy the filters to the SD card of your mobile phone.

3. **Filter Path:**  The path to the built\-in filters on the SD card is directly used in the following code block.


**To add a single\-point filter:** 


1. Create a new `NLEFilter` and apply settings to it.

2. Inside the`NLEFilter`, define a filter segment using the `segment`property.

3. Add the filter to the main track by creating an `NLEFilter`.

4. Within the filter segment, specify the filter resource using an`NLEResourceNode`. Set the`resourceFile`property to the path of the filter resource on the SD card. Replace the provided path with the actual path where your filter is stored.

5. ```Kotlin

```



// Replace this path with the actual path where your filters are stored.

resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"

```Plain Text

6. Indicate the resource type as `FILTER` by setting the`resourceType` property to `NLEResType.FILTER`.
7. Specify a tag for the filter using the `resourceTag` property. This parameter is required and can be set to any meaningful value, for example, "AMAZING".
   ```Kotlin
   resourceTag = NLEResTag.AMAZING 
```



8. Set the initial intensity of the filter using the`intensity`property. You can adjust the intensity as needed.

   ```Kotlin
   intensity = 1f 
   ```
   

9. If you want to adjust the duration of the filter when adding a track filter, you can set the `startTime`and`endTim`e parameters of the`NLESegmentFilter`. In this example, the filter starts at 0 seconds and ends at the 5th second. You can adjust these values according to your requirements.

   ```Kotlin
   this.startTime = 0 // Start from the 0 second.
   this.endTime = 5 * 1000000 // End at the 5th second.
   ```
   

10. Commit the changes.


```Kotlin
nleEditor.commit() 
```


**Full sample code**

```Kotlin
/**
 * This method shows how to add a track filter. 
 * 1. Some built-in filters are used in this example for demonstration. You can download filters that meet your business requirements from the server. 
 * 2. The built-in filters are stored in the assets directory of the sample code. When the "Add" button is clicked, the copy logic is executed to copy the filters to the SD card of the mobile phone. 
 * 3. The path of the built-in filters in the SD card is directly used in the following code block. Replace the path with the actual path where your filters are stored. 
 */

/**
 * A track filter applies to a track. For demonstration, we add the filter to the main track.
 */
nleEditor.model.mainTrack.addFilter(NLEFilter().apply {
    segment = NLESegmentFilter().apply {
        effectSDKFilter = NLEResourceNode().apply {
            //  The path of the filter resource in the SD card.
            resourceFile =
                "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/heben_7044036714998661151/heben_7044036714998661151"

            // Set the resource type to FILTER.
            resourceType = NLEResType.FILTER
            // Set the tag to AMAZING. This parameter is required.
            resourceTag = NLEResTag.AMAZING
        }
        //  Set the initial intensity of the filter.
        intensity = 1f
    }

   // When you add a track filter, you can set the startTime and endTime parameters of the NLESegmentFilter to adjust the duration of the filter.
    this.startTime = 0 // Start from the 0 second.
    this.endTime = 5 * 1000000 // End at the 5th second.
})

/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()

/**
 * For track filters, you must refresh to view the effect.
 */
nleMediaSession.playerApi.refreshCurrentFrame()
```


<span id="8e1e0051"></span>
# Deleting filters

Users can delete the three filters by following these code samples.

<span id="a087995b"></span>
## Deleting global filters

By following these steps, you can effectively delete global filters from all tracks that use the filter. Make sure to commit the changes for the effect to no longer appear in the preview video.

**To delete global filters:** 


1. Iterate through all tracks in the `NLEModel` to locate tracks that use the global filter.

   ```Kotlin
   nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.FILTER }.forEach {
   ```
   

2. Within each track that uses the filter, iterate through its sorted slots to identify filter slots. These slots represent segments where the global filter is applied.

   ```Kotlin
   it.sortedSlots.forEach { filterSlot ->
   ```
   

3. Check if the slot's main segment is of the filter type.

   ```Kotlin
   val filterSegment = NLESegmentFilter.dynamicCast(filterSlot.mainSegment)
   if (filterSegment != null) {
   ```
   

4. Once a filter slot is identified, remove it from the track to delete the global filter effect from that segment.

   ```Kotlin
   it.removeSlot(filterSlot) 
   
   ```
   

5. (Optional) If, after removing filter slots, the track has no remaining slots, consider deleting the entire track to remove all related filter effects.

   ```Kotlin
   if (it.sortedSlots.size <= 0) {
       nleEditor.model.removeTrack(it)
   ```
   

6. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full sample code**

```Kotlin
/**
 * This method shows how to delete a global filter.
 * 1. For demonstration, this method deletes the global filter from all tracks that use the filter.
 * 2. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you delete global filters,
 * You can check all NLETrackSlots in the NLEModel to find the slots that you need to delete.
 */
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.FILTER }.forEach {
    it.sortedSlots.forEach { filterSlot ->
        val filterSegment = NLESegmentFilter.dynamicCast(filterSlot.mainSegment)
        if (filterSegment != null) {
            it.removeSlot(filterSlot)
        }
    }
    // If you need to delete all slots in the track, delete the track instead.
 if (it.sortedSlots.size <= 0) {
        nleEditor.model.removeTrack(it)
    }
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="e3dd5459"></span>
## Deleting single\-point filters

By following these steps, you can effectively delete local filters from all tracks that use the filter. Remember to commit the changes to ensure the deleted filter effects no longer appear in the preview video.

**To delete single\-point filters:** 


1. Iterate through all sorted slots in the main track of the `NLEModel`.

   ```Kotlin
   nleEditor.model.mainTrack.sortedSlots.forEach {
   ```
   

2. For each slot in the main track, delete all filters from that slot.

   ```Kotlin
   it.clearFilter()
   ```
   

3. To ensure the deleted local filters' effects are no longer visible in the preview video, submit the modified data model.

   ```Kotlin
   nleEditor.commit()
   ```
   


**Full sample code**

```Kotlin
/**
 * This method shows how to delete a single-point filter (local filter).
 * 1. For demonstration, this method deletes the local filter from all tracks that use the filter.
 * 2. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you delete local filters,
 * You can check all NLETrackSlots in the NLEModel to find the slots that you need to delete.
 */
nleEditor.model.mainTrack.sortedSlots.forEach {
     // Delete all filters from all slots.
    it.clearFilter()
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="2ade8fb6"></span>
## Deleting track filters

By following these steps, you can effectively delete track filters from the main track. Similar methods can be used to delete track filters from other tracks in the `NLEModel`. Remember to commit the changes and, in the case of track filters, refresh the current frame for the effect to be visible.

**To delete single\-point filters:** 


1. For each slot in the main track, delete all filters from that slot.

   ```Kotlin
   nleEditor.model.mainTrack.clearFilter()
   ```
   

2. To ensure the deleted local filters' effects are no longer visible in the preview video, submit the modified data model.

   ```Kotlin
   nleEditor.commit()
   ```
   

3. If you have deleted track filters and want to see the effect in the preview video, you must refresh the current frame. This is specifically required for track filters.

   ```Kotlin
   nleMediaSession.playerApi.refreshCurrentFrame()
   ```
   


**Full sample code**

```Kotlin
/**
 * This method shows how to delete a single-point filter (local filter).
 * 1. For demonstration, this method deletes the local filter from all tracks that use the filter.
 * 2. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you delete local filters,
 * You can check all NLETrackSlots in the NLEModel to find the slots that you need to delete.
 */
nleEditor.model.mainTrack.sortedSlots.forEach {
     // Delete all filters from all slots.
    it.clearFilter()
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="858a5908"></span>
# Modifying filters

Users can modify the three filters by following these code samples.

<span id="f719c25c"></span>
## Modifying global filters

By following these steps, you can effectively modify a global filter. Iterate through the tracks that use the filter, update the filter's parameters, and then commit the changes to see the effect in the preview video.

**To modify global filters:** 


1. Iterate the tracks in the `NLEModel` to find filter slots and update their filter parameters.

   ```Kotlin
   // Step 1: Iterate through tracks with the "FILTER" extra track type
   nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.FILTER }.forEach { track ->
   ```
   

2. Iterate the filter slots.

   ```Kotlin
      // Step 2: Iterate through filter slots in the current track
      track.sortedSlots.forEach { filterSlot ->
   ```
   

3. Modify the parameter if the filter slot contains `NLESegmentFilter`.

   ```Kotlin
          // Step 3: Check if the slot contains a filter of type NLESegmentFilter
          val filterSegment = NLESegmentFilter.dynamicCast(filterSlot.mainSegment)
          if (filterSegment != null) {
   ```
   

4. Modify the parameters by updated `effectSDKFilter`.

   ```Kotlin
              // Step 4: Modify the filter parameters
              filterSegment.effectSDKFilter = NLEResourceNode().apply {
                  // Set the path of the filter resource in the SD card.
                  resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198"
                  // Set the resource type to FILTER.
                  resourceType = NLEResType.FILTER
                  // Set the tag to AMAZING. This parameter is required.
                  resourceTag = NLEResTag.AMAZING
              }
   ```
   

5. Commit the changes.

   ```Kotlin
              // Step 5: Commit the changes
   nleEditor.commit()
   ```
   


**Full code sample**

```Kotlin
/**
 * This method shows how to modify a global filter.
 * 1. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you modify a global filter,
 * You can check all NLETrackSlots in the NLEModel to find the global filter slot to be modified.
 */
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.FILTER }.forEach {
    it.sortedSlots.forEach { filterSlot ->
        val filterSegment = NLESegmentFilter.dynamicCast(filterSlot.mainSegment)
        filterSegment?.let {
            it.effectSDKFilter = NLEResourceNode().apply {
                // The path of the filter resource in the SD card.
                resourceFile =
                    "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198"

                // Set the resource type to FILTER.
                resourceType = NLEResType.FILTER
                // Set the tag to AMAZING. This parameter is required.
                resourceTag = NLEResTag.AMAZING
            }
        }
    }
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="21d0b097"></span>
## Modifying single\-point filters

By following these steps, you can effectively modify a single\-point filter (local filter). Iterate through the slots in the main track, update the filter parameters, and then commit the changes to see the effect in the preview video.

**To modify single\-point filters:** 


1. Iterate the main tracks in the `NLEModel` to find filter slots and update their filter parameters.

   ```Kotlin
   // Step 1: Iterate through slots in the main track of the NLEModel
   nleEditor.model.mainTrack.sortedSlots.forEach { slot ->
   ```
   

2. Iterate the filter slots.

   ```Kotlin
      // Step 2: Iterate through filters in the current slot
      slot.filters.forEach { nleFilter ->
   ```
   

3. Modify the parameter if the filter slot contains `NLESegmentFilter`.

   ```Kotlin
          // Step 3: Check if the filter contains a filter segment of type NLESegmentFilter
          val filterSegment = NLESegmentFilter.dynamicCast(nleFilter.segment)
          if (filterSegment != null) {
   ```
   

4. Modify the parameters by updated `effectSDKFilter`.

   ```Kotlin
              // Step 4: Modify the filter parameters
              filterSegment.effectSDKFilter = NLEResourceNode().apply {
                  // Set the path of the filter resource in the SD card.
                  resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198"
                  // Set the resource type to FILTER.
                  resourceType = NLEResType.FILTER
                  // Set the tag to AMAZING. This parameter is required.
                  resourceTag = NLEResTag.AMAZING
              }
          }
      }
   ```
   

5. Commit the changes.

   ```Kotlin
              // Step 5: Commit the changes
   nleEditor.commit()
   ```
   


**Full code sample**

```Kotlin
/**
 * This method shows how to modify a single-point filter (local filter).
 * 1. For demonstration, this method modifies the local filter in all slots that use the local filter.
 * 2. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you modify a local filter,
 * You can check all NLETrackSlots in the NLEModel to find the local filter slot to be modified.
 */
nleEditor.model.mainTrack.sortedSlots.forEach {
    it.filters.forEach { nleFilter ->
        val filterSegment = NLESegmentFilter.dynamicCast(nleFilter.segment)
        filterSegment?.let {
            it.effectSDKFilter = NLEResourceNode().apply {
                // The path of the filter resource in the SD card.
                resourceFile =
                    "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198"

                // Set the resource type to FILTER.
                resourceType = NLEResType.FILTER
                // Set the tag to AMAZING. This parameter is required.
                 resourceTag = NLEResTag.AMAZING
            }
        }
    }
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="b50ddc82"></span>
## Modifying track filters

By following these steps, you can effectively modify track filters in the main track. Iterate through the filters, update the filter parameters, and then commit the changes to see the effect in the preview video. If needed, refresh the frame for track filters.

**To modify track filters:** 


1. Iterate the main tracks in the `NLEModel` to find filter slots and update their filter parameters.

   ```Kotlin
   // Step 1: Iterate through the filters in the main track
   nleEditor.model.mainTrack.filters.forEach {
   ```
   

2. Check the filter slots for `NLESegmentFilter`.

   ```Kotlin
      // Step 2: Check if the filter contains a filter segment of type NLESegmentFilter
      val filterSegment = NLESegmentFilter.dynamicCast(it.segment)
      if (filterSegment != null) {
   ```
   

3. Modify the parameters by updated `effectSDKFilter`.

   ```Kotlin
              // Step 3: Modify the filter parameters
              filterSegment.effectSDKFilter = NLEResourceNode().apply {
                  // Set the path of the filter resource in the SD card.
                  resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198"
                  // Set the resource type to FILTER.
                  resourceType = NLEResType.FILTER
                  // Set the tag to AMAZING. This parameter is required.
                  resourceTag = NLEResTag.AMAZING
              }
          }
      }
   ```
   

4. Commit the changes.

   ```Kotlin
              // Step 4: Commit the changes
   nleEditor.commit()
   ```
   

5. Refresh to view the track filters effect.

   ```Kotlin
   // Step 5: Refresh for track filters (if necessary)
   nleMediaSession.playerApi.refreshCurrentFrame()
   ```
   


**Full code sample**

```Kotlin
/**
 * This method shows how to modify the track filter in the main track. You can use similar methods to modify the track filters of tracks other than the main track.
 * 1. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you modify a track filter,
 * You can check all NLETracks that meet your requirement in the NLEModel to find the track whose track filter you need to modify.
 */
nleEditor.model.mainTrack.filters.forEach {
    NLESegmentFilter.dynamicCast(it.segment)?.effectSDKFilter = NLEResourceNode().apply {
        // The path of the filter resource in the SD card.    
        resourceFile =
            "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/ve_filter.bundle/wuhou_6945244045434503198/wuhou_6945244045434503198"

        // Set the resource type to FILTER.
        resourceType = NLEResType.FILTER
        // Set the tag to AMAZING. This parameter is required.
        resourceTag = NLEResTag.AMAZING
    }
}
/**
  * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
  */
nleEditor.commit()

/**
 * For track filters, you must refresh to view the effect.
 */
nleMediaSession.playerApi.refreshCurrentFrame()
```


<span id="3e7073ec"></span>
# Modifying filter intensity

This guides you through the process of adjusting the intensity of filters, ensuring that the desired effect is achieved in your video content.

<span id="65d91a50"></span>
## Modifying global filter intensity

By following these steps, you can effectively modify the intensity of global filters. Iterate through the tracks, then the filter slots, update the intensity of filter segments, and commit the changes to see the effect in the preview video.

**To modify the intensity of the global filter:** 


1. Iterate through the tracks looking for global filters

   ```Kotlin
   // Step 1: Iterate through the tracks looking for global filters
   nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.FILTER }.forEach {
   ```
   

2. Within each track, the code iterates through the filter slots to find filter segments of type `NLESegmentFilter` and modify their intensity.

   ```Kotlin
      // Step 2: Iterate through the filter slots in the track
      it.sortedSlots.forEach { filterSlot ->
   ```
   

3. Modify the intensity of filter segments

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It specifically looks for segments of type <code>NLESegmentFilter</code> and sets their intensity to <code>0.5f</code> (adjusting from the initial value of <code>1</code>).   </div>
   

   ```Kotlin
          // Step 3: Modify the intensity of filter segments
          NLESegmentFilter.dynamicCast(filterSlot.mainSegment)?.intensity = 0.5f
      }
   ```
   

4. Commit the changes.

   ```Kotlin
              // Step 4: Commit the changes
   nleEditor.commit()
   ```
   


**Full code sample**

```Kotlin
/**
 * This method shows how to modify the intensity of a global filter.
 * 1. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you modify the intensity of a global filter,
 * You can check all NLETrackSlots in the NLEModel to find the global filter slot to be modified.
 */
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.FILTER }.forEach {
    it.sortedSlots.forEach { filterSlot ->
        // Change the intensity from the initial value 1 to 0.5f.
        NLESegmentFilter.dynamicCast(filterSlot.mainSegment)?.intensity = 0.5f
    }
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="d7dd8468"></span>
## Modifying single\-point filter intensity

By following these steps, you can effectively modify the intensity of single\-point filters. Iterate through the tracks, then the filter slots, update the intensity of filter segments, and commit the changes to see the effect in the preview video.

**To modify the intensity of the single\-point filter:** 


1. Iterate through the tracks looking for single\-point filters.

   ```Kotlin
   nleEditor.model.mainTrack.sortedSlots.forEach {
   ```
   

2. Within each track, the code iterates through the filter slots to find filter segments of type `NLESegmentFilter` and modify their intensity.

   ```Kotlin
   it.filters.forEach { nleFilter ->
   ```
   

3. Change the intensity of local filter segments from the initial value of 1 to 0.5

   ```Kotlin
   NLESegmentFilter.dynamicCast(nleFilter.segment)?.intensity = 0.5f
   ```
   

4. Commit the changes.

   ```Kotlin
   nleEditor.commit()
   ```
   


**Full code sample**

```Kotlin
/**
 * This method shows how to modify the intensity of a single-point filter (local filter).
 * 1. For demonstration, this method modifies the intensity of the local filter in all slots that use the local filter.
 * 2. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you modify the intensity of a local filter,
 * You can check all NLETrackSlots in the NLEModel to find the local filter slot to be modified.
 */
nleEditor.model.mainTrack.sortedSlots.forEach {
    it.filters.forEach { nleFilter ->
        // Change the intensity from the initial value 1 to 0.5f.
        NLESegmentFilter.dynamicCast(nleFilter.segment)?.intensity = 0.5f
    }
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()
```


<span id="0d290ac2"></span>
## Modifying track filter intensity

By following these steps, you can effectively modify the intensity of track filters. Iterate through the tracks, then the filter slots, update the intensity of filter segments, and commit the changes to see the effect in the preview video.

**To modify the intensity of the track filter:** 


1. Iterate through the tracks looking for track filters.

   ```Kotlin
   nleEditor.model.mainTrack.filters.forEach {
   ```
   

2. Change the intensity of local filter segments from the initial value of 1 to 0.5

   ```Kotlin
   NLESegmentFilter.dynamicCast(it.segment)?.intensity = 0.5f
   ```
   

3. Commit the changes.

   ```Kotlin
   nleEditor.commit()
   ```
   

4. For track filters, you must refresh to view the effect.

   ```Kotlin
   nleMediaSession.playerApi.refreshCurrentFrame()
   ```
   


**Full code sample**

```Kotlin
/**
 * This method shows how to modify the intensity of a track filter in the main track. You can use similar methods to modify the intensity of track filters in tracks other than the main track.
 * 1. The architecture of the SDK is data-driven. All data is saved in the NLEModel. Therefore, when you modify the intensity of a track filter,
 * You can check all NLETracks that meet your requirement in the NLEModel to find the track whose track filter you want to modify.
 */
nleEditor.model.mainTrack.filters.forEach {
    NLESegmentFilter.dynamicCast(it.segment)?.intensity = 0.5f
}
/**
 * Submit the modified data model. This step is required. Otherwise, the effect in the preview video is not displayed.
 */
nleEditor.commit()

/**
 * For track filters, you must refresh to view the effect.
 */
nleMediaSession.playerApi.refreshCurrentFrame()
```


&nbsp;
