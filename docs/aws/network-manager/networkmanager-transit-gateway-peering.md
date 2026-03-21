# Networkmanager Transit Gateway Peering

Manage Networkmanager Transit Gateway Peering resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_transit_gateway_peering:
    example:
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      transit_gateway_arn: ${aws_ec2_transit_gateway.example.arn}
      depends_on:
        - ${aws_ec2_transit_gateway_policy_table.example}
        - ${aws_networkmanager_core_network_policy_attachment.example}
```
