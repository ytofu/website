# Resource: aws_lambda_function

Manages an AWS Lambda Function. Use this resource to create serverless functions that run code in response to events without provisioning or managing servers.

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

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Unique name for your Lambda Function.
* `role` - (Required) ARN of the function's execution role. The role provides the function's identity and access to AWS services and resources.

The following arguments are optional:

* `architectures` - (Optional) Instruction set architecture for your Lambda function. Valid values are `["x86_64"]` and `["arm64"]`. Default is `["x86_64"]`. Removing this attribute, function's architecture stays the same.
* `capacity_provider_config` - (Optional) Configuration block for Lambda Capacity Provider. [See below](#capacity_provider_config-configuration).
* `code_sha256` - (Optional) Base64-encoded representation the source code package file. Use this argument to trigger updates when the function source code changes. For OCI, this value is relayed directly from the image digest. For zip files, this value is the Base64 encoded SHA-256 hash of the `.zip` file. Layers are not included in the calculation. To trigger updates using a non-standard hashing algorithm, use the `source_code_hash` argument instead.
* `code_signing_config_arn` - (Optional) ARN of a code-signing configuration to enable code signing for this function.
* `dead_letter_config` - (Optional) Configuration block for dead letter queue. [See below](#dead_letter_config-configuration-block).
* `description` - (Optional) Description of what your Lambda Function does.
* `durable_config` - (Optional) Configuration block for durable function settings. [See below](#durable_config-configuration-block). `durable_config` may only be available in [limited regions](https://builder.aws.com/build/capabilities), including `us-east-2`.
* `environment` - (Optional) Configuration block for environment variables. [See below](#environment-configuration-block).
* `ephemeral_storage` - (Optional) Amount of ephemeral storage (`/tmp`) to allocate for the Lambda Function. [See below](#ephemeral_storage-configuration-block).
* `file_system_config` - (Optional) Configuration block for EFS file system. [See below](#file_system_config-configuration-block).
* `filename` - (Optional) Path to the function's deployment package within the local filesystem. Conflicts with `image_uri` and `s3_bucket`. One of `filename`, `image_uri`, or `s3_bucket` must be specified.
* `handler` - (Optional) Function entry point in your code. Required if `package_type` is `Zip`.
* `image_config` - (Optional) Container image configuration values. [See below](#image_config-configuration-block).
* `image_uri` - (Optional) ECR image URI containing the function's deployment package. Conflicts with `filename` and `s3_bucket`. One of `filename`, `image_uri`, or `s3_bucket` must be specified.
* `kms_key_arn` - (Optional) ARN of the AWS Key Management Service key used to encrypt environment variables. If not provided when environment variables are in use, AWS Lambda uses a default service key. If provided when environment variables are not in use, the AWS Lambda API does not save this configuration.
* `layers` - (Optional) List of Lambda Layer Version ARNs (maximum of 5) to attach to your Lambda Function.
* `logging_config` - (Optional) Configuration block for advanced logging settings. [See below](#logging_config-configuration-block).
* `memory_size` - (Optional) Amount of memory in MB your Lambda Function can use at runtime. Valid value between 128 MB to 32,768 MB (32 GB), in 1 MB increments. Defaults to 128.
* `package_type` - (Optional) Lambda deployment package type. Valid values are `Zip` and `Image`. Defaults to `Zip`.
* `publish` - (Optional) Whether to publish creation/change as new Lambda Function Version. Defaults to `false`.
* `publish_to` - (Optional) Whether to publish to a alias or version number. Omit for regular version publishing. Option is `LATEST_PUBLISHED`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `replace_security_groups_on_destroy` - (Optional) Whether to replace the security groups on the function's VPC configuration prior to destruction. Default is `false`.
* `replacement_security_group_ids` - (Optional) List of security group IDs to assign to the function's VPC configuration prior to destruction. Required if `replace_security_groups_on_destroy` is `true`.
* `reserved_concurrent_executions` - (Optional) Amount of reserved concurrent executions for this lambda function. A value of `0` disables lambda from being triggered and `-1` removes any concurrency limitations. Defaults to Unreserved Concurrency Limits `-1`.
* `runtime` - (Optional) Identifier of the function's runtime. Required if `package_type` is `Zip`. See [Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/API_CreateFunction.html#SSS-CreateFunction-request-Runtime) for valid values.
* `s3_bucket` - (Optional) S3 bucket location containing the function's deployment package. Conflicts with `filename` and `image_uri`. One of `filename`, `image_uri`, or `s3_bucket` must be specified.
* `s3_key` - (Optional) S3 key of an object containing the function's deployment package. Required if `s3_bucket` is set.
* `s3_object_version` - (Optional) Object version containing the function's deployment package. Conflicts with `filename` and `image_uri`.
* `skip_destroy` - (Optional) Whether to retain the old version of a previously deployed Lambda Layer. Default is `false`.
* `snap_start` - (Optional) Configuration block for snap start settings. [See below](#snap_start-configuration-block).
* `source_code_hash` - (Optional) User-defined hash of the source code package file. Use this argument to trigger updates when the local function source code changes. This is a synthetic argument tracked only by the AWS provider and does not need to match the hashing algorithm used by Lambda to compute the `CodeSha256` response value. Out-of-band changes to the source code _will not_ be captured by this argument. To include out-of-band source code changes as an update trigger, use the `code_sha256` argument instead.
* `source_kms_key_arn` - (Optional) ARN of the AWS Key Management Service key used to encrypt the function's `.zip` deployment package. Conflicts with `image_uri`.
* `tags` - (Optional) Key-value map of tags for the Lambda function. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `timeout` - (Optional) Amount of time your Lambda Function has to run in seconds. Defaults to 3. Valid between 1 and 900.
* `tenancy_config` - (Optional) Configuration block for Tenancy. [See below](#tenancy_config-configuration-block).
* `tracing_config` - (Optional) Configuration block for X-Ray tracing. [See below](#tracing_config-configuration-block).
* `vpc_config` - (Optional) Configuration block for VPC. [See below](#vpc_config-configuration-block).

### capacity_provider_config Configuration

* `lambda_managed_instances_capacity_provider_config` - (Required) Configuration block for Lambda Managed Instances Capacity Provider. [See below](#lambda_managed_instances_capacity_provider_config-configuration-block).

### lambda_managed_instances_capacity_provider_config Configuration Block

* `capacity_provider_arn` - (Required) ARN of the Capacity Provider.
* `execution_environment_memory_gib_per_vcpu` - (Optional) Memory GiB per vCPU for the execution environment.
* `per_execution_environment_max_concurrency` - (Optional) Maximum concurrency per execution environment.

### dead_letter_config Configuration Block

* `target_arn` - (Required) ARN of an SNS topic or SQS queue to notify when an invocation fails.

### durable_config Configuration Block

`durable_config` may only be available in [limited regions](https://builder.aws.com/build/capabilities), including `us-east-2`.

* `execution_timeout` - (Required) Maximum execution time in seconds for the durable function. Valid value between 1 and 31622400 (366 days).
* `retention_period` - (Optional) Number of days to retain the function's execution state. Valid value between 1 and 90. If not specified, the function's execution state is not retained. Defaults to 14.

### environment Configuration Block

* `variables` - (Optional) Map of environment variables available to your Lambda function during execution.

### ephemeral_storage Configuration Block

* `size` - (Required) Amount of ephemeral storage (`/tmp`) in MB. Valid between 512 MB and 10,240 MB (10 GB).

### file_system_config Configuration Block

* `arn` - (Required) ARN of the Amazon EFS Access Point.
* `local_mount_path` - (Required) Path where the function can access the file system. Must start with `/mnt/`.

### image_config Configuration Block

* `command` - (Optional) Parameters to pass to the container image.
* `entry_point` - (Optional) Entry point to your application.
* `working_directory` - (Optional) Working directory for the container image.

### logging_config Configuration Block

* `application_log_level` - (Optional) Detail level of application logs. Valid values: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`.
* `log_format` - (Required) Log format. Valid values: `Text`, `JSON`.
* `log_group` - (Optional) CloudWatch log group where logs are sent.
* `system_log_level` - (Optional) Detail level of Lambda platform logs. Valid values: `DEBUG`, `INFO`, `WARN`.

### snap_start Configuration Block

* `apply_on` - (Required) When to apply snap start optimization. Valid value: `PublishedVersions`.

### tenancy_config Configuration Block

* `tenant_isolation_mode` - (Required) Tenant Isolation Mode. Valid values: `PER_TENANT`.

### tracing_config Configuration Block

* `mode` - (Required) X-Ray tracing mode. Valid values: `Active`, `PassThrough`.

### vpc_config Configuration Block

* `ipv6_allowed_for_dual_stack` - (Optional) Whether to allow outbound IPv6 traffic on VPC functions connected to dual-stack subnets. Default: `false`.
* `security_group_ids` - (Required) List of security group IDs associated with the Lambda function.
* `subnet_ids` - (Required) List of subnet IDs associated with the Lambda function.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN identifying your Lambda Function.
* `invoke_arn` - ARN to be used for invoking Lambda Function from API Gateway - to be used in `aws_api_gateway_integration`'s `uri`.
* `last_modified` - Date this resource was last modified.
* `qualified_arn` - ARN identifying your Lambda Function Version (if versioning is enabled via `publish = true`).
* `qualified_invoke_arn` - Qualified ARN (ARN with lambda version number) to be used for invoking Lambda Function from API Gateway - to be used in `aws_api_gateway_integration`'s `uri`.
* `signing_job_arn` - ARN of the signing job.
* `signing_profile_version_arn` - ARN of the signing profile version.
* `snap_start.optimization_status` - Optimization status of the snap start configuration. Valid values are `On` and `Off`.
* `source_code_size` - Size in bytes of the function .zip file.
* `response_streaming_invoke_arn` - ARN to be used for invoking Lambda Function from API Gateway with response streaming - to be used in `aws_api_gateway_integration`'s `uri`.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `version` - Latest published version of your Lambda Function.
* `vpc_config.vpc_id` - ID of the VPC.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_lambda_function.example example
```
