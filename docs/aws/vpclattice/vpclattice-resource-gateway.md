# Resource: aws_vpclattice_resource_gateway

ytofu resource for managing an AWS VPC Lattice Resource Gateway.

## Basic Example

```yaml
resource:
  aws_vpclattice_resource_gateway:
    example:
      name: Example
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
      tags:
        Environment: Example
```

## Specifying IP address type

```yaml
resource:
  aws_vpclattice_resource_gateway:
    example:
      name: Example
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
      ip_address_type: DUALSTACK
      tags:
        Environment: Example
```

## With security groups

```yaml
resource:
  aws_vpclattice_resource_gateway:
    example:
      name: Example
      vpc_id: ${aws_vpc.example.id}
      security_group_ids: 
        - ${aws_security_group.test.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
```

## Argument Reference

The following arguments are required:

* `name` - Name of the resource gateway.
* `subnet_ids` - IDs of the VPC subnets in which to create the resource gateway.
* `vpc_id` - ID of the VPC for the resource gateway.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `ip_address_type` - (Optional) IP address type used by the resource gateway. Valid values are `IPV4`, `IPV6`, and `DUALSTACK`. The IP address type of a resource gateway must be compatible with the subnets of the resource gateway and the IP address type of the resource.
* `ipv4_addresses_per_eni` - (Optional) The number of IPv4 addresses per ENI for your resource. This argument is only applicable to `IPV4` and `DUALSTACK` IP address types. Defaults to `16`.
* `security_group_ids` - (Optional) Security group IDs associated with the resource gateway. The security groups must be in the same VPC.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the resource gateway.
* `id` - ID of the resource gateway.
* `status` - Status of the resource gateway.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_vpclattice_resource_gateway.example rgw-0a1b2c3d4e5f
```
