# Resource: aws_egress_only_internet_gateway

[IPv6 only] Creates an egress-only Internet gateway for your VPC.
An egress-only Internet gateway is used to enable outbound communication
over IPv6 from instances in your VPC to the Internet, and prevents hosts
outside of your VPC from initiating an IPv6 connection with your instance.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.1.0.0/16
      assign_generated_ipv6_cidr_block: true

  aws_egress_only_internet_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      tags:
        Name: main```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_id` - (Required) The VPC ID to create in.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the egress-only Internet gateway.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_egress_only_internet_gateway.example eigw-015e0e244e24dfe8a
```
