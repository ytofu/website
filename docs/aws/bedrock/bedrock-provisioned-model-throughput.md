# Bedrock Provisioned Model Throughput

Manage Bedrock Provisioned Model Throughput resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrock_provisioned_model_throughput:
    example:
      provisioned_model_name: example-model
      model_arn: "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-v2"
      commitment_duration: SixMonths
      model_units: 1
```
