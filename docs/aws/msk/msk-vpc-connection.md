# MSK VPC Connection

Manage MSK VPC Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_vpc_connection:
    test:
      authentication: SASL_IAM
      target_cluster_arn: aws_msk_cluster.arn
      vpc_id: ${aws_vpc.test.id}
      client_subnets: ${aws_subnet.test[*].id}
      security_groups: 
        - ${aws_security_group.test.id}
```
