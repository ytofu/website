# Networkfirewall Firewall Transit Gateway Attachment Accepter

Manage Networkfirewall Firewall Transit Gateway Attachment Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkfirewall_firewall_transit_gateway_attachment_accepter:
    example:
      transit_gateway_attachment_id: ${aws_networkfirewall_firewall.example.firewall_status[0].transit_gateway_attachment_sync_state[0].attachment_id}
```
