# Resource: aws_eip

Provides an Elastic IP resource.

## Basic Example

```yaml
resource:
  aws_eip:
    lb:
      instance: ${aws_instance.web.id}
      domain: vpc
```

## Multiple EIPs associated with a single network interface

```yaml
resource:
  aws_network_interface:
    multi-ip:
      subnet_id: ${aws_subnet.main.id}
      private_ips: 
        - 10.0.0.10
        - 10.0.0.11

  aws_eip:
    one:
      domain: vpc
      network_interface: ${aws_network_interface.multi-ip.id}
      associate_with_private_ip: 10.0.0.10

  aws_eip:
    two:
      domain: vpc
      network_interface: ${aws_network_interface.multi-ip.id}
      associate_with_private_ip: 10.0.0.11```

## Attaching an EIP to an Instance with a pre-assigned private ip (VPC Only)

```yaml
resource:
  aws_vpc:
    default:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true

  aws_internet_gateway:
    gw:
      vpc_id: ${aws_vpc.default.id}

  aws_subnet:
    tf_test_subnet:
      vpc_id: ${aws_vpc.default.id}
      cidr_block: 10.0.0.0/24
      map_public_ip_on_launch: true
      depends_on: 
        - ${aws_internet_gateway.gw}

  aws_instance:
    foo:
      ami: ami-5189a661
      instance_type: t2.micro
      private_ip: 10.0.0.12
      subnet_id: ${aws_subnet.tf_test_subnet.id}

  aws_eip:
    bar:
      domain: vpc
      instance: ${aws_instance.foo.id}
      associate_with_private_ip: 10.0.0.12
      depends_on: 
        - ${aws_internet_gateway.gw}```

## Allocating EIP from the BYOIP pool

```yaml
resource:
  aws_eip:
    byoip-ip:
      domain: vpc
      public_ipv4_pool: ipv4pool-ec2-012345
```

## Allocating EIP from the IPAM Pool

```yaml
resource:
  aws_eip:
    ipam-ip:
      domain: vpc
      ipam_pool_id: ipam-pool-07ccc86aa41bef7ce
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `address` - (Optional) IP address from an EC2 BYOIP pool. This option is only available for VPC EIPs.
* `associate_with_private_ip` - (Optional) User-specified primary or secondary private IP address to associate with the Elastic IP address. If no private IP address is specified, the Elastic IP address is associated with the primary private IP address.
* `customer_owned_ipv4_pool` - (Optional) ID  of a customer-owned address pool. For more on customer owned IP addressed check out [Customer-owned IP addresses guide](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-networking-components.html#ip-addressing).
* `domain` - (Optional) Indicates if this EIP is for use in VPC (`vpc`).
* `instance` - (Optional) EC2 instance ID.
* `ipam_pool_id`- (Optional) The ID of an IPAM pool which has an Amazon-provided or BYOIP public IPv4 CIDR provisioned to it.
* `network_border_group` - (Optional) Location from which the IP address is advertised. Use this parameter to limit the address to this location.
* `network_interface` - (Optional) Network interface ID to associate with.
* `public_ipv4_pool` - (Optional) EC2 IPv4 address pool identifier or `amazon`.
  This option is only available for VPC EIPs.
* `tags` - (Optional) Map of tags to assign to the resource. Tags can only be applied to EIPs in a VPC. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `allocation_id` - ID that AWS assigns to represent the allocation of the Elastic IP address for use with instances in a VPC.
* `association_id` - ID representing the association of the address with an instance in a VPC.
* `carrier_ip` - Carrier IP address.
* `customer_owned_ip` - Customer owned IP.
* `id` - Contains the EIP allocation ID.
* `private_dns` - The Private DNS associated with the Elastic IP address (if in VPC).
* `private_ip` - Contains the private IP address (if in VPC).
* `ptr_record` - The DNS pointer (PTR) record for the IP address.
* `public_dns` - Public DNS associated with the Elastic IP address.
* `public_ip` - Contains the public IP address.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `read` - (Default `15m`)
- `update` - (Default `5m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_eip.bar eipalloc-00a10e96
```
