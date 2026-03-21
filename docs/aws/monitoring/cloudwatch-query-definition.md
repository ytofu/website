# Resource: aws_cloudwatch_query_definition

Provides a CloudWatch Logs query definition resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_query_definition:
    example:
      name: custom_query
      log_group_names:
        - /aws/logGroup1
        - /aws/logGroup2
      query_string: |
        fields @timestamp, @message
        | sort @timestamp desc
        | limit 25
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the query.
* `query_string` - (Required) The query to save. You can read more about CloudWatch Logs Query Syntax in the [documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax.html).
* `log_group_names` - (Optional) Specific log groups to use with the query.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `query_definition_id` - The query definition ID.

## Import

```bash
ytofu import aws_cloudwatch_query_definition.example arn:aws:logs:us-west-2:123456789012:query-definition:269951d7-6f75-496d-9d7b-6b7a5486bdbd
```
