# Resource: aws_networkmanager_transit_gateway_registration

Manages a Network Manager transit gateway registration. Registers a transit gateway to a global network. The transit gateway can be in any AWS Region, but it must be owned by the same AWS account that owns the global network. You cannot register a transit gateway in more than one global network.

## Basic Example

```yaml
resource:
  aws_networkmanager_global_network:
    example:
      description: example

  aws_ec2_transit_gateway:
    example:

  aws_networkmanager_transit_gateway_registration:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      transit_gateway_arn: ${aws_ec2_transit_gateway.example.arn}```

## Argument Reference

The following arguments are required:

* `global_network_id` - (Required) ID of the Global Network to register to.
* `transit_gateway_arn` - (Required) ARN of the Transit Gateway to register.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_transit_gateway_registration.example global-network-0d47f6t230mz46dy4,arn:aws:ec2:us-west-2:123456789012:transit-gateway/tgw-123abc05e04123abc
```
