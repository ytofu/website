# Resource: aws_ram_resource_association

Manages a Resource Access Manager (RAM) Resource Association.

## Basic Example

```yaml
resource:
  aws_ram_resource_association:
    example:
      resource_arn: ${aws_subnet.example.arn}
      resource_share_arn: ${aws_ram_resource_share.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) Amazon Resource Name (ARN) of the resource to associate with the RAM Resource Share.
* `resource_share_arn` - (Required) Amazon Resource Name (ARN) of the RAM Resource Share.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Name (ARN) of the resource share.

## Import

```bash
ytofu import aws_ram_resource_association.example arn:aws:ram:eu-west-1:123456789012:resource-share/73da1ab9-b94a-4ba3-8eb4-45917f7f4b12,arn:aws:ec2:eu-west-1:123456789012:subnet/subnet-12345678
```
