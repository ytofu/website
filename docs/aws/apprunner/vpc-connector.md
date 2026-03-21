# App Runner VPC Connector

Create VPC connectors for App Runner services using ytofu YAML.

## Basic Connector

```yaml
resource:
  aws_apprunner_vpc_connector:
    connector:
      vpc_connector_name: example
      subnets:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      security_groups:
        - ${aws_security_group.example.id}
```
