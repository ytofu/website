# Resource: aws_iot_event_configurations

Manages IoT event configurations.

## Basic Example

```yaml
resource:
  aws_iot_event_configurations:
    example:
      event_configurations: 
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `event_configurations` - (Required) Map. The new event configuration values. You can use only these strings as keys: `THING_GROUP_HIERARCHY`, `THING_GROUP_MEMBERSHIP`, `THING_TYPE`, `THING_TYPE_ASSOCIATION`, `THING_GROUP`, `THING`, `POLICY`, `CA_CERTIFICATE`, `JOB_EXECUTION`, `CERTIFICATE`, `JOB`. Use boolean for values of mapping.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iot_event_configurations.example us-west-2
```
