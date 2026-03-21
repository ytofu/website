# MSK Single Scram Secret Association

Manage MSK Single Scram Secret Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_single_scram_secret_association:
    example:
      cluster_arn: ${aws_msk_cluster.example.arn}
      secret_arn: ${aws_secretsmanager_secret.example.arn}
```
