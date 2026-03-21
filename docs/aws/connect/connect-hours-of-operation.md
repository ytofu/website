# Connect Hours Of Operation

Manage Connect Hours Of Operation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_hours_of_operation:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Office Hours
      description: Monday office hours
      time_zone: EST
      config:
        day: MONDAY
        end_time:
          hours: 23
          minutes: 8
        start_time:
          hours: 8
          minutes: 0
      config:
        day: TUESDAY
        end_time:
          hours: 21
          minutes: 0
        start_time:
          hours: 9
          minutes: 0
      tags: 
```
