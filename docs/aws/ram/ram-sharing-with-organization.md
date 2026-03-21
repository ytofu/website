# Resource: aws_ram_sharing_with_organization

Manages Resource Access Manager (RAM) Resource Sharing with AWS Organizations. If you enable sharing with your organization, you can share resources without using invitations. Refer to the [AWS RAM user guide](https://docs.aws.amazon.com/ram/latest/userguide/getting-started-sharing.html#getting-started-sharing-orgs) for more details.

## Basic Example

```yaml
resource:
  aws_ram_sharing_with_organization:
    example:
```

## Argument Reference

This resource does not support any arguments.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS Account ID.

## Import

```bash
ytofu import aws_ram_sharing_with_organization.example 123456789012
```
