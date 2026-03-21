# Apprunner VPC Connector

Manage Apprunner VPC Connector resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_vpc_connector:
    connector:
      vpc_connector_name: name
      subnets: 
        - subnet1
        - subnet2
      security_groups: 
        - sg1
        - sg2
```
