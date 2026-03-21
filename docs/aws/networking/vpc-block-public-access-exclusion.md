# Resource: aws_vpc_block_public_access_exclusion

ytofu resource for managing an AWS EC2 (Elastic Compute Cloud) VPC Block Public Access Exclusion.

## Basic Example

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.1.0.0/16

  aws_vpc_block_public_access_exclusion:
    test:
      vpc_id: ${aws_vpc.test.id}
      internet_gateway_exclusion_mode: allow-bidirectional```

## Usage with subnet id

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.1.0.0/16

  aws_subnet:
    test:
      cidr_block: 10.1.1.0/24
      vpc_id: ${aws_vpc.test.id}

  aws_vpc_block_public_access_exclusion:
    test:
      subnet_id: ${aws_subnet.test.id}
      internet_gateway_exclusion_mode: allow-egress```

## Argument Reference

The following arguments are required:

* `internet_gateway_exclusion_mode` - (Required) Mode of exclusion from Block Public Access. The allowed values are `allow-egress` and `allow-bidirectional`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_id` - (Optional) Id of the VPC to which this exclusion applies. Either this or the subnet_id needs to be provided.
* `subnet_id` - (Optional) Id of the subnet to which this exclusion applies. Either this or the vpc_id needs to be provided.
* `tags` - (Optional) A map of tags to assign to the exclusion. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC Block Public Access Exclusion.
* `resource_arn` - The Amazon Resource Name (ARN) the excluded resource.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_vpc_block_public_access_exclusion.example vpcbpa-exclude-1234abcd
```
