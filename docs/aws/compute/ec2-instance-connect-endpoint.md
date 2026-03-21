# EC2 Instance Connect Endpoint

Manage EC2 Instance Connect Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_instance_connect_endpoint:
    example:
      subnet_id: ${aws_subnet.example.id}
```
