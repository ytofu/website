# Resource: aws_vpc_peering_connection_accepter

Provides a resource to manage the accepter's side of a VPC Peering Connection.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_peering_connection_id` - (Required) The VPC Peering Connection ID to manage.
* `auto_accept` - (Optional) Whether or not to accept the peering request. Defaults to `false`.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Removing `aws_vpc_peering_connection_accepter` from your configuration

AWS allows a cross-account VPC Peering Connection to be deleted from either the requester's or accepter's side.
However, ytofu only allows the VPC Peering Connection to be deleted from the requester's side
by removing the corresponding `aws_vpc_peering_connection` resource from your configuration.
Removing a `aws_vpc_peering_connection_accepter` resource from your configuration will remove it
from your statefile and management, **but will not destroy the VPC Peering Connection.**

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC Peering Connection.
* `accept_status` - The status of the VPC Peering Connection request.
* `vpc_id` - The ID of the accepter VPC.
* `peer_vpc_id` - The ID of the requester VPC.
* `peer_owner_id` - The AWS account ID of the owner of the requester VPC.
* `peer_region` - The region of the accepter VPC.
* `accepter` - A configuration block that describes [VPC Peering Connection]
(https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) options set for the accepter VPC.
* `requester` - A configuration block that describes [VPC Peering Connection]
(https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) options set for the requester VPC.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

#### Accepter and Requester Attribute Reference

* `allow_remote_vpc_dns_resolution` - Indicates whether a local VPC can resolve public DNS hostnames to
private IP addresses when queried from instances in a peer VPC.

## Import

```bash
ytofu import aws_vpc_peering_connection_accepter.example pcx-12345678
```
