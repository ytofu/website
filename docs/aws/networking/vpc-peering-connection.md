# Resource: aws_vpc_peering_connection

Provides a resource to manage a VPC peering connection.

## Basic Example

```yaml
resource:
  aws_vpc_peering_connection:
    foo:
      peer_owner_id: example-peer_owner_id
      peer_vpc_id: ${aws_vpc.bar.id}
      vpc_id: ${aws_vpc.foo.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `peer_owner_id` - (Optional) The AWS account ID of the target peer VPC.
   Defaults to the account ID the [AWS provider][1] is currently connected to, so must be managed if connecting cross-account.
* `peer_vpc_id` - (Required) The ID of the target VPC with which you are creating the VPC Peering Connection.
* `vpc_id` - (Required) The ID of the requester VPC.
* `auto_accept` - (Optional) Accept the peering (both VPCs need to be in the same AWS account and region).
* `peer_region` - (Optional) The region of the accepter VPC of the VPC Peering Connection. `auto_accept` must be `false`,
and use the `aws_vpc_peering_connection_accepter` to manage the accepter side.
* `accepter` (Optional) - An optional configuration block that allows for [VPC Peering Connection](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) options to be set for the VPC that accepts
the peering connection (a maximum of one).
* `requester` (Optional) - A optional configuration block that allows for [VPC Peering Connection](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) options to be set for the VPC that requests
the peering connection (a maximum of one).
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

#### Accepter and Requester Arguments

* `allow_remote_vpc_dns_resolution` - (Optional) Allow a local VPC to resolve public DNS hostnames to
private IP addresses when queried from instances in the peer VPC.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC Peering Connection.
* `accept_status` - The status of the VPC Peering Connection request.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `1m`)
- `update` - (Default `1m`)
- `delete` - (Default `1m`)

## Import

```bash
ytofu import aws_vpc_peering_connection.test_connection pcx-111aaa111
```
