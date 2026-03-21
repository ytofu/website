# Resource: aws_subnet

Provides an VPC subnet resource.

## Basic Example

```yaml
resource:
  aws_subnet:
    main:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      tags:
        Name: Main
```

## Subnets In Secondary VPC CIDR Blocks

```yaml
resource:
  aws_vpc_ipv4_cidr_block_association:
    secondary_cidr:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 172.20.0.0/16

resource:
  aws_subnet:
    in_secondary_cidr:
      vpc_id: ${aws_vpc_ipv4_cidr_block_association.secondary_cidr.vpc_id}
      cidr_block: 172.20.0.0/24
```

## IPAM-Managed Subnets

```yaml
data:
  aws_region:
    current:

resource:
  aws_vpc_ipam:
    test:
      operating_regions:
        region_name: ${data.aws_region.current.region}

resource:
  aws_vpc_ipam_pool:
    test:
      address_family: ipv4
      ipam_scope_id: ${aws_vpc_ipam.test.private_default_scope_id}
      locale: ${data.aws_region.current.name}

resource:
  aws_vpc_ipam_pool_cidr:
    test:
      ipam_pool_id: ${aws_vpc_ipam_pool.test.id}
      cidr: 10.0.0.0/16

resource:
  aws_vpc:
    test:
      ipv4_ipam_pool_id: ${aws_vpc_ipam_pool.test.id}
      ipv4_netmask_length: 24
      depends_on: 
        - ${aws_vpc_ipam_pool_cidr.test}

resource:
  aws_vpc_ipam_pool:
    vpc:
      address_family: ipv4
      ipam_scope_id: ${aws_vpc_ipam.test.private_default_scope_id}
      locale: ${data.aws_region.current.name}
      source_ipam_pool_id: ${aws_vpc_ipam_pool.test.id}
      source_resource:
        resource_id: ${aws_vpc.test.id}
        resource_owner: ${data.aws_caller_identity.current.account_id}
        resource_region: ${data.aws_region.current.name}
        resource_type: vpc

resource:
  aws_vpc_ipam_pool_cidr:
    vpc:
      ipam_pool_id: ${aws_vpc_ipam_pool.vpc.id}
      cidr: ${aws_vpc.test.cidr_block}

resource:
  aws_subnet:
    test:
      vpc_id: ${aws_vpc.test.id}
      ipv4_ipam_pool_id: ${aws_vpc_ipam_pool.vpc.id}
      ipv4_netmask_length: 28
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      depends_on: 
        - ${aws_vpc_ipam_pool_cidr.vpc}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `assign_ipv6_address_on_creation` - (Optional) Specify true to indicate
    that network interfaces created in the specified subnet should be
    assigned an IPv6 address. Default is `false`
* `availability_zone` - (Optional) AZ for the subnet.
* `availability_zone_id` - (Optional) AZ ID of the subnet. This argument is not supported in all regions or partitions. If necessary, use `availability_zone` instead.
* `cidr_block` - (Optional) The IPv4 CIDR block for the subnet.
* `customer_owned_ipv4_pool` - (Optional) The customer owned IPv4 address pool. Typically used with the `map_customer_owned_ip_on_launch` argument. The `outpost_arn` argument must be specified when configured.
* `enable_dns64` - (Optional) Indicates whether DNS queries made to the Amazon-provided DNS Resolver in this subnet should return synthetic IPv6 addresses for IPv4-only destinations. Default: `false`.
* `enable_lni_at_device_index` - (Optional) Indicates the device position for local network interfaces in this subnet. For example, 1 indicates local network interfaces in this subnet are the secondary network interface (eth1). A local network interface cannot be the primary network interface (eth0).
* `enable_resource_name_dns_aaaa_record_on_launch` - (Optional) Indicates whether to respond to DNS queries for instance hostnames with DNS AAAA records. Default: `false`.
* `enable_resource_name_dns_a_record_on_launch` - (Optional) Indicates whether to respond to DNS queries for instance hostnames with DNS A records. Default: `false`.
* `ipv6_cidr_block` - (Optional) The IPv6 network range for the subnet,
    in CIDR notation. The subnet size must use a /64 prefix length. If the existing IPv6 subnet was created with `assign_ipv6_address_on_creation = true`, changing this value will force resource recreation.
* `ipv6_native` - (Optional) Indicates whether to create an IPv6-only subnet. Default: `false`.
* `ipv4_ipam_pool_id` - (Optional) ID of an IPv4 VPC Resource Planning IPAM Pool. The CIDR of this pool is used to allocate the CIDR for the subnet.
* `ipv4_netmask_length` - (Optional) Netmask. Requires specifying a `ipv4_ipam_pool_id`.
* `ipv6_ipam_pool_id` - (Optional) ID of an IPv6 VPC Resource Planning IPAM Pool. The CIDR of this pool is used to allocate the CIDR for the subnet.
* `ipv6_netmask_length` - (Optional) Netmask. Requires specifying a `ipv6_ipam_pool_id`. Valid values are from 44 to 64 in increments of 4.
* `map_customer_owned_ip_on_launch` -  (Optional) Specify `true` to indicate that network interfaces created in the subnet should be assigned a customer owned IP address. The `customer_owned_ipv4_pool` and `outpost_arn` arguments must be specified when set to `true`. Default is `false`.
* `map_public_ip_on_launch` -  (Optional) Specify true to indicate that instances launched into the subnet should be assigned a public IP address. Default is `false`.
* `outpost_arn` - (Optional) The Amazon Resource Name (ARN) of the Outpost.
* `private_dns_hostname_type_on_launch` - (Optional) The type of hostnames to assign to instances in the subnet at launch. For IPv6-only subnets, an instance DNS name must be based on the instance ID. For dual-stack and IPv4-only subnets, you can specify whether DNS names use the instance IPv4 address or the instance ID. Valid values: `ip-name`, `resource-name`.
* `vpc_id` - (Required) The VPC ID.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the subnet
* `arn` - The ARN of the subnet.
* `ipv6_cidr_block_association_id` - The association ID for the IPv6 CIDR block.
* `owner_id` - The ID of the AWS account that owns the subnet.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_subnet.example subnet-9d4a7b6c
```
