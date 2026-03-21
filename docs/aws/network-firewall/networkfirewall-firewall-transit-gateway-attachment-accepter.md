# Resource: aws_networkfirewall_firewall_transit_gateway_attachment_accepter

Manages an AWS Network Firewall Firewall Transit Gateway Attachment Accepter.

## Basic Example

```yaml
resource:
  aws_networkfirewall_firewall_transit_gateway_attachment_accepter:
    example:
      transit_gateway_attachment_id: ${aws_networkfirewall_firewall.example.firewall_status[0].transit_gateway_attachment_sync_state[0].attachment_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `transit_gateway_attachment_id` - (Required) The unique identifier of the transit gateway attachment to accept. This ID is returned in the response when creating a transit gateway-attached firewall.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `delete` - (Default `60m`)

## Import

```bash
ytofu import aws_networkfirewall_firewall_transit_gateway_attachment_accepter.example tgw-attach-0c3b7e9570eee089c
```
