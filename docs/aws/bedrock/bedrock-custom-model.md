# Bedrock Custom Model

Manage Bedrock Custom Model resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_bedrock_foundation_model:
    example:
      model_id: amazon.titan-text-express-v1

resource:
  aws_bedrock_custom_model:
    example:
      custom_model_name: example-model
      job_name: example-job-1
      base_model_identifier: ${data.aws_bedrock_foundation_model.example.model_arn}
      role_arn: ${aws_iam_role.example.arn}
      hyperparameters: 
      output_data_config:
        s3_uri: "s3://${aws_s3_bucket.output.id}/data/"
      training_data_config:
        s3_uri: "s3://${aws_s3_bucket.training.id}/data/train.jsonl"
```
