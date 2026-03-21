# Resource: aws_vpc_ipam_pool_cidr_allocation

Allocates (reserves) a CIDR from an IPAM address pool, preventing usage by IPAM. Only works for private IPv4.

## Basic Example

```yaml
data:
  aws_region:
    current:

resource:
  aws_vpc_ipam_pool_cidr_allocation:
    example:
      ipam_pool_id: ${aws_vpc_ipam_pool.example.id}
      cidr: 172.20.0.0/24
      depends_on:
        - ${aws_vpc_ipam_pool_cidr.example}

  aws_vpc_ipam_pool_cidr:
    example:
      ipam_pool_id: ${aws_vpc_ipam_pool.example.id}
      cidr: 172.20.0.0/16

  aws_vpc_ipam_pool:
    example:
      address_family: ipv4
      ipam_scope_id: ${aws_vpc_ipam.example.private_default_scope_id}
      locale: ${data.aws_region.current.region}

  aws_vpc_ipam:
    example:
      operating_regions:
        region_name: ${data.aws_region.current.region}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cidr` - (Optional, Forces new resource) The CIDR you want to assign to the pool.
* `description` - (Optional, Forces new resource) The description for the allocation.
* `disallowed_cidrs` - (Optional, Forces new resource) Exclude a particular CIDR range from being returned by the pool.
* `ipam_pool_id` - (Required, Forces new resource) The ID of the pool to which you want to assign a CIDR.
* `netmask_length` - (Optional, Forces new resource) The netmask length of the CIDR you would like to allocate to the IPAM pool. Valid Values: `0-128`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the allocation.
* `resource_id` - The ID of the resource.
* `resource_owner` - The owner of the resource.
* `resource_type` - The type of the resource.

## Import

```bash
ytofu import aws_vpc_ipam_pool_cidr_allocation.example ipam-pool-alloc-0dc6d196509c049ba8b549ff99f639736_ipam-pool-07cfb559e0921fcbe
```
