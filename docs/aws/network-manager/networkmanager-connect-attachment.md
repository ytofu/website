# Networkmanager Connect Attachment

Manage Networkmanager Connect Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_vpc_attachment:
    example:
      subnet_arns: ${aws_subnet.example[*].arn}
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpc_arn: ${aws_vpc.example.arn}

resource:
  aws_networkmanager_connect_attachment:
    example:
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      transport_attachment_id: ${aws_networkmanager_vpc_attachment.example.id}
      edge_location: ${aws_networkmanager_vpc_attachment.example.edge_location}
      options:
        protocol: GRE
```

## Usage with attachment accepter

```yaml
resource:
  aws_networkmanager_vpc_attachment:
    example:
      subnet_arns: ${aws_subnet.example[*].arn}
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpc_arn: ${aws_vpc.example.arn}

resource:
  aws_networkmanager_attachment_accepter:
    example:
      attachment_id: ${aws_networkmanager_vpc_attachment.example.id}
      attachment_type: ${aws_networkmanager_vpc_attachment.example.attachment_type}

resource:
  aws_networkmanager_connect_attachment:
    example:
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      transport_attachment_id: ${aws_networkmanager_vpc_attachment.example.id}
      edge_location: ${aws_networkmanager_vpc_attachment.example.edge_location}
      options:
        protocol: GRE
      depends_on:
        - ${aws_networkmanager_attachment_accepter.example}

resource:
  aws_networkmanager_attachment_accepter:
    example2:
      attachment_id: ${aws_networkmanager_connect_attachment.example.id}
      attachment_type: ${aws_networkmanager_connect_attachment.example.attachment_type}
```
