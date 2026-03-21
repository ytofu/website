# Batch Scheduling Policy

Manage Batch Scheduling Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_batch_scheduling_policy:
    example:
      name: example
      fair_share_policy:
        compute_reservation: 1
        share_decay_seconds: 3600
        share_distribution:
          share_identifier: "A1*"
          weight_factor: 0.1
        share_distribution:
          share_identifier: A2
          weight_factor: 0.2
      tags: 
```
