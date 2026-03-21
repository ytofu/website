# Resource: aws_lambda_alias

Manages an AWS Lambda Alias. Use this resource to create an alias that points to a specific Lambda function version for traffic management and deployment strategies.

## Basic Example

```yaml
resource:
  aws_lambda_alias:
    example:
      name: production
      description: Production environment alias
      function_name: ${aws_lambda_function.example.arn}
      function_version: 1
```

## Alias with Traffic Splitting

```yaml
resource:
  aws_lambda_alias:
    example:
      name: staging
      description: Staging environment with traffic splitting
      function_name: ${aws_lambda_function.example.function_name}
      function_version: 2
      routing_config:
        additional_version_weights: 
```

## Blue-Green Deployment Alias

```yaml
resource:
  aws_lambda_alias:
    example:
      name: live
      description: Live traffic with gradual rollout to new version
      function_name: ${aws_lambda_function.example.function_name}
      function_version: "5" # Current stable version
      routing_config:
        additional_version_weights: 
```

## Development Alias

```yaml
resource:
  aws_lambda_alias:
    example:
      name: dev
      description: Development environment - always points to latest
      function_name: ${aws_lambda_function.example.function_name}
      function_version: $LATEST
```

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Name or ARN of the Lambda function.
* `function_version` - (Required) Lambda function version for which you are creating the alias. Pattern: `(\$LATEST|[0-9]+)`.
* `name` - (Required) Name for the alias. Pattern: `(?!^[0-9]+$)([a-zA-Z0-9-_]+)`.

The following arguments are optional:

* `description` - (Optional) Description of the alias.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `routing_config` - (Optional) Lambda alias' route configuration settings. [See below](#routing_config-configuration-block).

### routing_config Configuration Block

* `additional_version_weights` - (Optional) Map that defines the proportion of events that should be sent to different versions of a Lambda function.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN identifying your Lambda function alias.
* `invoke_arn` - ARN to be used for invoking Lambda Function from API Gateway - to be used in `aws_api_gateway_integration`'s `uri`.
