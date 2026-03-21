# Networkmanager Attachment Routing Policy Label

Manage Networkmanager Attachment Routing Policy Label resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_attachment_routing_policy_label:
    example:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      attachment_id: ${aws_networkmanager_vpc_attachment.example.id}
      routing_policy_label: attachmentPolicyLabel
```
