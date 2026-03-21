# MSK Serverless Cluster

Manage MSK Serverless Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_serverless_cluster:
    example:
      cluster_name: Example
      vpc_config:
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      client_authentication:
        sasl:
          iam:
            enabled: true
```
