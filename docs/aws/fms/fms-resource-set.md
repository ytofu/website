# FMS Resource Set

Manage FMS Resource Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fms_resource_set:
    example:
      resource_set:
        name: testing
        resource_type_list: 
          - "AWS::NetworkFirewall::Firewall"
```
