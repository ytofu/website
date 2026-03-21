# Synthetics Canary

Manage Synthetics Canary resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_synthetics_canary:
    some:
      name: some-canary
      artifact_s3_location: "s3://some-bucket/"
      execution_role_arn: some-role
      handler: exports.handler
      zip_file: test-fixtures/lambdatest.zip
      runtime_version: syn-1.0
      schedule:
        expression: rate(0 minute)
```
