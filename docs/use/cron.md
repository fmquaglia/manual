DETA allows you to schedule to program to run periodically. You have to methods of achieving tht:

## Setting
### 1) Rate expression (simple)

Rate based scheduling will execute a program every `interval` according to the `unit`. 
Usage is straight forward, just follow this template:

```ruby
set -cron <interval> <unit>
```

The accepted unit values are **`minutes`**, **`hours`** and **`days`**; or **`minute`**, **`hour`** and **`day`** If the `interval` is `1`.

**Command examples**
```ruby
set -cron 1 day
```

```ruby
set -cron 30 minutes
```

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

## Checking

To check the Schedule setting for a specific program, simply run:

```ruby
ls -cron
```

## Removing
To unschedule running a program, simply run:

```ruby
rm -cron 
```
