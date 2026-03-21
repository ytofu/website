# Resiliencehub Resiliency Policy

Manage Resiliencehub Resiliency Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_resiliencehub_resiliency_policy:
    example:
      name: testexample
      description: testexample
      tier: NonCritical
      data_location_constraint: AnyLocation
      policy:
        region:
          rpo: 24h
          rto: 24h
        az:
          rpo: 24h
          rto: 24h
        hardware:
          rpo: 24h
          rto: 24h
        software:
          rpo: 24h
          rto: 24h
```
