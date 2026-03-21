# Redshiftserverless Resource Policy

Manage Redshiftserverless Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshiftserverless_resource_policy:
    example:
      resource_arn: ${aws_redshiftserverless_snapshot.example.arn}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Principal": { "AWS": ["12345678901"] } "Action": [ "redshift-serverless:RestoreFromSnapshot", ] "Sid": "" }] }'
```
