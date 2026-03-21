# Cloudwatch Event Target

Manage Cloudwatch Event Target resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_target:
    yada:
      target_id: Yada
      rule: ${aws_cloudwatch_event_rule.console.name}
      arn: ${aws_kinesis_stream.test_stream.arn}
      run_command_targets:
        key: "tag:Name"
        values: 
          - FooBar
      run_command_targets:
        key: InstanceIds
        values: 
          - i-162058cd308bffec2

resource:
  aws_cloudwatch_event_rule:
    console:
      name: capture-ec2-scaling-events
      description: Capture all EC2 scaling events
      event_pattern: '{ "source": [ "aws.autoscaling" ] detail-"type": [ "EC2 Instance Launch Successful", "EC2 Instance Terminate Successful", "EC2 Instance Launch Unsuccessful", "EC2 Instance Terminate Unsuccessful" ] }'

resource:
  aws_kinesis_stream:
    test_stream:
      name: terraform-kinesis-test
      shard_count: 1
```

## SSM Document Usage

```yaml
data:
  aws_iam_policy_document:
    ssm_lifecycle_trust:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - events.amazonaws.com

data:
  aws_iam_policy_document:
    ssm_lifecycle:
      statement:
        effect: Allow
        actions: 
          - "ssm:SendCommand"
        resources: 
          - "arn:aws:ec2:eu-west-1:1234567890:instance/*"
        condition:
          test: StringEquals
          values: 
            - "*"
      statement:
        effect: Allow
        actions: 
          - "ssm:SendCommand"
        resources: 
          - ${aws_ssm_document.stop_instance.arn}

resource:
  aws_iam_role:
    ssm_lifecycle:
      name: SSMLifecycle
      assume_role_policy: ${data.aws_iam_policy_document.ssm_lifecycle_trust.json}

resource:
  aws_iam_policy:
    ssm_lifecycle:
      name: SSMLifecycle
      policy: ${data.aws_iam_policy_document.ssm_lifecycle.json}

resource:
  aws_iam_role_policy_attachment:
    ssm_lifecycle:
      policy_arn: ${aws_iam_policy.ssm_lifecycle.arn}
      role: ${aws_iam_role.ssm_lifecycle.name}

resource:
  aws_ssm_document:
    stop_instance:
      name: stop_instance
      document_type: Command
      content: '{ "schemaVersion": "1.2" "description": "Stop an instance" "parameters": {} "runtimeConfig": { "aws:runShellScript" = { "properties": [ { "id": "0.aws:runShellScript" "runCommand": ["halt"] } ] } } }'

resource:
  aws_cloudwatch_event_rule:
    stop_instances:
      name: StopInstance
      description: Stop instances nightly
      schedule_expression: "cron(0 0 * * ? *)"

resource:
  aws_cloudwatch_event_target:
    stop_instances:
      target_id: StopInstance
      arn: ${aws_ssm_document.stop_instance.arn}
      rule: ${aws_cloudwatch_event_rule.stop_instances.name}
      role_arn: ${aws_iam_role.ssm_lifecycle.arn}
      run_command_targets:
        key: "tag:Terminate"
        values: 
          - midnight
```

## RunCommand Usage

```yaml
resource:
  aws_cloudwatch_event_rule:
    stop_instances:
      name: StopInstance
      description: Stop instances nightly
      schedule_expression: "cron(0 0 * * ? *)"

resource:
  aws_cloudwatch_event_target:
    stop_instances:
      target_id: StopInstance
      arn: "arn:aws:ssm:example-aws_region::document/AWS-RunShellScript"
      input: "{\"commands\":[\"halt\"]}"
      rule: ${aws_cloudwatch_event_rule.stop_instances.name}
      role_arn: ${aws_iam_role.ssm_lifecycle.arn}
      run_command_targets:
        key: "tag:Terminate"
        values: 
          - midnight
