# VPC Peering Connection Accepter

Manage VPC Peering Connection Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpc:
    peer:
      cidr_block: 10.1.0.0/16

data:
  aws_caller_identity:
    peer:

resource:
  aws_vpc_peering_connection:
    peer:
      vpc_id: ${aws_vpc.main.id}
      peer_vpc_id: ${aws_vpc.peer.id}
      peer_owner_id: ${data.aws_caller_identity.peer.account_id}
      peer_region: us-west-2
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
```

## Cross-Region Peering (Same Account) Terraform AWS Provider v6 (and above)

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpc:
    peer:
      region: us-west-2
      cidr_block: 10.1.0.0/16

resource:
  aws_vpc_peering_connection:
    peer:
      vpc_id: ${aws_vpc.main.id}
      peer_vpc_id: ${aws_vpc.peer.id}
      peer_region: us-west-2
      auto_accept: false
      tags:
        Side: Requester

resource:
  aws_vpc_peering_connection_accepter:
    peer:
      region: us-west-2
      vpc_peering_connection_id: ${aws_vpc_peering_connection.peer.id}
      auto_accept: true
      tags:
        Side: Accepter
```
