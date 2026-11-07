---
title: "Playlist management"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playlist-management"
---

BytePlus VOD playlists allow you to engage viewers by arranging videos for sequential playback. This guide provides step\-by\-step instructions on how to create, edit, and delete playlists through the BytePlus VOD console.

<span id="72259d30"></span>
## Create a playlist

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eda5683745624d6e9a1249cc4548fc29~tplv-goo7wpa0wc-image.image) </span>

Follow the steps below to create a playlist.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. Click **Enter space** to enter the designated space.

4. Click **Playlist management** on the left navigation bar.

5. Click **Create playlist**, and fill in the following information:

   
   |**Field** |**Description** |
   |---|---|
   |Playlist name |Enter the playlist name. It should be no more than 128 characters. |
   |Time |Select the start and end dates and times of the playlist. The start time cannot be earlier than the current time, and the end time cannot be earlier than the start time. |
   |Number of loops |(Optional) Enter the number of times the playlist should loop. The default is 1. Enter 0 for continuous playback. |
   |Video list |Click **Add video**, and select videos from your space. After selecting videos, click **Save** to proceed. You can modify the order of the videos by dragging and dropping, or by entering the desired sequence.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Unpublished videos will not play when the playlist goes live.</div><br> |
   

6. Click **Save** to save the playlist.

7. After creating a playlist, use the player SDK to start video playback. See [Playlist](https://docs.byteplus.com/docs/byteplus-vod/docs-playlist) documentation for the complete user workflow.


<span id="973c4a75"></span>
## Edit a playlist

Click **Edit** on the action bar of the designated playlist to modify the playlist name, start time, end time, loop count, video list, and change the playback order. Changes are saved upon clicking **Save**. Click **Cancel** to discard changes.

<span id="cf0edb89"></span>
## Delete a playlist

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only playlists outside their active playback time window can be deleted.</div>


Click **Delete** on the action bar of the designated playlist to delete the playlist, and then click **OK** in the pop\-up window to confirm the deletion.
