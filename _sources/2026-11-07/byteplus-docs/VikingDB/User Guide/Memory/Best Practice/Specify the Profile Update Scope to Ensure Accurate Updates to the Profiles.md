---
title: "Specify the Profile Update Scope to Ensure Accurate Updates to the Profiles"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Specify_the_Profile_Update_Scope_to_Ensure_Accurate_Updates_to_the_Profiles"
---

In the AddSession interface, there is an optional field called `profiles`, which is used to define a list of profile information that requires special attention or updates. If not defined, the system will automatically determine which profiles to update. If manually specified, updates will only be performed within the specified profile scope.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|profiles |Array of Object |No |List of profile information that needs special attention or updates. The system will attempt to associate processed events with these profiles. |
|* profile_type |String |Yes |Profile type name, must be an profile type already defined in the memory collection. |
|* profile_scope |Array of Object |Yes |Specific profile instance list. Each object contains properties used to uniquely identify and define the profile instance (these properties should be marked as UseProvided: true or IsPrimaryKey: true in the corresponding ProfileTypeSchema), for example: |


**When is it necessary to specify the profile update scope?** 

When using template profiles, the default dimension for profile memory is `user_id`. If a "custom primary key field" (`"IsPrimaryKey": true`) is not defined for a profile, each profile rule will maintain one record per `user_id`. The default user profile (`user_profile`) in the template is a typical example of profile memory at the `user_id` dimension.

**Profile Memory with Custom Primary Key**

Building on the keyless profile memory, we also support profile memory with a given primary key. For example, if we want to track a user’s memory of a specific movie, we can define a primary key field called `movie_name`. In this case, the actual storage primary key becomes: `['movie_name', 'user_id']`. We will maintain a state for each `movie_name` under each user, and retrieval can be performed based on the profile rule name and the movie name.

Configuration example:

Event Rule

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f597131370ad44e99bb6dc3911b3e8b2~tplv-goo7wpa0wc-image.image) </span>

Profile Rule

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52c83cfc7d574e248a137f6c01f08499~tplv-goo7wpa0wc-image.image) </span>

**Defining the Scope for Custom Primary Key Extraction**

The above configuration achieves the following effect: allowing the large model to extract `movie_name`. However, in more customized scenarios, we may want the information extracted by the large model to be associated with business data. For example, in movie review analysis, we might want the memory of reviews to be linked to a unique record in our internal movie database (or in an educational scenario, to a specific record in a knowledge point collection). In such cases, if the primary key is extracted by the large model first and then associated with business data, deviations may occur (e.g., inconsistencies in the granularity of knowledge points).

Our approach allows users to provide a primary key scope for profiles when extracting memories, specifying the profile scope for each dialogue segment when uploading events.

When calling the AddSession interface, the `profiles` field can be provided to constrain the large model to only focus on the specified profiles when extracting content. For example:

```Python
payload = {
    "collection_name": "collection_name",
    "session_id": "xxx",
    "messages": [
    ...
    ],
    "metadata": {
    ...
    },
    "profiles": [
        {
          "profile_type": "movie_preferences",
          "profile_scope": [
            { 
              "movie_id": 201, # Movie ID from the business database
              "movie_name": "碟中谍 6：全面瓦解",
              "movie_alias": ["不可能的任务：全面瓦解", "职业特工队：叛逆之谜", "Mission: Impossible – Fallout"]
            }，
            { 
              "movie_id": 202, # Movie ID from the business database
              "movie_name": "夺宝奇兵 5：命运转盘",
              "movie_alias": ["印第安纳琼斯：命运轮盘", "Indiana Jones and the Dial of Destiny"]
            }
          ]
        }
    ]
}
```


In the `profile_scope`, it is necessary to provide semantically meaningful field information that the large model can recognize. This gives the large model more information to make "multiple\-choice" decisions rather than "fill\-in\-the\-blank" ones, similar to providing few\-shot examples to the large model.

In the example above 👆, if only the `movie_id` column is provided to the large model, when processing a new dialogue about the same movie, it is likely that two different profile entities might be extracted for the same movie.
