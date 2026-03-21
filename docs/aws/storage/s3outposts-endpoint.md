# S3outposts Endpoint

Manage S3outposts Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3outposts_endpoint:
    example:
      outpost_id: ${data.aws_outposts_outpost.example.id}
      security_group_id: ${aws_security_group.example.id}
      subnet_id: ${aws_subnet.example.id}
```
