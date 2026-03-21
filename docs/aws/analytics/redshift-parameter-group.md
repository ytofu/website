# Redshift Parameter Group

Manage Redshift Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_parameter_group:
    bar:
      name: parameter-group-test-terraform
      family: redshift-1.0
      parameter:
        name: require_ssl
        value: true
      parameter:
        name: query_group
        value: example
      parameter:
        name: enable_user_activity_logging
        value: true
```
