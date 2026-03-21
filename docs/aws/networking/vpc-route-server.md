# VPC Route Server

Manage VPC Route Server resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_route_server:
    test:
      amazon_side_asn: 65534
      tags:
        Name: Test
```

## Persist Route and SNS Notification

```yaml
resource:
  aws_vpc_route_server:
    test:
      amazon_side_asn: 65534
      persist_routes: enable
      persist_routes_duration: 2
      sns_notifications_enabled: true
      tags:
        Name: Main Route Server
```
