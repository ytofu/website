# Resource: aws_dynamodb_contributor_insights

Provides a DynamoDB contributor insights resource

## Basic Example

```yaml
resource:
  aws_dynamodb_contributor_insights:
    test:
      table_name: ExampleTableName
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `table_name` - (Required) The name of the table to enable contributor insights
* `index_name` - (Optional) The global secondary index name
* `mode` - (Optional) argument to specify the [CloudWatch contributor insights mode](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/contributorinsights_HowItWorks.html#contributorinsights_HowItWorks.Modes)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

## Import

```bash
ytofu import aws_dynamodb_contributor_insights.test name:ExampleTableName/index:ExampleIndexName/123456789012
```
