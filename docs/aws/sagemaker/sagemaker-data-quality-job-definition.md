# Sagemaker Data Quality Job Definition

Manage Sagemaker Data Quality Job Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_data_quality_job_definition:
    test:
      name: my-data-quality-job-definition
      data_quality_app_specification:
        image_uri: ${data.aws_sagemaker_prebuilt_ecr_image.monitor.registry_path}
      data_quality_job_input:
        endpoint_input:
          endpoint_name: ${aws_sagemaker_endpoint.my_endpoint.name}
      data_quality_job_output_config:
        monitoring_outputs:
          s3_output:
            s3_uri: "https://${aws_s3_bucket.my_bucket.bucket_regional_domain_name}/output"
      job_resources:
        cluster_config:
          instance_count: 1
          instance_type: ml.t3.medium
          volume_size_in_gb: 20
      role_arn: ${aws_iam_role.my_role.arn}
```
