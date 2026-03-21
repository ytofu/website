# Resource: aws_networkfirewall_vpc_endpoint_association

Manages a firewall endpoint for an AWS Network Firewall firewall.

## Basic Example

```yaml
resource:
  aws_networkfirewall_vpc_endpoint_association:
    example:
      firewall_arn: ${aws_networkfirewall_firewall.example.arn}
      vpc_id: ${aws_vpc.example.id}
      subnet_mapping:
        subnet_id: ${aws_subnet.example.id}
      tags:
        Name: example endpoint
```

## Argument Reference

This resource supports the following arguments:

* `description` (Optional) - A description of the VPC endpoint association.
* `firewall_arn` (Required) - The Amazon Resource Name (ARN) that identifies the firewall.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `subnet_mapping` (Required) - The ID for a subnet that's used in an association with a firewall. See [Subnet Mapping](#subnet-mapping) below for details.
* `tags` - (Optional) Map of resource tags to associate with the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_id` (Required) - The unique identifier of the VPC for the endpoint association.

### Subnet Mapping

The `subnet_mapping` block supports the following arguments:

* `ip_address_type` - (Optional) The subnet's IP address type. Valid values: `"DUALSTACK"`, `"IPV4"`.
* `subnet_id` - (Required) The unique identifier for the subnet.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `vpc_endpoint_association_arn` - ARN of the VPC Endpoint Association.
* `vpc_endpoint_association_id` - The unique identifier of the VPC endpoint association.
* `vpc_endpoint_association_status` - Nested list of information about the current status of the VPC Endpoint Association.
    * `association_sync_state` - Set of subnets configured for use by the VPC Endpoint Association.
        * `attachment` - Nested list describing the attachment status of the firewall's VPC Endpoint Association with a single VPC subnet.
            * `endpoint_id` - The identifier of the VPC endpoint that AWS Network Firewall has instantiated in the subnet. You use this to identify the firewall endpoint in the VPC route tables, when you redirect the VPC traffic through the endpoint.
            * `subnet_id` - The unique identifier of the subnet that you've specified to be used for a VPC Endpoint Association endpoint.
        * `availability_zone` - The Availability Zone where the subnet is configured.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_networkfirewall_vpc_endpoint_association.example arn:aws:network-firewall:us-west-1:123456789012:vpc-endpoint-association/example
```
