DETA allows you to schedule programs to run periodically, providing two ways of doing so: `rate` epressions and `cron` expressions.

*To change the schedule settings of a program, the program needs to be open (`open myprog`) in the [(Studio)](https://web.deta.sh/studio), and you need to have a ['full' access permission](/permissions/).*



## Setting a Schedule
### 1) Rate expression (simple)

Rate based scheduling will execute a program every `interval` according to the `unit`. 

To set a program on a rate based execution schedule, follow this template:

```ruby
set -cron <interval> <unit>
```

*The accepted unit values are **`minutes`**, **`hours`** and **`days`**. If the `interval` is `1`, use **`minute`**, **`hour`** or **`day`**.*

<br />

**Command examples**
```ruby
set -cron 1 day
```

```ruby
set -cron 30 minutes
```

<br />

### 2) Cron expression (advanced)
```ruby
set -cron <minute> <hour> <month_day> <week_day> <year>
```
!!! Important
    **[Click here to learn more about what cron values to use and what they mean.](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html#CronExpressions)**

**Command examples**

* **`#!rb set -cron 0 10 * * ? *`**: Run at 10:00 am (UTC) every day
* **`#!rb set -cron 15 12 * * ? *`**: Run at 12:15 pm (UTC) every day
* **`#!rb set -cron 0 18 ? * MON-FRI *`**: Run at 6:00 pm (UTC) every Monday through Friday
* **`#!rb set -cron 0 8 1 * ? * `**: Run at 8:00 am (UTC) every 1st day of the month
* **`#!rb set -cron 0/15 * * * ? *`**: Run every 15 minutes
* **`#!rb set -cron 0/10 * ? * MON-FRI *`**: Run every 10 minutes Monday through Friday
* **`#!rb set -cron 0/5 8-17 ? * MON-FRI *`**: Run every 5 minutes Monday through Friday between 8:00 am and 5:55 pm (UTC)

## Checking a Schedule

To check if a program is set to run on a schedule, simply run:

```ruby
ls -cron
```

## Removing a Schedule
To stop a program from executing on a schedule, simply run:

```ruby
rm -cron 
```
