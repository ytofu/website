# Bedrock Custom Model

Create custom model training jobs using ytofu YAML.

## Fine-Tuned Model

```yaml
resource:
  aws_bedrock_custom_model:
    example:
      custom_model_name: my-custom-model
      job_name: my-fine-tuning-job
      base_model_identifier: amazon.titan-text-express-v1
      role_arn: ${aws_iam_role.bedrock.arn}
      hyperparameters:
        epochCount: "1"
        batchSize: "1"
        learningRate: "0.00001"
      training_data_config:
        s3_uri: s3://${aws_s3_bucket.training.id}/train.jsonl
      output_data_config:
        s3_uri: s3://${aws_s3_bucket.output.id}/output/
```
