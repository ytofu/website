# Resource: aws_dax_parameter_group

Provides a DAX Parameter Group resource.

## Basic Example

```yaml
resource:
  aws_dax_parameter_group:
    example:
      name: example
      parameters:
        name: query-ttl-millis
        value: 100000
      parameters:
        name: record-ttl-millis
        value: 100000
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the parameter group.
* `description` - (Optional, ForceNew) A description of the parameter group.
* `parameters` - (Optional) The parameters of the parameter group.

## parameters

`parameters` supports the following:

* `name` - (Required) The name of the parameter.
* `value` - (Required) The value for the parameter.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the parameter group.

## Import

```bash
ytofu import aws_dax_parameter_group.example my_dax_pg
```
