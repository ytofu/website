# KMS Key Policy

Manage KMS Key Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: example

resource:
  aws_kms_key_policy:
    example:
      key_id: ${aws_kms_key.example.id}
      policy: '{ "Id": "example" "Statement": [ { "Action": "kms:*" "Effect": "Allow" "Principal": { "AWS": "*" } "Resource": "*" "Sid": "Enable IAM User Permissions" }, ] "Version": "2012-10-17" }'
```
