# Networkmanager Attachment Accepter

Manage Networkmanager Attachment Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_attachment_accepter:
    example:
      attachment_id: ${aws_networkmanager_vpc_attachment.example.id}
      attachment_type: ${aws_networkmanager_vpc_attachment.example.attachment_type}
```

## Site-to-Site VPN Attachment

```yaml
resource:
  aws_networkmanager_attachment_accepter:
    example:
      attachment_id: ${aws_networkmanager_site_to_site_vpn_attachment.example.id}
      attachment_type: ${aws_networkmanager_site_to_site_vpn_attachment.example.attachment_type}
```

## Connect Attachment

```yaml
resource:
  aws_networkmanager_attachment_accepter:
    example:
      attachment_id: ${aws_networkmanager_connect_attachment.example.id}
      attachment_type: ${aws_networkmanager_connect_attachment.example.attachment_type}
```

## Transit Gateway Route Table Attachment

```yaml
resource:
  aws_networkmanager_attachment_accepter:
    example:
      attachment_id: ${aws_networkmanager_transit_gateway_route_table_attachment.example.id}
      attachment_type: ${aws_networkmanager_transit_gateway_route_table_attachment.example.attachment_type}
```

## Direct Connect Gateway Attachment

```yaml
resource:
  aws_networkmanager_attachment_accepter:
    example:
      attachment_id: ${aws_networkmanager_dx_gateway_attachment.example.id}
      attachment_type: ${aws_networkmanager_dx_gateway_attachment.example.attachment_type}
```
