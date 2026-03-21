# Shield Drt Access Log Bucket Association

Manage Shield Drt Access Log Bucket Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_shield_drt_access_role_arn_association:
    test:
      role_arn: "arn:aws:iam:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:example-shield_drt_access_role_name"

resource:
  aws_shield_drt_access_log_bucket_association:
    test:
      log_bucket: example-shield_drt_access_log_bucket
      role_arn_association_id: ${aws_shield_drt_access_role_arn_association.test.id}
```
