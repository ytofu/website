# EIP

Manage EIP resources using ytofu YAML.

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

resource:
  aws_eip:
    one:
      domain: vpc
      network_interface: ${aws_network_interface.multi-ip.id}
      associate_with_private_ip: 10.0.0.10

resource:
  aws_eip:
    two:
      domain: vpc
      network_interface: ${aws_network_interface.multi-ip.id}
      associate_with_private_ip: 10.0.0.11
```

## Attaching an EIP to an Instance with a pre-assigned private ip (VPC Only)

```yaml
resource:
  aws_vpc:
    default:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true

resource:
  aws_internet_gateway:
    gw:
      vpc_id: ${aws_vpc.default.id}

resource:
  aws_subnet:
    tf_test_subnet:
      vpc_id: ${aws_vpc.default.id}
      cidr_block: 10.0.0.0/24
      map_public_ip_on_launch: true
      depends_on: 
        - ${aws_internet_gateway.gw}

resource:
  aws_instance:
    foo:
      ami: ami-5189a661
      instance_type: t2.micro
      private_ip: 10.0.0.12
      subnet_id: ${aws_subnet.tf_test_subnet.id}

resource:
  aws_eip:
    bar:
      domain: vpc
      instance: ${aws_instance.foo.id}
      associate_with_private_ip: 10.0.0.12
      depends_on: 
        - ${aws_internet_gateway.gw}
```

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
