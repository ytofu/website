# Securitylake Aws Log Source

Manage Securitylake Aws Log Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securitylake_aws_log_source:
    example:
      source:
        accounts: 
          - 123456789012
        regions: 
          - eu-west-1
        source_name: ROUTE53
      depends_on: 
        - ${aws_securitylake_data_lake.example}
```
