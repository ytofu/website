# Resource: aws_ram_principal_association

Provides a Resource Access Manager (RAM) principal association. Depending if [RAM Sharing with AWS Organizations is enabled](https://docs.aws.amazon.com/ram/latest/userguide/getting-started-sharing.html#getting-started-sharing-orgs), the RAM behavior with different principal types changes.

## Basic Example

```yaml
resource:
  aws_ram_resource_share:
    example:
      allow_external_principals: true

  aws_ram_principal_association:
    example:
      principal: 111111111111
      resource_share_arn: ${aws_ram_resource_share.example.arn}```

## AWS Organization

```yaml
resource:
  aws_ram_principal_association:
    example:
      principal: ${aws_organizations_organization.example.arn}
      resource_share_arn: ${aws_ram_resource_share.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `principal` - (Required) The principal to associate with the resource share. Possible values are an AWS account ID, an AWS Organizations Organization ARN, or an AWS Organizations Organization Unit ARN.
* `resource_share_arn` - (Required) The Amazon Resource Name (ARN) of the resource share.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Name (ARN) of the Resource Share and the principal, separated by a comma.

## Import

```bash
ytofu import aws_ram_principal_association.example arn:aws:ram:eu-west-1:123456789012:resource-share/73da1ab9-b94a-4ba3-8eb4-45917f7f4b12,123456789012
```
