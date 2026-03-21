# Sagemaker Labeling Job

Manage Sagemaker Labeling Job resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_labeling_job:
    test:
      label_attribute_name: label1
      labeling_job_name: my-labeling-job
      role_arn: ${aws_iam_role.example.arn}
      label_category_config_s3_uri: "s3://${aws_s3_bucket.example.bucket}/${aws_s3_object.example.key}"
      human_task_config:
        number_of_human_workers_per_data_object: 1
        task_description: Apply the labels provided to specific words or phrases within the larger text block.
        task_title: Named entity Recognition task
        task_time_limit_in_seconds: 28800
        workteam_arn: ${aws_sagemaker_workteam.example.arn}
        ui_config:
          human_task_ui_arn: "arn:aws:sagemaker:us-west-2:394669845002:human-task-ui/NamedEntityRecognition"
        pre_human_task_lambda_arn: "arn:aws:lambda:us-west-2:081040173940:function:PRE-NamedEntityRecognition"
        annotation_consolidation_config:
          annotation_consolidation_lambda_arn: "arn:aws:lambda:us-west-2:081040173940:function:ACS-NamedEntityRecognition"
      input_config:
        data_source:
          sns_data_source:
            sns_topic_arn: ${aws_sns_topic.example.arn}
      output_config:
        s3_output_path: "s3://${aws_s3_bucket.example.bucket}/"
```
