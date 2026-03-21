# Redshift Resource Policy

Manage Redshift Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_resource_policy:
    example:
      resource_arn: ${aws_redshift_cluster.example.cluster_namespace_arn}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::12345678901:root" } "Action": "redshift:CreateInboundIntegration" "Resource": aws_redshift_cluster.example.cluster_namespace_arn "Sid": "" }] }'
```
