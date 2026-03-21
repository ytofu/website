# Subnet

Manage Subnet resources using ytofu YAML.

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
