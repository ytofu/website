# Redshiftserverless Usage Limit

Manage Redshiftserverless Usage Limit resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshiftserverless_workgroup:
    example:
      namespace_name: ${aws_redshiftserverless_namespace.example.namespace_name}
      workgroup_name: example

resource:
  aws_redshiftserverless_usage_limit:
    example:
      resource_arn: ${aws_redshiftserverless_workgroup.example.arn}
      usage_type: serverless-compute
      amount: 60
```
