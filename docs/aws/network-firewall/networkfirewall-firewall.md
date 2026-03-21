# Networkfirewall Firewall

Manage Networkfirewall Firewall resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkfirewall_firewall:
    example:
      name: example
      firewall_policy_arn: ${aws_networkfirewall_firewall_policy.example.arn}
      vpc_id: ${aws_vpc.example.id}
      enabled_analysis_types: 
        - TLS_SNI
        - HTTP_HOST
      subnet_mapping:
        subnet_id: ${aws_subnet.example.id}
      tags:
        Tag1: Value1
        Tag2: Value2
      timeouts:
        create: 40m
        update: 50m
        delete: 1h
```

## Transit Gateway Attached Firewall

```yaml
data:
  aws_availability_zones:
    example:
      state: available

resource:
  aws_networkfirewall_firewall:
    example:
      name: example
      firewall_policy_arn: ${aws_networkfirewall_firewall_policy.example.arn}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      availability_zone_mapping:
        availability_zone_id: ${data.aws_availability_zones.example.zone_ids[0]}
      availability_zone_mapping:
        availability_zone_id: ${data.aws_availability_zones.example.zone_ids[1]}
```
