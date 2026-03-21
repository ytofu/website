# Sagemaker Flow Definition

Manage Sagemaker Flow Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_flow_definition:
    example:
      flow_definition_name: example
      role_arn: ${aws_iam_role.example.arn}
      human_loop_config:
        human_task_ui_arn: ${aws_sagemaker_human_task_ui.example.arn}
        task_availability_lifetime_in_seconds: 1
        task_count: 1
        task_description: example
        task_title: example
        workteam_arn: ${aws_sagemaker_workteam.example.arn}
      output_config:
        s3_output_path: "s3://${aws_s3_bucket.example.bucket}/"
```

## Public Workteam Usage

```yaml
resource:
  aws_sagemaker_flow_definition:
    example:
      flow_definition_name: example
      role_arn: ${aws_iam_role.example.arn}
      human_loop_config:
        human_task_ui_arn: ${aws_sagemaker_human_task_ui.example.arn}
        task_availability_lifetime_in_seconds: 1
        task_count: 1
        task_description: example
        task_title: example
        workteam_arn: "arn:aws:sagemaker:${data.aws_region.current.region}:394669845002:workteam/public-crowd/default"
        public_workforce_task_price:
          amount_in_usd:
            cents: 1
            tenth_fractions_of_a_cent: 2
      output_config:
        s3_output_path: "s3://${aws_s3_bucket.example.bucket}/"
```

## Human Loop Activation Config Usage

```yaml
resource:
  aws_sagemaker_flow_definition:
    example:
      flow_definition_name: example
      role_arn: ${aws_iam_role.example.arn}
      human_loop_config:
        human_task_ui_arn: ${aws_sagemaker_human_task_ui.example.arn}
        task_availability_lifetime_in_seconds: 1
        task_count: 1
        task_description: example
        task_title: example
        workteam_arn: ${aws_sagemaker_workteam.example.arn}
      human_loop_request_source:
        aws_managed_human_loop_request_source: AWS/Textract/AnalyzeDocument/Forms/V1
      human_loop_activation_config:
        human_loop_activation_conditions_config:
          human_loop_activation_conditions: |
            {
            "Conditions": [
            {
            "ConditionType": "Sampling",
            "ConditionParameters": {
            "RandomSamplingPercentage": 5
            }
            }
            ]
            }
      output_config:
        s3_output_path: "s3://${aws_s3_bucket.example.bucket}/"
```
