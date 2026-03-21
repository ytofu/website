# VPC Peering Connection Options

Manage VPC Peering Connection Options resources using ytofu YAML.

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
