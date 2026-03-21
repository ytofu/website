# Resource: aws_internet_gateway_attachment

Provides a resource to create a VPC Internet Gateway Attachment.

## Basic Example

```yaml
resource:
  aws_internet_gateway_attachment:
    example:
      internet_gateway_id: ${aws_internet_gateway.example.id}
      vpc_id: ${aws_vpc.example.id}

  aws_vpc:
    example:
      cidr_block: 10.1.0.0/16

  aws_internet_gateway:
    example:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `internet_gateway_id` - (Required) The ID of the internet gateway.
* `vpc_id` - (Required) The ID of the VPC.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC and Internet Gateway separated by a colon.

## Timeouts

Configuration options:

- `create` - (Default `20m`)
- `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_internet_gateway_attachment.example igw-c0a643a9:vpc-123456
```
