# Networkmonitor Probe

Manage Networkmonitor Probe resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmonitor_monitor:
    example:
      aggregation_period: 30
      monitor_name: example

resource:
  aws_networkmonitor_probe:
    example:
      monitor_name: ${aws_networkmonitor_monitor.example.monitor_name}
      destination: 127.0.0.1
      destination_port: 80
      protocol: TCP
      source_arn: ${aws_subnet.example.arn}
      packet_size: 200
```
