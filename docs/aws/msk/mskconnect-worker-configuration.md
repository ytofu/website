# Resource: aws_mskconnect_worker_configuration

Provides an Amazon MSK Connect Worker Configuration Resource.

## Basic Example

```yaml
resource:
  aws_mskconnect_worker_configuration:
    example:
      name: example
      properties_file_content: |
        key.converter=org.apache.kafka.connect.storage.StringConverter
        value.converter=org.apache.kafka.connect.storage.StringConverter
```

## Argument Reference

The following arguments are required:

* `name` - (Required, Forces new resource) The name of the worker configuration.
* `properties_file_content` - (Required, Forces new resource) Contents of connect-distributed.properties file. The value can be either base64 encoded or in raw format.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional, Forces new resource) A summary description of the worker configuration.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - the Amazon Resource Name (ARN) of the worker configuration.
* `latest_revision` - an ID of the latest successfully created revision of the worker configuration.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_mskconnect_worker_configuration.example 'arn:aws:kafkaconnect:eu-central-1:123456789012:worker-configuration/example/8848493b-7fcc-478c-a646-4a52634e3378-4'
```
