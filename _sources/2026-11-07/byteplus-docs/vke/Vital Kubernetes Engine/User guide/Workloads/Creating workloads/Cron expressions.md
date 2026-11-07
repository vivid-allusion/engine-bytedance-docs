---
title: "Cron expressions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cron-expressions"
---

In Vital Kubernetes Engine (VKE), CronJobs use Cron expressions to specify the trigger time for Jobs. This topic describes the usage of Cron expressions adapted for VKE.

<span id=".Y3Jvbi3ml7bpl7Tooajor63ms5U="></span>
## Cron schedule expressions

CronJobs use Cron expressions to specify the exact execution time for Jobs. The Cron expressions consist of five fields, including minutes, hours, days of the month, months, and days of the week.

```Plain Text
# ┌───────────── Minute (0 - 59)
# │ ┌───────────── Hour (0 - 23)
# │ │ ┌───────────── Date (1 - 31)
# │ │ │ ┌───────────── Month (1 - 12)
# │ │ │ │ ┌───────────── Week (0 - 6) （From Sunday to Monday; In some systems, 7 represents Sunday.）
# │ │ │ │ │
# │ │ │ │ │
# │ │ │ │ │
# * * * * * 
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you need to set the trigger time to a specific <strong>day of the month</strong>, we recommend that you do not set a <strong>day of the week</strong> to ensure that the Jobs are triggered within the specified time. When you set both the day of the month and the week, the Jobs will be triggered if either condition is met.</div>


<span id=".Y3Jvbi3ooajovr7lvI8="></span>
## Cron expressions

You can enter multiple values in a field by using a Cron expression to meet different Job execution requirements.


* Comma ( **`,`** ): Indicates enumeration. For example, **`1,3,4,7 * * * *`**  indicates that the Job is executed at the 1st, 3rd, 4th, and 7th minute of every hour.

* Hyphen ( **`-`** ): Indicates a range. For example, **`1-6 * * * *`**  indicates that the Job will be executed every minute from the 1st to the 6th minute of each hour.

* Asterisk ( **`*`** ): Indicates any possible value. For example, an asterisk (\*) in the hour field indicates every hour.

* Slash ( **`/`** ): indicates how often the Job is executed. For example,  **`*/2 * * * *`**  indicates that the Job is executed at every time point divisible by 2, which is 0, 2, ..., 56, and 58.


<span id=".56S65L6L"></span>
## Example


|Expression |Description |
|---|---|
|`*/20 1-6 * * 0,1,3` |The Job is executed at the 0th, 20th, and 40th minutes of every hour between 01:00 and 06:59 every Sunday, Monday, and Wednesday. |
|`59 1 1-7 4 0` |The job runs daily at 1:59 from April 1 to 7, and at 1:59 on every remaining Sunday in April. |
