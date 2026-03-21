# Quicksight Refresh Schedule

Manage Quicksight Refresh Schedule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_refresh_schedule:
    example:
      data_set_id: dataset-id
      schedule_id: schedule-id
      schedule:
        refresh_type: FULL_REFRESH
        schedule_frequency:
          interval: HOURLY
```

## With Weekly Refresh

```yaml
resource:
  aws_quicksight_refresh_schedule:
    example:
      data_set_id: dataset-id
      schedule_id: schedule-id
      schedule:
        refresh_type: INCREMENTAL_REFRESH
        schedule_frequency:
          interval: WEEKLY
          time_of_the_day: "01:00"
          timezone: Europe/London
          refresh_on_day:
            day_of_week: MONDAY
```

## With Monthly Refresh

```yaml
resource:
  aws_quicksight_refresh_schedule:
    example:
      data_set_id: dataset-id
      schedule_id: schedule-id
      schedule:
        refresh_type: INCREMENTAL_REFRESH
        schedule_frequency:
          interval: MONTHLY
          time_of_the_day: "01:00"
          timezone: Europe/London
          refresh_on_day:
            day_of_month: 1
```
