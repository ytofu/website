# VPC Peering Connection

Manage VPC Peering Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_peering_connection:
    foo:
      peer_owner_id: example-peer_owner_id
      peer_vpc_id: ${aws_vpc.bar.id}
      vpc_id: ${aws_vpc.foo.id}
```
