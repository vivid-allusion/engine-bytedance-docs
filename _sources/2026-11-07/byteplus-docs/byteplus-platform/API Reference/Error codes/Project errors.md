---
title: "Project errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-project"
---

Below are project related error codes.


|**Error** |**Message** |**HTTP Status Code** |
|---|---|---|
|ProjectNotExist |Project `%s` can not be found. |404 |
|ProjectAlreadyExists |Project `%s` already exists. |409 |
|InvalidProjectName |Invalid ProjectName `%s`, err: `%s`. |400 |
|InvalidNewProjectName |Invalid NewProjectName `%s`, err: `%s`. |400 |
|ProjectNameAlreadyExists |ProjectName `%s` is already used. |409 |
|ProjectDeleteConflictWithUser |Cannot delete Project `%s`, must remove all User first. |409 |
|ProjectDeleteConflictWithRole |Cannot delete Project `%s`, must remove all Role first. |409 |
|ProjectDeleteConflictWithResource |Cannot delete Project `%s`, must remove all resource first. |409 |
|ProjectIdentityNotExist |Identity `%+v` can not be found. |404 |
|InvalidProjectIdentityType |Invalid IdentityType `%s`, err: `%s`. |400 |
|AddProjectUserConflict |User `%s` already be added to the Project `%s`. |409 |
|RemoveProjectUserConflict |User `%s` not be added to the Project `%s`. |409 |
|AddProjectRoleConflict |Role `%s` already be added to the Project `%s`. |409 |
|RemoveProjectRoleConflict |Role `%s` not be added to the Project `%s`. |409 |
|ProjectConfigAlreadyExists |ProjectConfig `%s` already exists. |409 |
