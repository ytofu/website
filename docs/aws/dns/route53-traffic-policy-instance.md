# Route53 Traffic Policy Instance

Manage Route53 Traffic Policy Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_traffic_policy_instance:
    test:
      name: test.example.com
      traffic_policy_id: b3gb108f-ea6f-45a5-baab-9d112d8b4037
      traffic_policy_version: 1
      hosted_zone_id: Z033120931TAQO548OGJC
      ttl: 360
```
