# Lambda Function

Manage Lambda Function resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - lambda.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: lambda_execution_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  archive_file:
    example:
      type: zip
      source_file: "${path.module}/lambda/index.js"
      output_path: "${path.module}/lambda/function.zip"

resource:
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
      image_uri: "${aws_ecr_repository.example.repository_url}:latest"
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

resource:
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
        mode: "Active" # Enable X-Ray tracing
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

resource:
  aws_efs_mount_target:
    example:
      file_system_id: ${aws_efs_file_system.example.id}
      subnet_id: example-value
      security_groups: 
        - ${aws_security_group.efs.id}

resource:
  aws_efs_access_point:
    example:
      file_system_id: ${aws_efs_file_system.example.id}
      root_directory:
        path: /lambda
        creation_info:
          owner_gid: 1000
          owner_uid: 1000
          permissions: 755
      posix_user:
        gid: 1000
        uid: 1000

resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_efs_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      vpc_config:
        subnet_ids: example-subnet_ids
        security_group_ids: 
          - ${aws_security_group.lambda.id}
      file_system_config:
        arn: ${aws_efs_access_point.example.arn}
        local_mount_path: /mnt/data
      depends_on: 
        - ${aws_efs_mount_target.example}
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

resource:
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
        - ${aws_cloudwatch_log_group.example}
```

## Function with logging to S3 or Data Firehose

```yaml
resource:
  aws_s3_bucket:
    lambda_log_export:
      bucket: "example-lambda_function_name-bucket"

resource:
  aws_cloudwatch_log_group:
    export:
      name: "/aws/lambda/example-lambda_function_name"
      log_group_class: DELIVERY

data:
  aws_iam_policy_document:
    logs_assume_role:
      statement:
        actions: 
          - "sts:AssumeRole"
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - logs.amazonaws.com

resource:
  aws_iam_role:
    logs_log_export:
      name: "example-lambda_function_name-lambda-log-export-role"
      assume_role_policy: ${data.aws_iam_policy_document.logs_assume_role.json}

data:
  aws_iam_policy_document:
    lambda_log_export:
      statement:
        actions:
          - "s3:PutObject"
        effect: Allow
        resources:
          - "${aws_s3_bucket.lambda_log_export.arn}/*"

resource:
  aws_iam_role_policy:
    lambda_log_export:
      policy: ${data.aws_iam_policy_document.lambda_log_export.json}
      role: ${aws_iam_role.logs_log_export.name}

resource:
  aws_cloudwatch_log_subscription_filter:
    lambda_log_export:
      name: "example-lambda_function_name-filter"
      log_group_name: ${aws_cloudwatch_log_group.export.name}
      filter_pattern: 
      destination_arn: ${aws_s3_bucket.lambda_log_export.arn}
      role_arn: ${aws_iam_role.logs_log_export.arn}

resource:
  aws_lambda_function:
    log_export:
      function_name: example-lambda_function_name
      handler: index.lambda_handler
      runtime: python3.13
      role: ${aws_iam_role.example.arn}
      filename: function.zip
      logging_config:
        log_format: Text
        log_group: ${aws_cloudwatch_log_group.export.name}
      depends_on:
        - ${aws_cloudwatch_log_group.export}
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

resource:
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

## CloudWatch Logging and Permissions

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: "/aws/lambda/example-function_name"
      retention_in_days: 14
      tags:
        Environment: production
        Function: example-function_name

resource:
  aws_iam_role:
    example:
      name: lambda_execution_role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "lambda.amazonaws.com" } } ] }'

resource:
  aws_iam_policy:
    lambda_logging:
      name: lambda_logging
      path: /
      description: IAM policy for logging from Lambda
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "logs:CreateLogGroup", "logs:CreateLogStream", "logs:PutLogEvents" ] "Resource": ["arn:aws:logs:*:*:*"] } ] }'

resource:
  aws_iam_role_policy_attachment:
    lambda_logs:
      role: ${aws_iam_role.example.name}
      policy_arn: ${aws_iam_policy.lambda_logging.arn}

resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example-function_name
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      logging_config:
        log_format: JSON
        application_log_level: INFO
        system_log_level: WARN
      depends_on:
        - ${aws_iam_role_policy_attachment.lambda_logs}
        - ${aws_cloudwatch_log_group.example}
```

## Function with Durable Configuration

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example_durable_function
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs22.x
      memory_size: 512
      timeout: 30
      durable_config:
        execution_timeout: 3600
        retention_period: 7
      environment:
        variables:
          DURABLE_MODE: enabled
      timeouts:
        delete: 60m
      tags:
        Environment: production
        Type: durable
```

## Capacity Provider Configuration

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: example
      role: ${aws_iam_role.example.arn}
      handler: index.handler
      runtime: nodejs20.x
      memory_size: 2048
      publish: true
      capacity_provider_config:
        lambda_managed_instances_capacity_provider_config:
          capacity_provider_arn: ${aws_lambda_capacity_provider.example.arn}

resource:
  aws_lambda_capacity_provider:
    example:
      name: example
      vpc_config:
        subnet_ids: 
          - ${aws_subnet.example.id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      permissions_config:
        capacity_provider_operator_role_arn: ${aws_iam_role.example.arn}
```
