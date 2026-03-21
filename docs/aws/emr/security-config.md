# EMR Security Configuration

Configure security settings for EMR clusters using ytofu YAML.

## With Encryption

```yaml
resource:
  aws_emr_security_configuration:
    example:
      name: example
      configuration: |
        {
          "EncryptionConfiguration": {
            "AtRestEncryptionConfiguration": {
              "S3EncryptionConfiguration": {
                "EncryptionMode": "SSE-S3"
              },
              "LocalDiskEncryptionConfiguration": {
                "EncryptionKeyProviderType": "AwsKms",
                "AwsKmsKey": "${aws_kms_key.example.arn}"
              }
            },
            "EnableInTransitEncryption": false,
            "EnableAtRestEncryption": true
          }
        }
```
