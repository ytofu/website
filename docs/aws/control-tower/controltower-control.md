# Resource: aws_controltower_control

Allows the application of pre-defined controls to organizational units. For more information on usage, please see the
[AWS Control Tower User Guide](https://docs.aws.amazon.com/controltower/latest/userguide/enable-guardrails.html).

## Basic Example

```yaml
data:
  aws_region:
    current:

  aws_organizations_organization:
    example:

  aws_organizations_organizational_units:
    example:
      parent_id: ${data.aws_organizations_organization.example.roots[0].id}

resource:
  aws_controltower_control:
    example:
      control_identifier: "arn:aws:controltower:${data.aws_region.current.region}::control/AWS-GR_EC2_VOLUME_INUSE_CHECK"
      target_identifier: 'example-list'
      parameters:
        key: AllowedRegions
        value: example-value```

## Argument Reference

The following arguments are required:

* `control_identifier` - (Required) The ARN of the control. Only Strongly recommended and Elective controls are permitted, with the exception of the Region deny guardrail.
* `target_identifier` - (Required) The ARN of the organizational unit.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `parameters` - (Optional) Parameter values which are specified to configure the control when you enable it. See [Parameters](#parameters) for more details.

### Parameters

* `key` - (Required) The name of the parameter.
* `value` - (Required) The value of the parameter.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the EnabledControl resource.
* `id` - The ARN of the organizational unit.

## Import

```bash
ytofu import aws_controltower_control.example arn:aws:organizations::123456789101:ou/o-qqaejywet/ou-qg5o-ufbhdtv3,arn:aws:controltower:us-east-1::control/WTDSMKDKDNLE
```
