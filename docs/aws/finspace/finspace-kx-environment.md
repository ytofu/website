# Finspace Kx Environment

Manage Finspace Kx Environment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: Sample KMS Key
      deletion_window_in_days: 7

resource:
  aws_finspace_kx_environment:
    example:
      name: my-tf-kx-environment
      kms_key_id: ${aws_kms_key.example.arn}
```

## With Transit Gateway Configuration

```yaml
resource:
  aws_kms_key:
    example:
      description: Sample KMS Key
      deletion_window_in_days: 7

resource:
  aws_ec2_transit_gateway:
    example:
      description: example

resource:
  aws_finspace_kx_environment:
    example_env:
      name: my-tf-kx-environment
      description: Environment description
      kms_key_id: ${aws_kms_key.example.arn}
      transit_gateway_configuration:
        transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
        routable_cidr_space: 100.64.0.0/26
      custom_dns_configuration:
        custom_dns_server_name: example.finspace.amazonaws.com
        custom_dns_server_ip: 10.0.0.76
```

## With Transit Gateway Attachment Network ACL Configuration

```yaml
resource:
  aws_kms_key:
    example:
      description: Sample KMS Key
      deletion_window_in_days: 7

resource:
  aws_ec2_transit_gateway:
    example:
      description: example

resource:
  aws_finspace_kx_environment:
    example_env:
      name: my-tf-kx-environment
      description: Environment description
      kms_key_id: ${aws_kms_key.example.arn}
      transit_gateway_configuration:
        transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
        routable_cidr_space: 100.64.0.0/26
        attachment_network_acl_configuration:
          rule_number: 1
          protocol: 6
          rule_action: allow
          cidr_block: 0.0.0.0/0
          port_range:
            from: 53
            to: 53
          icmp_type_code:
            type: -1
            code: -1
      custom_dns_configuration:
        custom_dns_server_name: example.finspace.amazonaws.com
        custom_dns_server_ip: 10.0.0.76
```
