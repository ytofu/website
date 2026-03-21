# Resource: aws_codeconnections_connection

ytofu resource for managing an AWS CodeConnections Connection.

## Basic Example

```yaml
resource:
  aws_codeconnections_connection:
    example:
      name: example-connection
      provider_type: Bitbucket
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the connection to be created. The name must be unique in the calling AWS account. Changing `name` will create a new resource.
* `provider_type` - (Optional) The name of the external provider where your third-party code repository is configured. Changing `provider_type` will create a new resource. Conflicts with `host_arn`.
* `host_arn` - (Optional) The Amazon Resource Name (ARN) of the host associated with the connection. Conflicts with `provider_type`
* `tags` - (Optional) Map of key-value resource tags to associate with the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The codeconnections connection ARN.
* `connection_status` - The codeconnections connection status. Possible values are `PENDING`, `AVAILABLE` and `ERROR`.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_codeconnections_connection.test-connection arn:aws:codeconnections:us-west-1:0123456789:connection/79d4d357-a2ee-41e4-b350-2fe39ae59448
```
