# Savingsplans Savings Plan

Manage Savingsplans Savings Plan resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_savingsplans_savings_plan:
    example:
      savings_plan_offering_id: 00000000-0000-0000-0000-000000000000
      commitment: 1.0
      tags:
        Environment: production
```

## Scheduled Purchase

```yaml
resource:
  aws_savingsplans_savings_plan:
    scheduled:
      savings_plan_offering_id: 00000000-0000-0000-0000-000000000000
      commitment: 5.0
      purchase_time: "2026-12-01T00:00:00Z"
      tags:
        Environment: production
```
