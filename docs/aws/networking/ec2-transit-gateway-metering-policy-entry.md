# EC2 Transit Gateway Metering Policy Entry

Manage EC2 Transit Gateway Metering Policy Entry resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_metering_policy_entry:
    example:
      transit_gateway_metering_policy_id: ${aws_ec2_transit_gateway_metering_policy.example.transit_gateway_metering_policy_id}
      policy_rule_number: 100
      metered_account: source-attachment-owner
```

## Full Traffic Matching Rule

```yaml
resource:
  aws_ec2_transit_gateway_metering_policy_entry:
    example:
      transit_gateway_metering_policy_id: ${aws_ec2_transit_gateway_metering_policy.example.transit_gateway_metering_policy_id}
      policy_rule_number: 200
      metered_account: destination-attachment-owner
      source_cidr_block: 10.0.0.0/8
      destination_cidr_block: 172.16.0.0/12
      protocol: 6
```
