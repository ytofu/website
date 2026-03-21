# Resource: aws_api_gateway_stage

Manages an API Gateway Stage. A stage is a named reference to a deployment, which can be done via the [`aws_api_gateway_deployment` resource](api_gateway_deployment.html). Stages can be optionally managed further with the [`aws_api_gateway_base_path_mapping` resource](api_gateway_base_path_mapping.html), [`aws_api_gateway_domain_name` resource](api_gateway_domain_name.html), and [`aws_api_method_settings` resource](api_gateway_method_settings.html). For more information, see the [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-stages.html).

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      body: '{ "openapi": "3.0.1" "info": { "title": "example" "version": "1.0" } "paths": { "/path1" = { "get": { x-amazon-apigateway-"integration": { "httpMethod": "GET" "payloadFormatVersion": "1.0" "type": "HTTP_PROXY" "uri": "https://ip-ranges.amazonaws.com/ip-ranges.json" } } } } }'
      name: example

  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example

  aws_api_gateway_method_settings:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: ${aws_api_gateway_stage.example.stage_name}
      method_path: "*/*"
      settings:
        metrics_enabled: true
        logging_level: INFO```

## Managing the API Logging CloudWatch Log Group

```yaml
resource:
  aws_api_gateway_rest_api:
    example:

  aws_api_gateway_stage:
    example:
      depends_on: 
        - ${aws_cloudwatch_log_group.example}
      stage_name: example-stage_name

  aws_cloudwatch_log_group:
    example:
      name: "API-Gateway-Execution-Logs_${aws_api_gateway_rest_api.example.id}/example-stage_name"
      retention_in_days: 7```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) ID of the associated REST API
* `stage_name` - (Required) Name of the stage
* `deployment_id` - (Required) ID of the deployment that the stage points to
* `access_log_settings` - (Optional) Enables access logs for the API stage. See [Access Log Settings](#access-log-settings) below.
* `cache_cluster_enabled` - (Optional) Whether a cache cluster is enabled for the stage
* `cache_cluster_size` - (Optional) Size of the cache cluster for the stage, if enabled. Allowed values include `0.5`, `1.6`, `6.1`, `13.5`, `28.4`, `58.2`, `118` and `237`.
* `canary_settings` - (Optional) Configuration settings of a canary deployment. See [Canary Settings](#canary-settings) below.
* `client_certificate_id` - (Optional) Identifier of a client certificate for the stage.
* `description` - (Optional) Description of the stage.
* `documentation_version` - (Optional) Version of the associated API documentation.
* `variables` - (Optional) Map that defines the stage variables.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `xray_tracing_enabled` - (Optional) Whether active tracing with X-ray is enabled. Defaults to `false`.

### Access Log Settings

* `destination_arn` - (Required) ARN of the CloudWatch Logs log group or Kinesis Data Firehose delivery stream to receive access logs. If you specify a Kinesis Data Firehose delivery stream, the stream name must begin with `amazon-apigateway-`. Automatically removes trailing `:*` if present.
* `format` - (Required) Formatting and values recorded in the logs.
For more information on configuring the log format rules visit the AWS [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html)

### Canary Settings

* `deployment_id` - (Required) ID of the deployment that the canary points to.
* `percent_traffic` - (Optional) Percent `0.0` - `100.0` of traffic to divert to the canary deployment.
* `stage_variable_overrides` - (Optional) Map of overridden stage `variables` (including new variables) for the canary deployment.
* `use_stage_cache` - (Optional) Whether the canary deployment uses the stage cache. Defaults to false.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN
* `id` - ID of the stage
* `invoke_url` - URL to invoke the API pointing to the stage,
  e.g., `https://z4675bid1j.execute-api.eu-west-2.amazonaws.com/prod`
* `execution_arn` - Execution ARN to be used in `lambda_permission`'s `source_arn`
  when allowing API Gateway to invoke a Lambda function,
  e.g., `arn:aws:execute-api:eu-west-2:123456789012:z4675bid1j/prod`
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `web_acl_arn` - ARN of the WebAcl associated with the Stage.

## Import

```bash
ytofu import aws_api_gateway_stage.example 12345abcde/example
```
