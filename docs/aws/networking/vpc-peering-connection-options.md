# Resource: aws_vpc_peering_connection_options

Provides a resource to manage VPC peering connection options.

## Basic Example

```yaml
resource:
  aws_vpc:
    foo:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpc:
    bar:
      cidr_block: 10.1.0.0/16

resource:
  aws_vpc_peering_connection:
    foo:
      vpc_id: ${aws_vpc.foo.id}
      peer_vpc_id: ${aws_vpc.bar.id}
      auto_accept: true

resource:
  aws_vpc_peering_connection_options:
    foo:
      vpc_peering_connection_id: ${aws_vpc_peering_connection.foo.id}
      accepter:
        allow_remote_vpc_dns_resolution: true
```

## Cross-Account Usage

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_support: true
      enable_dns_hostnames: true

resource:
  aws_vpc:
    peer:
      cidr_block: 10.1.0.0/16
      enable_dns_support: true
      enable_dns_hostnames: true

data:
  aws_caller_identity:
    peer:

resource:
  aws_vpc_peering_connection:
    peer:
      vpc_id: ${aws_vpc.main.id}
      peer_vpc_id: ${aws_vpc.peer.id}
      peer_owner_id: ${data.aws_caller_identity.peer.account_id}
      auto_accept: false
      tags:
        Side: Requester

resource:
  aws_vpc_peering_connection_accepter:
    peer:
      vpc_peering_connection_id: ${aws_vpc_peering_connection.peer.id}
      auto_accept: true
      tags:
        Side: Accepter

resource:
  aws_vpc_peering_connection_options:
    requester:
      vpc_peering_connection_id: ${aws_vpc_peering_connection_accepter.peer.id}
      requester:
        allow_remote_vpc_dns_resolution: true

resource:
  aws_vpc_peering_connection_options:
    accepter:
      vpc_peering_connection_id: ${aws_vpc_peering_connection_accepter.peer.id}
      accepter:
        allow_remote_vpc_dns_resolution: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_peering_connection_id` - (Required) The ID of the requester VPC peering connection.
* `accepter` (Optional) - An optional configuration block that allows for [VPC Peering Connection](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) options to be set for the VPC that accepts the peering connection (a maximum of one).
* `requester` (Optional) - A optional configuration block that allows for [VPC Peering Connection](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) options to be set for the VPC that requests the peering connection (a maximum of one).

#### Accepter and Requester Arguments

* `allow_remote_vpc_dns_resolution` - (Optional) Allow a local VPC to resolve public DNS hostnames to private IP addresses when queried from instances in the peer VPC.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC Peering Connection Options.

## Import

```bash
ytofu import aws_vpc_peering_connection_options.foo pcx-111aaa111
```
