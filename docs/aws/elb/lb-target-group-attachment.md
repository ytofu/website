# LB Target Group Attachment

Manage LB Target Group Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lb_target_group_attachment:
    test:
      target_group_arn: ${aws_lb_target_group.test.arn}
      target_id: ${aws_instance.test.id}
      port: 80

resource:
  aws_lb_target_group:
    test:

resource:
  aws_instance:
    test:
```

## Lambda Target

```yaml
resource:
  aws_lambda_permission:
    with_lb:
      statement_id: AllowExecutionFromlb
      action: "lambda:InvokeFunction"
      function_name: ${aws_lambda_function.test.function_name}
      principal: elasticloadbalancing.amazonaws.com
      source_arn: ${aws_lb_target_group.test.arn}

resource:
  aws_lb_target_group:
    test:
      name: test
      target_type: lambda

resource:
  aws_lambda_function:
    test:

resource:
  aws_lb_target_group_attachment:
    test:
      target_group_arn: ${aws_lb_target_group.test.arn}
      target_id: ${aws_lambda_function.test.arn}
      depends_on: 
        - ${aws_lambda_permission.with_lb}
```

## Target using QUIC

```yaml
resource:
  aws_lb_target_group:
    test:
      name: test
      port: 443
      protocol: QUIC

resource:
  aws_lb_target_group_attachment:
    test:
      target_group_arn: ${aws_lb_target_group.test.arn}
      target_id: ${aws_instance.test.id}
      port: 443
      quic_server_id: 0x1a2b3c4d5e6f7a8b

resource:
  aws_instance:
    test:
```

## Registering Multiple Targets

```yaml
resource:
  aws_instance:
    example:

resource:
  aws_lb_target_group:
    example:

resource:
  aws_lb_target_group_attachment:
    example:
      target_group_arn: ${aws_lb_target_group.example.arn}
      target_id: example-id
      port: 80
```
