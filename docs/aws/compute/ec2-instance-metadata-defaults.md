# EC2 Instance Metadata Defaults

Manage EC2 Instance Metadata Defaults resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_instance_metadata_defaults:
    enforce-imdsv2:
      http_tokens: required
      http_put_response_hop_limit: 1
```