```

## ECS Run Task with Role and Task Override Usage

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - events.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    ecs_events:
      name: ecs_events
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    ecs_events_run_task_with_any_role:
      statement:
        effect: Allow
        actions: 
          - "iam:PassRole"
        resources: 
          - "*"
      statement:
        effect: Allow
        actions: 
          - "ecs:RunTask"
        resources: 
          - replaced-value

resource:
  aws_iam_role_policy:
    ecs_events_run_task_with_any_role:
      name: ecs_events_run_task_with_any_role
      role: ${aws_iam_role.ecs_events.id}
      policy: ${data.aws_iam_policy_document.ecs_events_run_task_with_any_role.json}

resource:
  aws_cloudwatch_event_target:
    ecs_scheduled_task:
      target_id: run-scheduled-task-every-hour
      arn: ${aws_ecs_cluster.cluster_name.arn}
      rule: ${aws_cloudwatch_event_rule.every_hour.name}
      role_arn: ${aws_iam_role.ecs_events.arn}
      ecs_target:
        task_count: 1
        task_definition_arn: ${aws_ecs_task_definition.task_name.arn}
      input: '{ "containerOverrides": [ { "name": "name-of-container-to-override", "command": [ "bin/console", "scheduled-task" ] } ] }'
```

## API Gateway target

```yaml
resource:
  aws_cloudwatch_event_target:
    example:
      arn: "${aws_api_gateway_stage.example.execution_arn}/GET"
      rule: ${aws_cloudwatch_event_rule.example.id}
      http_target:
        query_string_parameters:
          Body: $.detail.body
        header_parameters:
          Env: Test

resource:
  aws_cloudwatch_event_rule:
    example:

resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

resource:
  aws_api_gateway_stage:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      deployment_id: ${aws_api_gateway_deployment.example.id}
```

## Cross-Account Event Bus target

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - events.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    event_bus_invoke_remote_event_bus:
      name: event-bus-invoke-remote-event-bus
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    event_bus_invoke_remote_event_bus:
      statement:
        effect: Allow
        actions: 
          - "events:PutEvents"
        resources: 
          - "arn:aws:events:eu-west-1:1234567890:event-bus/My-Event-Bus"

resource:
  aws_iam_policy:
    event_bus_invoke_remote_event_bus:
      name: event_bus_invoke_remote_event_bus
      policy: ${data.aws_iam_policy_document.event_bus_invoke_remote_event_bus.json}

resource:
  aws_iam_role_policy_attachment:
    event_bus_invoke_remote_event_bus:
      role: ${aws_iam_role.event_bus_invoke_remote_event_bus.name}
      policy_arn: ${aws_iam_policy.event_bus_invoke_remote_event_bus.arn}

resource:
  aws_cloudwatch_event_rule:
    stop_instances:
      name: StopInstance
      description: Stop instances nightly
      schedule_expression: "cron(0 0 * * ? *)"

resource:
  aws_cloudwatch_event_target:
    stop_instances:
      target_id: StopInstance
      arn: "arn:aws:events:eu-west-1:1234567890:event-bus/My-Event-Bus"
      rule: ${aws_cloudwatch_event_rule.stop_instances.name}
      role_arn: ${aws_iam_role.event_bus_invoke_remote_event_bus.arn}
```

## Input Transformer Usage - JSON Object

```yaml
resource:
  aws_cloudwatch_event_target:
    example:
      arn: ${aws_lambda_function.example.arn}
      rule: ${aws_cloudwatch_event_rule.example.id}
      input_transformer:
        input_paths:
          instance: "$.detail.instance"
          status: "$.detail.status"
        input_template: |
          {
          "instance_id": <instance>,
          "instance_status": <status>
          }

resource:
  aws_cloudwatch_event_rule:
    example:
```

## Input Transformer Usage - Simple String

```yaml
resource:
  aws_cloudwatch_event_target:
    example:
      arn: ${aws_lambda_function.example.arn}
      rule: ${aws_cloudwatch_event_rule.example.id}
      input_transformer:
        input_paths:
          instance: "$.detail.instance"
          status: "$.detail.status"
        input_template: '"<instance> is in state <status>"'

