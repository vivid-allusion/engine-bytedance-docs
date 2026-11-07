---
title: "Upload Skills to Skill Center"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Upload_Skills_to_Skill_Center"
---

<span id="e68b08c4"></span>
## Upload skills to Skill Center

Upload a `skill.zip`archive to the Skill Center. If a skill with the same name already exists, the server level will delete the old version before uploading the new version (idempotent upsert).

<span id="47a01d4d"></span>
### Request description


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/skill/upload` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|Content\-Type |`multipart/form-data` |



* **Path** : `/dataAgent/llm/openApi/v2/skill/upload`

* **Description** : Upsert is uniquely identified by the `name`in the `SKILL.md`YAML frontmatter.


<span id="5651e7bd"></span>
### Request parameters


|Field |Location |Type |Required |Explain |
|---|---|---|---|---|
|`file` |form\-file |file |Yes |Skills `.zip`archive. The archive must contain `SKILL.md`(located in the root directory or first\-level subdirectory of the archive), and its YAML frontmatter must contain the `name`field. |
|`scene` |form\-field |string |No |Description of skill usage scenarios. When no or empty strings are passed, the server level is populated by default with the `description`field in the `SKILL.md`frontmatter. |
|`show_name` |form\-field |string |No |Skill display name (display name). When not passing or passing the empty string, take the `show_name`/ `display_name` in the frontmatter in turn; if there is still no, return to the skill `name`. |
|`tags` |form\-field |string |No |Skill tag. Supports duplicate fields ( `tags = a & tags = b`) or single field comma delimited ( `tags = a, b`); blank tags are ignored. If it is not passed, the label will not be set. |


<span id="5fa4cbac"></span>
### Skill pack structure requirements

The compressed package must contain a `SKILL.md`, and the file must start with YAML frontmatter, for example:

```Plain
---
name: my-data-analysis-skill
description: Example skill for data analysis
show_name: Sale data assistant
tags: [sales, analytics]
---

## My Data Analysis Skill

Skill description……
```



* `Name`: Required, unique skill identifier; upsert by this name to determine whether it already exists.

* `Description`: Optional; server level can be used as the default for `scene`when the request does not pass a `scene`.

* `show_name`/ `display_name`: optional; default value for the skill display name (overrides when requesting explicit `show_name`).

* Packaging automatically skips `.git`, `__pycache__`, hidden files/directories, etc.


<span id="d457f403"></span>
### Request example

<span id="0fa04511"></span>
#### 1) Minimum available calls (upload only zip)

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/skill/upload" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -F 'file=@/path/to/my-skill.zip;type=application/zip' \
  --silent | jq
```


<span id="f7a4ea71"></span>
#### 2) with `scene`, `show_name`and `tags`

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/skill/upload" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -F 'file=@/path/to/my-skill.zip;type=application/zip' \
  -F 'scene=Data Q&A skills for sales scenarios' \
  -F 'show_name=Sale data assistant' \
  -F 'tags=sales' \
  -F 'tags=analytics' \
  --silent | jq
```


`Tags`can also be separated by commas in a single field (equivalent to the two duplicate fields above), for example:

```Plain
-F 'tags=sales,analytics'
```


<span id="e875afdd"></span>
### Return parameters


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.name` |string |`my-data-analysis-skill` |Skill name (unique identifier). Usually from the YAML frontmatter `name`field `SKILL.md`within the skill pack. |
|`data.skillUid` |string |`my-data-analysis-skill` |A skill unique identifier that is used for subsequent reference to the skill (e.g. binding a skill in a scenario/choreography). Generally consistent with `data.name`(subject to actual return). |
|`data.version` |string |`v1.0` |Skill version number (subject to actual return). |
|`data.replaced` |boolean |`false` |Whether to replace an existing skill with the same name: `true`means upsert overwrite occurred (the skill with the same name existed before uploading); `false`means first upload/new. |


<span id="faed6c91"></span>
#### Back to example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "name": "my-data-analysis-skill",
    "replaced": false,
    "skillUid": "my-data-analysis-skill",
    "version": "v1.0"
  },
  "msg": {}
}
```
