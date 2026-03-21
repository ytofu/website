# ECR Replication Configuration

Manage ECR Replication Configuration resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_regions:
    example:

resource:
  aws_ecr_replication_configuration:
    example:
      replication_configuration:
        rule:
          destination:
            region: ${data.aws_regions.example.names[0]}
            registry_id: ${data.aws_caller_identity.current.account_id}
```
