# Transfer Family Tag

Manage Transfer server tags for custom hostnames using ytofu YAML.

## Custom Hostname

```yaml
resource:
  aws_transfer_tag:
    zone_id:
      resource_arn: ${aws_transfer_server.example.arn}
      key: aws:transfer:route53HostedZoneId
      value: /hostedzone/${aws_route53_zone.example.zone_id}

  aws_transfer_tag:
    hostname:
      resource_arn: ${aws_transfer_server.example.arn}
      key: aws:transfer:customHostname
      value: sftp.example.com
```
