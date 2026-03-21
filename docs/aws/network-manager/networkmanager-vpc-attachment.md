# Networkmanager VPC Attachment

Manage Networkmanager VPC Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_vpc_attachment:
    example:
      subnet_arns: 
        - ${aws_subnet.example.arn}
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpc_arn: ${aws_vpc.example.arn}
```

## Usage with Options

```yaml
resource:
  aws_networkmanager_vpc_attachment:
    example:
      subnet_arns: 
        - ${aws_subnet.example.arn}
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpc_arn: ${aws_vpc.example.arn}
      options:
        appliance_mode_support: false
        dns_support: true
        ipv6_support: false
        security_group_referencing_support: true
```
