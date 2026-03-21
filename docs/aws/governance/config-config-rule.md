# Config Config Rule

Manage Config Config Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_config_config_rule:
    r:
      name: example
      source:
        owner: AWS
        source_identifier: S3_BUCKET_VERSIONING_ENABLED
      depends_on: 
        - ${aws_config_configuration_recorder.foo}

resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - config.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    r:
      name: my-awsconfig-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    p:
      statement:
        effect: Allow
        actions: 
          - "config:Put*"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    p:
      name: my-awsconfig-policy
      role: ${aws_iam_role.r.id}
      policy: ${data.aws_iam_policy_document.p.json}
```

## Custom Rules

```yaml
resource:
  aws_config_configuration_recorder:
    example:

resource:
  aws_lambda_function:
    example:

resource:
  aws_lambda_permission:
    example:
      action: "lambda:InvokeFunction"
      function_name: ${aws_lambda_function.example.arn}
      principal: config.amazonaws.com
      statement_id: AllowExecutionFromConfig

resource:
  aws_config_config_rule:
    example:
      source:
        owner: CUSTOM_LAMBDA
        source_identifier: ${aws_lambda_function.example.arn}
      depends_on:
        - ${aws_config_configuration_recorder.example}
        - ${aws_lambda_permission.example}
```

## Custom Policies

```yaml
resource:
  aws_config_config_rule:
    example:
      name: example
      source:
        owner: CUSTOM_POLICY
        source_detail:
          message_type: ConfigurationItemChangeNotification
        custom_policy_details:
          policy_runtime: guard-2.x.x
          policy_text: |
            rule tableisactive when
            resourceType == "AWS::DynamoDB::Table" {
            configuration.tableStatus == ['ACTIVE']
            }
            
            rule checkcompliance when
            resourceType == "AWS::DynamoDB::Table"
            tableisactive {
            supplementaryConfiguration.ContinuousBackupsDescription.pointInTimeRecoveryDescription.pointInTimeRecoveryStatus == "ENABLED"
            }
```
