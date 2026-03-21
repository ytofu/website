# Cloudwatch Log Delivery Destination

Manage Cloudwatch Log Delivery Destination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_delivery_destination:
    example:
      name: example
      delivery_destination_configuration:
        destination_resource_arn: ${aws_cloudwatch_log_group.example.arn}
```

## X-Ray Trace Delivery

```yaml
resource:
  aws_cloudwatch_log_delivery_destination:
    xray:
      name: xray-traces
      delivery_destination_type: XRAY
```
