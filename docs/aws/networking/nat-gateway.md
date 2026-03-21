# Resource: aws_nat_gateway

Provides a resource to create a VPC NAT Gateway.

## Basic Example

```yaml
resource:
  aws_nat_gateway:
    example:
      allocation_id: ${aws_eip.example.id}
      subnet_id: ${aws_subnet.example.id}
      tags:
        Name: gw NAT
      depends_on: 
        - ${aws_internet_gateway.example}
```

## Public NAT with Secondary Private IP Addresses

```yaml
resource:
  aws_nat_gateway:
    example:
      allocation_id: ${aws_eip.example.id}
      subnet_id: ${aws_subnet.example.id}
      secondary_allocation_ids: 
        - ${aws_eip.secondary.id}
      secondary_private_ip_addresses: 
        - 10.0.1.5
```

## Private NAT

```yaml
resource:
  aws_nat_gateway:
    example:
      connectivity_type: private
      subnet_id: ${aws_subnet.example.id}
```

## Private NAT with Secondary Private IP Addresses

```yaml
resource:
  aws_nat_gateway:
    example:
      connectivity_type: private
      subnet_id: ${aws_subnet.example.id}
      secondary_private_ip_address_count: 7
```

## Regional NAT Gateway with auto mode

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_internet_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_nat_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      availability_mode: regional
```

## Regional NAT Gateway with manual mode

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_internet_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_eip:
    example:
      domain: vpc

resource:
  aws_nat_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      availability_mode: regional
      availability_zone_address:
        allocation_ids: 
          - ${aws_eip.example[0].id}
        availability_zone: ${data.aws_availability_zones.available.names[0]}
      availability_zone_address:
        allocation_ids: 
          - ${aws_eip.example[1].id}
          - ${aws_eip.example[2].id}
        availability_zone: ${data.aws_availability_zones.available.names[1]}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `allocation_id` - (Optional, zonal NAT gateways only) The Allocation ID of the Elastic IP address for the NAT Gateway. Required when `connectivity_type` is set to `public` and `availability_mode` is set to `zonal`. When `availability_mode` is set to `regional`, this must not be set; instead, use the `availability_zone_address` block to specify EIPs for each AZ.
* `availability_mode` - (Optional) Specifies whether to create a zonal (single-AZ) or regional (multi-AZ) NAT gateway. Valid values are `zonal` and `regional`. Defaults to `zonal`.
* `availability_zone_address` - (Optional, regional NAT gateways only) Repeatable configuration block for the Elastic IP addresses (EIPs) and availability zones for the regional NAT gateway. When not specified, the regional NAT gateway will automatically expand to new AZs and associate EIPs upon detection of an elastic network interface (auto mode). When specified, auto-expansion is disabled (manual mode). See [`availability_zone_address`](#availability_zone_address) below for details.
* `connectivity_type` - (Optional) Connectivity type for the NAT Gateway. Valid values are `private` and `public`. When `availability_mode` is set to `regional`, this must be set to `public`. Defaults to `public`.
* `private_ip` - (Optional, zonal NAT gateways only) The private IPv4 address to assign to the NAT Gateway. If you don't provide an address, a private IPv4 address will be automatically assigned.
* `subnet_id` - (Optional, zonal NAT gateways only) The Subnet ID of the subnet in which to place the NAT Gateway. Required when `availability_mode` is set to `zonal`. Must not be set when `availability_mode` is set to `regional`.
* `secondary_allocation_ids` - (Optional, zonal NAT gateways only) A list of secondary allocation EIP IDs for this NAT Gateway. To remove all secondary allocations an empty list should be specified.
* `secondary_private_ip_address_count` - (Optional, zonal and private NAT gateways only) The number of secondary private IPv4 addresses you want to assign to the NAT Gateway.
* `secondary_private_ip_addresses` - (Optional, zonal NAT gateways only) A list of secondary private IPv4 addresses to assign to the NAT Gateway. To remove all secondary private addresses an empty list should be specified.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_id` - (Optional, regional NAT gateways only) VPC ID where this NAT Gateway will be created. Required when `availability_mode` is set to `regional`.

### `availability_zone_address`

* `allocation_ids` - (Required) List of allocation IDs of the Elastic IP addresses (EIPs) to be used for handling outbound NAT traffic in this specific Availability Zone.
* `availability_zone` - (Optional) Availability Zone (e.g. `us-west-2a`) where this specific NAT gateway configuration will be active. Exactly one of `availability_zone` or `availability_zone_id` must be specified.
* `availability_zone_id` - (Optional) Availability Zone ID (e.g. `usw2-az2`) where this specific NAT gateway configuration will be active. Exactly one of `availability_zone` or `availability_zone_id` must be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `association_id` - (zonal NAT gateways only) The association ID of the Elastic IP address that's associated with the NAT Gateway. Only available when `connectivity_type` is `public`.
* `auto_provision_zones` - (regional NAT gateways only) Indicates whether AWS automatically manages AZ coverage.
* `auto_scaling_ips` - (regional NAT gateways only) Indicates whether AWS automatically allocates additional Elastic IP addresses (EIPs) in an AZ when the NAT gateway needs more ports due to increased concurrent connections to a single destination from that AZ.
* `id` - The ID of the NAT Gateway.
* `network_interface_id` - (zonal NAT gateways only) The ID of the network interface associated with the NAT Gateway.
* `public_ip` - (zonal NAT gateways only) The Elastic IP address associated with the NAT Gateway.
* `regional_nat_gateway_address` - (regional NAT gateways only) Repeatable blocks for information about the IP addresses and network interface associated with the regional NAT gateway.
    * `allocation_id` - Allocation ID of the Elastic IP address.
    * `association_id` - Association ID of the Elastic IP address.
    * `availability_zone` - Availability Zone where this specific NAT gateway configuration is active.
    * `availability_zone_id` - Availability Zone ID where this specific NAT gateway configuration is active
    * `network_interface_id` - ID of the network interface.
    * `public_ip` - Public IP address.
    * `status` - Status of the NAT gateway address.
* `route_table_id` - (regional NAT gateways only) ID of the automatically created route table.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `update` - (Default `10m`)
- `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_nat_gateway.private_gw nat-05dba92075d71c408
```
