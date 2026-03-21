# Sagemaker Model Card Export Job

Manage Sagemaker Model Card Export Job resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_model_card_export_job:
    example:
      model_card_export_job_name: my-model-card-export-job
      model_card_name: ${aws_sagemaker_model_card.example.model_card_name}
      output_config:
        s3_output_path: "s3://${aws_s3_bucket.test.example}/"
```
