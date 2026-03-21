# Transfer Tag

Manage Transfer Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_server:
    example:
      identity_provider_type: SERVICE_MANAGED

resource:
  aws_transfer_tag:
    zone_id:
      resource_arn: ${aws_transfer_server.example.arn}
      key: "transfer:route53HostedZoneId"
      value: /hostedzone/MyHostedZoneId

resource:
  aws_transfer_tag:
    hostname:
      resource_arn: ${aws_transfer_server.example.arn}
      key: "transfer:customHostname"
      value: example.com
```
