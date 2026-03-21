# Resource: aws_apprunner_connection

Manages an App Runner Connection.

## Basic Example

```yaml
resource:
  aws_apprunner_connection:
    example:
      connection_name: example
      provider_type: GITHUB
      tags:
        Name: example-apprunner-connection
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `connection_name` - (Required) Name of the connection.
* `provider_type` - (Required) Source repository provider. Valid values: `GITHUB`.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the connection.
* `status` - Current state of the App Runner connection. When the state is `AVAILABLE`, you can use the connection to create an [`aws_apprunner_service` resource](apprunner_service.html).
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_apprunner_connection.example example
```
