# Ssmcontacts Rotation

Manage Ssmcontacts Rotation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssmcontacts_rotation:
    example:
      contact_ids:
        - ${aws_ssmcontacts_contact.example.arn}
      name: rotation
      recurrence:
        number_of_on_calls: 1
        recurrence_multiplier: 1
        daily_settings:
          hour_of_day: 9
          minute_of_hour: 00
      time_zone_id: Australia/Sydney
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```

## Usage with Weekly Settings and Shift Coverages Fields

```yaml
resource:
  aws_ssmcontacts_rotation:
    example:
      contact_ids:
        - ${aws_ssmcontacts_contact.example.arn}
      name: rotation
      recurrence:
        number_of_on_calls: 1
        recurrence_multiplier: 1
        weekly_settings:
          day_of_week: WED
          hand_off_time:
            hour_of_day: 04
            minute_of_hour: 25
        weekly_settings:
          day_of_week: FRI
          hand_off_time:
            hour_of_day: 15
            minute_of_hour: 57
        shift_coverages:
          map_block_key: MON
          coverage_times:
            start:
              hour_of_day: 01
              minute_of_hour: 00
            end:
              hour_of_day: 23
              minute_of_hour: 00
      start_time: "2023-07-20T02:21:49+00:00"
      time_zone_id: Australia/Sydney
      tags:
        key1: tag1
        key2: tag2
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```

## Usage with Monthly Settings Fields

```yaml
resource:
  aws_ssmcontacts_rotation:
    example:
      contact_ids:
        - ${aws_ssmcontacts_contact.example.arn}
      name: rotation
      recurrence:
        number_of_on_calls: 1
        recurrence_multiplier: 1
        monthly_settings:
          day_of_month: 20
          hand_off_time:
            hour_of_day: 8
            minute_of_hour: 00
        monthly_settings:
          day_of_month: 13
          hand_off_time:
            hour_of_day: 12
            minute_of_hour: 34
      time_zone_id: Australia/Sydney
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```