resource:
  aws_cloudwatch_event_rule:
    example:
```

## Cloudwatch Log Group Usage

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: /aws/events/guardduty/logs
      retention_in_days: 1

data:
  aws_iam_policy_document:
    example_log_policy:
      statement:
        effect: Allow
        actions:
          - "logs:CreateLogStream"
        resources:
          - "${aws_cloudwatch_log_group.example.arn}:*"
        principals:
          type: Service
          identifiers:
            - events.amazonaws.com
            - delivery.logs.amazonaws.com
      statement:
        effect: Allow
        actions:
          - "logs:PutLogEvents"
        resources:
          - "${aws_cloudwatch_log_group.example.arn}:*:*"
        principals:
          type: Service
          identifiers:
            - events.amazonaws.com
            - delivery.logs.amazonaws.com
        condition:
          test: ArnEquals
          values: 
            - ${aws_cloudwatch_event_rule.example.arn}

resource:
  aws_cloudwatch_log_resource_policy:
    example:
      policy_document: ${data.aws_iam_policy_document.example_log_policy.json}
      policy_name: guardduty-log-publishing-policy

resource:
  aws_cloudwatch_event_rule:
    example:
      name: guard-duty_event_rule
      description: GuardDuty Findings
      event_pattern: 'example-json-policy'
      tags:
        Environment: example

resource:
  aws_cloudwatch_event_target:
    example:
      rule: ${aws_cloudwatch_event_rule.example.name}
      arn: ${aws_cloudwatch_log_group.example.arn}
```

## AppSync Usage

```yaml
resource:
  aws_cloudwatch_event_rule:
    invoke_appsync_mutation:
      name: invoke-appsync-mutation
      description: schedule_batch_test
      schedule_expression: rate(5 minutes)

resource:
  aws_cloudwatch_event_target:
    invoke_appsync_mutation:
      arn: replaced-value
      rule: ${aws_cloudwatch_event_rule.invoke_appsync_mutation.id}
      role_arn: ${aws_iam_role.appsync_mutation_role.arn}
      input_transformer:
        input_paths:
          input: $.detail.input
        input_template: |
          {
          "input": <input>
          }
      appsync_target:
        graphql_operation: "mutation TestMutation($input:MutationInput!){testMutation(input: $input) {test}}"

resource:
  aws_iam_role:
    appsync_mutation_role:
      name: appsync-mutation-role
      assume_role_policy: ${data.aws_iam_policy_document.appsync_mutation_role_trust.json}

data:
  aws_iam_policy_document:
    appsync_mutation_role_trust:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - events.amazonaws.com

data:
  aws_iam_policy_document:
    appsync_mutation_role_policy_document:
      statement:
        actions: 
          - "appsync:GraphQL"
        effect: Allow
        resources:
          - ${aws_appsync_graphql_api.graphql-api.arn}

resource:
  aws_iam_policy:
    appsync_mutation_role_policy:
      name: appsync-mutation-role-policy
      policy: ${data.aws_iam_policy_document.appsync_mutation_role_policy_document.json}

resource:
  aws_iam_role_policy_attachment:
    appsync_mutation_role_attachment:
      policy_arn: ${aws_iam_policy.appsync_mutation_role_policy.arn}
      role: ${aws_iam_role.appsync_mutation_role.name}

resource:
  aws_appsync_graphql_api:
    graphql-api:
      name: api
      authentication_type: AWS_IAM
      schema: |
        schema {
        mutation: Mutation
        query: Query
        }
        
        type Query {
        testQuery: String
        }
        
        type Mutation {
        testMutation(input: MutationInput!): TestMutationResult
        }
        
        type TestMutationResult {
        test: String
        }
        
        input MutationInput {
        testInput: String
        }
```
