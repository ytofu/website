# Resource: aws_ami_launch_permission

Adds a launch permission to an Amazon Machine Image (AMI).

## Basic Example

```yaml
resource:
  aws_ami_launch_permission:
    example:
      image_id: ami-12345678
      account_id: 123456789012
```

## Public Access

```yaml
resource:
  aws_ami_launch_permission:
    example:
      image_id: ami-12345678
      group: all
```

## Organization Access

```yaml
data:
  aws_organizations_organization:
    current:

resource:
  aws_ami_launch_permission:
    example:
      image_id: ami-12345678
      organization_arn: ${data.aws_organizations_organization.current.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Optional) AWS account ID for the launch permission.
* `group` - (Optional) Name of the group for the launch permission. Valid values: `"all"`.
* `image_id` - (Required) ID of the AMI.
* `organization_arn` - (Optional) ARN of an organization for the launch permission.
* `organizational_unit_arn` - (Optional) ARN of an organizational unit for the launch permission.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Launch permission ID.

## Import

```bash
ytofu import aws_ami_launch_permission.example 123456789012/ami-12345678
```
