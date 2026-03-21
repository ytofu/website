# MSK Serverless Cluster

Create serverless Kafka clusters using ytofu YAML.

## Basic Serverless Cluster

```yaml
resource:
  aws_msk_serverless_cluster:
    example:
      cluster_name: example
      vpc_config:
        - subnet_ids:
            - ${aws_subnet.a.id}
            - ${aws_subnet.b.id}
            - ${aws_subnet.c.id}
          security_group_ids:
            - ${aws_security_group.msk.id}
      client_authentication:
        sasl:
          iam:
            enabled: true
```
