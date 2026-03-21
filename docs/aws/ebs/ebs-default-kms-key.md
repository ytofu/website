# EBS Default KMS Key

Manage EBS Default KMS Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ebs_default_kms_key:
    example:
      key_arn: ${aws_kms_key.example.arn}
```
