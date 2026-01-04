# Lambda Function

Deploy serverless functions with AWS Lambda using ytofu YAML.

## Basic Function with Node.js

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        - effect: Allow
          principals:
            - type: Service
              identifiers:
                - lambda.amazonaws.com
          actions:
            - sts:AssumeRole

  archive_file:
    example:
      type: zip
      source_file: ${path.module}/lambda/index.js
      output_path: ${path.module}/lambda/function.zip

resource:
  aws_iam_role:
    example:
      name: lambda_execution_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_lambda_function:
    example:
      filename: ${data.archive_file.example.output_path}
      function_name: example_lambda_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      code_sha256: ${data.archive_file.example.output_base64sha256}
      runtime: nodejs20.x
      environment:
        variables:
          ENVIRONMENT: production
          LOG_LEVEL: info
      tags:
        Environment: production
        Application: example
```

## Container Image Function

```yaml
resource:
  aws_lambda_function:
    example:
      function_name: example_container_function
      role: ${aws_iam_role.example.arn}
      package_type: Image
      image_uri: ${aws_ecr_repository.example.repository_url}:latest
      image_config:
        entry_point:
          - /lambda-entrypoint.sh
        command:
          - app.handler
      memory_size: 512
      timeout: 30
      architectures:
        - arm64
```

## Function with Lambda Layers

```yaml
resource:
  aws_lambda_layer_version:
    example:
      filename: layer.zip
      layer_name: example_dependencies_layer
      description: Common dependencies for Lambda functions
      compatible_runtimes:
        - nodejs20.x
        - python3.12
      compatible_architectures:
        - x86_64
        - arm64

  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_layered_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      layers:
        - ${aws_lambda_layer_version.example.arn}
      tracing_config:
        mode: Active
```

## VPC Function with Enhanced Networking

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_vpc_function
      role: ${aws_iam_role.example.arn}
      handler: app.handler
      runtime: python3.12
      memory_size: 1024
      timeout: 30
      vpc_config:
        subnet_ids:
          - ${aws_subnet.example_private1.id}
          - ${aws_subnet.example_private2.id}
        security_group_ids:
          - ${aws_security_group.example_lambda.id}
        ipv6_allowed_for_dual_stack: true
      ephemeral_storage:
        size: 5120
      snap_start:
        apply_on: PublishedVersions
```

## Function with EFS Integration

```yaml
resource:
  aws_efs_file_system:
    example:
      encrypted: true
      tags:
        Name: lambda-efs

  aws_efs_access_point:
    example:
      file_system_id: ${aws_efs_file_system.example.id}
      root_directory:
        path: /lambda
        creation_info:
          owner_gid: 1000
          owner_uid: 1000
          permissions: "755"
      posix_user:
        gid: 1000
        uid: 1000

  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_efs_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      vpc_config:
        subnet_ids:
          - ${aws_subnet.private_a.id}
          - ${aws_subnet.private_b.id}
        security_group_ids:
          - ${aws_security_group.lambda.id}
      file_system_config:
        arn: ${aws_efs_access_point.example.arn}
        local_mount_path: /mnt/data
      depends_on:
        - aws_efs_mount_target.example
```

## Function with Advanced Logging

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: /aws/lambda/example_function
      retention_in_days: 14
      tags:
        Environment: production
        Application: example

  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      logging_config:
        log_format: JSON
        application_log_level: INFO
        system_log_level: WARN
      depends_on:
        - aws_cloudwatch_log_group.example
```

## Function with Error Handling

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      dead_letter_config:
        target_arn: ${aws_sqs_queue.dlq.arn}

  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      maximum_event_age_in_seconds: 60
      maximum_retry_attempts: 2
      destination_config:
        on_failure:
          destination: ${aws_sqs_queue.dlq.arn}
        on_success:
          destination: ${aws_sns_topic.success.arn}
```

## CloudWatch Logging with Permissions

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: /aws/lambda/example_function
      retention_in_days: 14
      tags:
        Environment: production
        Function: example_function

  aws_iam_role:
    example:
      name: lambda_execution_role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Effect": "Allow",
            "Principal": {"Service": "lambda.amazonaws.com"}
          }]
        }

  aws_iam_policy:
    lambda_logging:
      name: lambda_logging
      path: /
      description: IAM policy for logging from Lambda
      policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Effect": "Allow",
            "Action": [
              "logs:CreateLogGroup",
              "logs:CreateLogStream",
              "logs:PutLogEvents"
            ],
            "Resource": ["arn:aws:logs:*:*:*"]
          }]
        }

  aws_iam_role_policy_attachment:
    lambda_logs:
      role: ${aws_iam_role.example.name}
      policy_arn: ${aws_iam_policy.lambda_logging.arn}

  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      logging_config:
        log_format: JSON
        application_log_level: INFO
        system_log_level: WARN
      depends_on:
        - aws_iam_role_policy_attachment.lambda_logs
        - aws_cloudwatch_log_group.example
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| function_name | string | Yes | Function name |
| role | string | Yes | IAM role ARN |
| runtime | string | Yes* | Runtime (e.g., nodejs20.x, python3.12) |
| handler | string | Yes* | Handler function (e.g., index.handler) |
| filename | string | No | Path to deployment package |
| s3_bucket | string | No | S3 bucket containing code |
| s3_key | string | No | S3 object key for code |
| package_type | string | No | Zip or Image |
| image_uri | string | No | ECR image URI for container |
| memory_size | number | No | Memory in MB (128-10240) |
| timeout | number | No | Timeout in seconds (1-900) |
| environment | object | No | Environment variables |
| vpc_config | object | No | VPC configuration |
| layers | list | No | Lambda layer ARNs |
| architectures | list | No | x86_64 or arm64 |
| ephemeral_storage | object | No | /tmp storage size |
| logging_config | object | No | CloudWatch logging config |
| tracing_config | object | No | X-Ray tracing config |
| snap_start | object | No | SnapStart configuration |
| tags | map | No | Resource tags |

*Not required for container images

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| arn | Function ARN |
| invoke_arn | ARN for invoking the function |
| qualified_arn | ARN with version |
| version | Latest published version |

## Best Practices

- **Right-size memory** - More memory = more CPU, find the optimal balance
- **Set appropriate timeouts** - Avoid paying for idle time
- **Use environment variables** for configuration
- **Enable X-Ray tracing** for debugging
- **Use Lambda Layers** for shared dependencies
- **Use JSON log format** for better CloudWatch insights
- **Use SnapStart** for Java functions to reduce cold starts
- **Use arm64 architecture** for better price/performance

## Related Resources

- [VPC](../networking/vpc.md)
- [Security Groups](../networking/security-groups.md)
- [ECS](ecs.md)
